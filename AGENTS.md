# AGENTS.md

> **Purpose**  
> Primary guide for the Codex agent (CLI + VS Code extension).  
> Works together with **PROJECT_ARCHITECTURE.md** (human-facing architecture, decisions, backlog).  
> Adapt the placeholders `{{...}}` to this repository (see README and PLACEHOLDERS.md for reference).

---

## 1) Read First (Priority)

1. **PROJECT_ARCHITECTURE.md** — source of truth for architecture, decisions, status.
2. **DATABASE_CHANGELOG.md** (if database used) — current DB schema and migration history.
3. **README.md** — setup & quick start.
4. **CONTRIBUTING.md** (if present) — code style, commit/PR rules.
5. **docs/** (if present) — ADRs, diagrams, specs.

> If a file conflicts with this AGENTS.md, prefer **PROJECT_ARCHITECTURE.md** and update this file accordingly.

---

## 2) Project Variables (fill per repo)

- **Project name:** `{{PROJECT_NAME}}`
- **Primary language:** `{{LANGUAGE}}` (TypeScript, Python, Go, Java, etc.)
- **Package manager / build tool:** `{{PKG_MANAGER}}` (pnpm, npm, yarn, poetry, uv, pipenv, Maven, Gradle)
- **Runtime / hosting:** `{{RUNTIME}}` (Node.js, Python, Go, Docker/K8s, serverless, Vercel, Fly, etc.)
- **Database (optional):** `{{DB_ENGINE}}` (PostgreSQL, MySQL, SQLite, MongoDB, None) with migrations in `{{MIGRATIONS_DIR}}`
- **Monorepo?** `{{MONOREPO}}` (Yes / No); if yes: `{{PACKAGES}}`
- **CI system:** `{{CI}}` (GitHub Actions, GitLab CI, CircleCI, None)
- **Entrypoints / dev commands:** see §4 Commands

Keep these in sync with README, PROJECT_ARCHITECTURE, and PLACEHOLDERS.md.

---

## 3) Codex Operating Rules

- **Approvals:** Ask before running shell commands, writing files, changing schema, or modifying CI.
- **Scope:** One focused change set at a time; include a **verification step**.
- **Plan → Diff → Explain:** Propose a short plan, provide minimal diffs, annotate intent & rollback.
- **Prefer smallest safe edits:** Favor additive and reversible changes.
- **No hidden side effects:** Surface assumptions, required env, or migration impacts.

---

## 4) Commands (customize for this repo)

Replace placeholders with real commands.

**Install deps**  
- `{{PKG_MANAGER}} install`

**Dev run (local)**  
- `{{PKG_MANAGER}} run dev`

**Build**  
- `{{PKG_MANAGER}} run build`

**Start (prod)**  
- `{{PKG_MANAGER}} run start`

**Type checks / Lint / Format**  
- `{{PKG_MANAGER}} run type-check`  
- `{{PKG_MANAGER}} run lint --fix`  
- `{{PKG_MANAGER}} run format` _(if applicable)_

**Tests**  
- `{{PKG_MANAGER}} test` (CI)  
- `{{PKG_MANAGER}} run test:watch` (local)  
- Coverage: `{{PKG_MANAGER}} run coverage`

**DB / Infra** _(enable if applicable)_  
- Migrate: `{{MIGRATE_CMD}}`  
- Verify: `{{DB_VERIFY_CMD}}`  
- Infra up/down: `{{INFRA_UP}}` / `{{INFRA_DOWN}}`

> **Agent tip:** Before multi-file edits, run `type-check` + tests to ensure a clean baseline.

---

## 5) Guardrails (Do / Don't)

**Don't**
- Modify DB schema **outside migrations**.
- Commit secrets or `.env*`. Use local `.env.local` (git-ignored) + CI secrets.
- Bypass access layers (repositories/services).
- Run unbounded loops/polling; always add backoff/limits.
- Change CI/CD or deploy without a plan and confirmation.

**Do**
- Keep types/schemas in sync with code and migrations.
- Document architectural changes in **PROJECT_ARCHITECTURE.md**.
- Update **DATABASE_CHANGELOG.md** after DB schema changes.
- Add a verification step for destructive or large refactors.
- Use structured logs and typed errors; avoid silent failures.

---

## 6) Quality Gates

- **Compiles / type-checks:** `{{PKG_MANAGER}} run type-check`
- **Tests pass:** `{{PKG_MANAGER}} test`
- **No runtime errors** in dev run
- **Docs updated:** PROJECT_ARCHITECTURE.md / README.md / DATABASE_CHANGELOG.md (if DB changed)

> Failing any gate → stop and fix before expanding scope.

---

## 7) Repository Structure (adapt to your architecture)

```
{{PROJECT_ROOT}}/
├── {{SOURCE_DIR}}/          # Source code (src/, app/, lib/, cmd/, pkg/)
│   ├── {{COMPONENTS_DIR}}/  # UI components (if frontend)
│   ├── {{SERVICES_DIR}}/    # Business logic / API services
│   ├── {{UTILS_DIR}}/       # Utilities
│   └── {{ENTRY_FILE}}       # Main entry (main.py, App.tsx, main.go)
├── {{TESTS_DIR}}/           # Tests (tests/, __tests__, test/)
├── {{MIGRATIONS_DIR}}/      # Database migrations (if DB used)
├── {{DOCS_DIR}}/            # Documentation
│   └── DATABASE_CHANGELOG.md
├── {{CONFIG_DIR}}/          # Configuration
├── {{BUILD_DIR}}/           # Build output (dist/, build/, target/)
└── {{PACKAGES}}/            # Monorepo packages (if monorepo)
```

Common patterns: `src/`, `app/`, `lib/`, `cmd/`, `pkg/`, `internal/`

---

## 8) Code Style & Conventions (language-agnostic)

- **Naming:** `camelCase` vars/functions, `PascalCase` types/classes/components, `SCREAMING_SNAKE_CASE` constants.
- **Files:** `feature-action.ext`, `module.service.ext`, `useThing.ext`, `thing.repository.ext`.
- **Commits:** Conventional Commits (`feat:`, `fix:`, `chore:`, `refactor:`, `test:`, `docs:`).
- **Errors/Logs:** Typed errors; structured logs; redact secrets.

---

## 9) Data & Migrations (enable if DB present)

- All schema changes via migrations in `{{MIGRATIONS_DIR}}`.  
- Prefer additive, backward-compatible changes; backfill where needed.  
- Verify post-migration with `{{DB_VERIFY_CMD}}` or sanity queries.  
- Provide rollback steps (down migration or documented procedure).
- **Update DATABASE_CHANGELOG.md** after every migration with:
  - Current schema state
  - Migration history entry
  - Rollback procedure
  - Verification queries

---

## 10) External APIs & Rate Limits (enable if applicable)

- Timeouts, retries with exponential backoff, idempotency/dedupe keys.
- Persist progress for large jobs; resume on failure.
- Bound concurrency (queues/worker pools).

---

## 11) Testing Strategy

- **Unit:** core logic (parsers/validators/domain rules).
- **Integration:** DB/repo boundaries, critical API flows.
- **Smoke:** minimal e2e happy paths.
- Prefer deterministic tests; avoid flaky external calls.

---

## 12) Workflow (One change = One verification)

1. Read PROJECT_ARCHITECTURE.md; confirm constraints.
2. If DB changes: Read DATABASE_CHANGELOG.md for current schema.
3. Plan a minimal diff; identify risks/rollback.
4. Implement incrementally; run type-check/tests often.
5. Verify with a concrete step (command/test/sample run).
6. Document changes/decisions:
   - PROJECT_ARCHITECTURE.md (if architectural)
   - DATABASE_CHANGELOG.md (if DB schema changed)
   - README.md (if setup changed)
7. Commit clearly; open PR with checklist.

---

## 13) PR Checklist

- [ ] Scope described and limited
- [ ] Build / type-check / tests pass
- [ ] Migrations (if any) applied and verified
- [ ] DATABASE_CHANGELOG.md updated (if DB changed)
- [ ] Rollback/mitigation documented (if risky)
- [ ] Docs updated (PROJECT_ARCHITECTURE / README / changelog)
- [ ] Logs/screenshots for verification (if relevant)

---

## 14) Playbooks (opt-in)

- **Large refactor:** extract seam → flag → migrate gradually → remove dead code.
- **DB backfill:** add structures → dual-read/write → backfill → flip → remove old path.
- **Rate limits:** lower concurrency; jittered backoff; persist offsets; retry failed batch.
- **Hotfix:** minimal change; add post-hoc tests; document incident/follow-ups.

---

## 15) Related Documentation

### For understanding placeholders:
- **PLACEHOLDERS.md** — Complete reference of all `{{VARIABLES}}` used in templates

### For AI tools:
- **CLAUDE.md** — Alternative guide for Claude Code (if using Claude instead of Codex)

### For architecture:
- **PROJECT_ARCHITECTURE.md** — Architecture decisions, tech stack, backlog
- **DATABASE_CHANGELOG.md** — Database schema history (if DB used)

### For developers:
- **README.md** — Project overview and setup
- **CONTRIBUTING.md** — Development standards (if present)

---

*Keep this file in sync with PROJECT_ARCHITECTURE.md and DATABASE_CHANGELOG.md*  
*Last updated: 2025-10-11*
