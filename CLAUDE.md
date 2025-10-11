---

# Claude Code Working Instructions (Universal)

**Project:** `{{PROJECT_NAME}}`
**Purpose:** Operational guide for efficient development with Claude Code in VS Code
**Last Updated:** 2025-10-11

> Pair this file with **PROJECT_ARCHITECTURE.md** (human-facing architecture, decisions, backlog).
> Keep both in sync. Use `{{...}}` placeholders to adapt to your stack.

---

## 🎯 READ FIRST (Priority Order)

1. **PROJECT_ARCHITECTURE.md** — 🎯 single source of truth (architecture, backlog, decisions)
2. **{{SCHEMA_CHANGELOG_PATH | e.g., supabase/docs/DATABASE_CHANGELOG.md}}** — current DB structure (if DB is used)
3. **README.md** — project overview & quick start
4. **CONTRIBUTING.md** (if present) — style/PR rules

> If a document conflicts with this file, prefer **PROJECT_ARCHITECTURE.md** and then update this file accordingly.

---

## 🚫 NEVER DO

* Change database schema **outside** of migrations.
* Duplicate external API calls (especially in polling) — always dedupe/reuse state.
* Commit secrets or `.env*` files to VCS.
* Bypass access/authorization layers or RLS (if used).
* Start coding major changes **before** reading PROJECT_ARCHITECTURE.md.
* Close a sprint without updating documentation and verifications.
* Run unbounded loops; always add limits/backoff/time budgets.

---

## ✅ ALWAYS DO

* Read PROJECT_ARCHITECTURE.md before architectural or cross-cutting changes.
* Test migrations in a dev/staging environment first.
* Keep types in code synchronized with DB schema (after migrations).
* Ask for confirmation before large refactors or behavior changes.
* Reuse existing patterns (see below) instead of inventing new ones.
* Update **{{SCHEMA_CHANGELOG_PATH}}** after DB changes.
* At sprint completion update: PROJECT_ARCHITECTURE.md, {{SCHEMA_CHANGELOG_PATH}}, CLAUDE.md (if patterns changed), README.md.

---

## 🏗️ Architecture Options (toggle per project)

> Enable the parts that apply; remove what doesn’t.

* **Files/Assets storage:** `{{FILES_BACKEND}}` (e.g., OpenAI Files API / S3 / local)
* **State management (web):** `{{STATE_LIB}}` (e.g., Zustand / Redux / Context / Vuex / Signals)
* **Database:** `{{DB_ENGINE}}` (e.g., Postgres/MySQL/SQLite) with migrations in `{{MIGRATIONS_DIR}}`
* **External APIs:** `{{APIS}}` (e.g., OpenAI / Stripe / Search) — define rate limits & dedupe keys
* **Identifiers:** `{{ID_POLICY}}` (e.g., UUIDv4 for primary keys)
* **Indexing / JSON fields:** `{{JSON_POLICY}}` (e.g., JSONB + GIN for metadata)

> If your API requires Latin-only identifiers, set `{{REQUIRES_LATIN}} = true` and enforce **transliteration** where needed.

---

## 🔧 Essential Implementation Patterns (adapt to your stack)

### 1) Service Method (generic external API)

```typescript
async function doRemoteTask(name: string, client = apiClient): Promise<Result> {
  if (!client) throw new Error('Client not initialized');

  const safeName = {{REQUIRES_LATIN ? 'transliterate(name)' : 'name'}};

  try {
    const res = await client.call({ name: safeName });
    return res as Result;
  } catch (err) {
    console.error('Remote API error:', err);
    throw new Error(`Remote task failed: ${String(err)}`);
  }
}
```

### 2) State Action (store pattern; replace with your state lib)

```typescript
const doAction = async (param: string) => {
  set({ loading: true, error: null });
  try {
    // 1) DB update (if applicable)
    const updated = await db.updateRecord({ param });

    // 2) External sync (optional)
    await doRemoteTask(updated.safeName);

    // 3) State update
    set({ data: updated, loading: false });
  } catch (e: any) {
    set({ loading: false, error: e?.message ?? 'Unknown error' });
  }
};
```

### 3) Migration (run discrete steps; avoid multi-DDL transactions if your RPC/tooling forbids them)

```javascript
// Pseudo-example; replace with your migration runner
await runSql('ALTER TABLE items ADD COLUMN IF NOT EXISTS tag TEXT;');
await runSql('CREATE INDEX IF NOT EXISTS idx_items_tag ON items(tag);');
```

### 4) Types after DB changes (keep nullability & optionality in sync)

```typescript
export interface DbItem {
  id: string;               // primary key policy: {{ID_POLICY}}
  tag: string | null;       // match DB nullability
}
```

### 5) Polling with Dedupe/State Reuse

```typescript
async function waitForResult(id: string) {
  let status = 'pending';
  while (status !== 'completed' && status !== 'failed') {
    await delay(1000);
    const next = await getStatus(id);
    status = next.status;
    set({ lastCheck: next });   // reuse lastCheck to prevent duplicate calls
  }
}
```

### 6) UI Component (selective subscriptions; avoid over-render)

```tsx
export function MyList() {
  const items = useStore(s => s.items);     // subscribe to needed slices
  const loading = useStore(s => s.loading);
  return (
    <div>{loading ? 'Loading…' : items.map(i => <Row key={i.id} {...i} />)}</div>
  );
}
```

---

## 🐛 Top Issues & Quick Fixes (make these yours)

1. **Duplicate API calls**
   Symptom: burst of identical requests / rate-limit errors
   Fix: reuse last check/state; dedupe by `(resourceId, op)`; backoff & caps.

2. **Invalid identifiers / locales**
   Symptom: API rejects non-Latin or special chars
   Fix: enable transliteration/slugify when `{{REQUIRES_LATIN}} = true`.

3. **Migration conflicts**
   Symptom: deadlocks / failures in RPC/DDL
   Fix: split DDL into discrete steps; verify between steps; no implicit transactions if tool forbids.

4. **Type drift after schema changes**
   Symptom: TS errors / runtime nulls
   Fix: update types with accurate nullability; regenerate client types if available.

5. **Wrong file flow**
   Symptom: files not reaching consumer
   Fix: follow agreed flow → Upload to `{{FILES_BACKEND}}` → persist metadata → notify consumers.

---

## 🔄 Sprint Workflow

**Phase 1 — Planning (5–10%)**

1. Understand request & constraints
2. Read PROJECT_ARCHITECTURE.md (what’s done?)
3. Read {{SCHEMA_CHANGELOG_PATH}} (DB state)
4. Draft TODO (+ risks/rollback)
5. Confirm with owner

**Phase 2 — Implementation (70–80%)**

* Bottom-up: DB → types → services → state → UI
* Incremental commits; test continuously

**Phase 3 — Testing (10–15%)**

* Manual: happy path + edges
* Run checks: `{{PKG_MANAGER}} run type-check`, `{{PKG_MANAGER}} run build`, tests

**Phase 4 — Documentation (10–15%)**

* Update PROJECT_ARCHITECTURE.md & {{SCHEMA_CHANGELOG_PATH}}
* Update CLAUDE.md (new patterns/issues)
* Update README (commands/versions)

**Phase 5 — Completion (≈5%)**

* Final commit (see template below)
* Push + ask owner to confirm closure

---

## 📝 Sprint Commit Template

```bash
Sprint: [Short feature brief]

- Implemented: [core functionality]
- Updated: PROJECT_ARCHITECTURE.md{{SCHEMA_CHANGELOG_PATH ? `, ${SCHEMA_CHANGELOG_PATH}` : ''}}
- Fixed: [if any]
- Docs: updated project documentation

Tested:
✓ [test 1]
✓ [test 2]

Co-Authored-By: Claude <noreply@anthropic.com>
```

---

## 🌳 Decision Tree: New Feature

```
New request
├─ DB changes?
│  ├─ YES → read changelog → plan migration → verify
│  └─ NO → code analysis
├─ External APIs touched?
│  ├─ YES → check identifiers/limits/backoff
│  └─ NO → continue
└─ Prior pattern exists?
   ├─ YES → reuse/adapt
   └─ NO  → propose minimal, testable plan
```

---

## 📟 Quick Commands (fill per project)

```bash
# Database (examples)
{{MIGRATE_CMD}}
{{DB_VERIFY_CMD}}

# Development
{{PKG_MANAGER}} run dev
{{PKG_MANAGER}} run build
{{PKG_MANAGER}} run type-check
{{PKG_MANAGER}} test
{{PKG_MANAGER}} run test:watch

# Navigation / Search (examples)
tree -L 2 -I 'node_modules|dist'
rg "search_term" --type {{LANGUAGE | 'ts'}}
```

---

## 🔍 Quick Diagnostics

### Database (examples)

```sql
-- Structure
SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name = '{{TABLE_NAME}}';

-- Indexes
SELECT indexname FROM pg_indexes
WHERE tablename = '{{TABLE_NAME}}';
```

### State (examples)

```typescript
// Browser or Node REPL
const s = useStore.getState?.();
console.log('State:', s);
```

### Network (examples)

```javascript
// Simple client-side interceptor (dev only)
let n = 0;
const origFetch = window.fetch;
window.fetch = (...args) => {
  if (String(args[0]).includes('{{API_HOST_FRAGMENT}}')) {
    console.log(`API call #${++n}:`, args[0]);
  }
  return origFetch.apply(window, args);
};
```

---

## 📋 Sprint Completion Checklist

* [ ] Feature matches acceptance criteria
* [ ] Tests pass (manual + type-check + build + automated where present)
* [ ] No runtime/console errors
* [ ] PROJECT_ARCHITECTURE.md updated
* [ ] {{SCHEMA_CHANGELOG_PATH}} updated (if DB changed)
* [ ] CLAUDE.md updated (if new patterns/issues)
* [ ] README.md updated (if commands changed)
* [ ] User/owner confirmed closure

---

## 📚 Naming Conventions (defaults)

```text
Files:       feature-action.ext, module.service.ext, useThing.ext, thing.repository.ext
Variables:   camelCase
Constants:   SCREAMING_SNAKE_CASE
Classes/TSX: PascalCase
DB:          snake_case tables & columns (e.g., user_profiles, created_at)
Functions:   verbs (fetchData), booleans prefixed (isValid/hasAccess/canRun)
```

---

## 🔄 Quick Recovery

**Rollback migration**

* Use your down migration or a documented rollback procedure.
* Re-sync application types with the DB.

**Reset local state (example)**

```typescript
useStore?.setState?.(initialState);
```

**Emergency reset (git)**

```bash
git stash push -m "backup_$(date +%Y%m%d_%H%M)"
git reset --hard <last_good_commit>
rm -rf node_modules && {{PKG_MANAGER}} install
{{PKG_MANAGER}} run dev
```

---

*Maintain this file at each sprint completion.*
*Last updated: 2025-10-11*
