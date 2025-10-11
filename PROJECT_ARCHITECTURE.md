### Development & DevOps

- **Package Manager:** `{{PKG_MANAGER}}` (npm / pnpm / yarn / bun / poetry / pip / go mod)
- **Monorepo:** `{{MONOREPO}}` (Yes / No)
  - **Packages:** `{{PACKAGES}}` (if monorepo: @app/web, @app/api, @app/shared, etc.)
- **Version Control:** `{{VCS}}` (Git / GitHub /# Project Architecture Overview

**Project:** `{{PROJECT_NAME}}`  
**Version:** `{{VERSION}}`  
**Last Updated:** `{{LAST_UPDATED}}`  
**Status:** `{{STATUS}}` (Planning / Active Development / Maintenance / Production)

---

## 🎯 Quick Reference

**For Claude Code / Codex:** Read this section first for immediate context

### Critical Architecture Decisions

- **Primary Language:** `{{LANGUAGE}}` (TypeScript / JavaScript / Python / Go / Java / etc.)
- **Framework:** `{{FRAMEWORK}}` (React / Vue / Next.js / FastAPI / Django / Express / etc.)
- **Database:** `{{DB_ENGINE}}` (PostgreSQL / MySQL / SQLite / MongoDB / None)
- **State Management:** `{{STATE_LIB}}` (Zustand / Redux / Context / Pinia / Vuex / N/A)
- **File Storage:** `{{FILES_BACKEND}}` (S3 / OpenAI Files API / Local / Cloudflare R2 / N/A)

### Key Files to Read

- **This file:** Architecture overview and active backlog
- **CLAUDE.md** or **AGENTS.md:** AI tool-specific operational guidelines
- **DATABASE_CHANGELOG.md:** Database structure history (if database used)
- **README.md:** Project overview and setup
- **CONTRIBUTING.md:** Development standards and PR process (if present)

### Active Backlog Location

👉 **See "Current Implementation Status" section below** - this is the SINGLE SOURCE OF TRUTH for what's done and what's planned.

---

## 📊 Technology Stack

> This section is adapted to your project during setup

### Frontend (if applicable)

- **Framework:** `{{FRONTEND_FRAMEWORK}}` (e.g., React 18 / Vue 3 / Svelte / Angular / Next.js)
- **Language:** `{{LANGUAGE}}` (TypeScript / JavaScript)
- **Build Tool:** `{{BUILD_TOOL}}` (Vite / Webpack / Turbopack / esbuild)
- **State Management:** `{{STATE_LIB}}` (Zustand / Redux / Context / Pinia / Signals / N/A)
- **UI Framework:** `{{UI_FRAMEWORK}}` (Tailwind CSS / MUI / Chakra UI / Bootstrap / Custom CSS)
- **Icons:** `{{ICON_LIB}}` (Lucide React / Heroicons / Font Awesome / N/A)
- **Routing:** `{{ROUTING_LIB}}` (React Router / Vue Router / Next.js routing / N/A)

### Backend & Infrastructure

- **Runtime:** `{{RUNTIME}}` (Node.js / Python / Go / Java / .NET)
- **Framework:** `{{BACKEND_FRAMEWORK}}` (Express / FastAPI / Django / Gin / Spring Boot / N/A)
- **Database:** `{{DB_ENGINE}}` (PostgreSQL / MySQL / SQLite / MongoDB / Supabase / None)
- **ORM/Query Builder:** `{{ORM}}` (Prisma / TypeORM / SQLAlchemy / GORM / Drizzle / Raw SQL)
- **Authentication:** `{{AUTH_PROVIDER}}` (Supabase Auth / Auth0 / Clerk / NextAuth / JWT / Custom)
- **File Storage:** `{{FILES_BACKEND}}` (AWS S3 / OpenAI Files API / Cloudflare R2 / Local / N/A)
- **Caching:** `{{CACHE}}` (Redis / Memcached / In-memory / None)

### External Integrations

- **APIs Used:** `{{APIS}}` (OpenAI / Stripe / Twilio / SendGrid / etc.)
- **Analytics:** `{{ANALYTICS}}` (Google Analytics / Posthog / Mixpanel / None)
- **Monitoring:** `{{MONITORING}}` (Sentry / DataDog / New Relic / None)

### Development & DevOps

- **Package Manager:** `{{PKG_MANAGER}}` (npm / pnpm / yarn / bun / poetry / pip / go mod)
- **Monorepo:** `{{MONOREPO}}` (Yes / No)
  - **Packages:** `{{PACKAGES}}` (if monorepo: @app/web, @app/api, @app/shared, etc.)
- **Runtime:** `{{RUNTIME}}` (Node.js 20 / Python 3.12 / Go 1.21 / JVM 17 / .NET 8 / Deno / Bun)
- **Version Control:** `{{VCS}}` (Git / GitHub / GitLab / Bitbucket) GitLab / Bitbucket)
- **CI/CD:** `{{CI}}` (GitHub Actions / GitLab CI / CircleCI / Jenkins / None)
- **Deployment:** `{{DEPLOYMENT}}` (Vercel / Netlify / AWS / Docker / Kubernetes / Traditional server)
- **Testing:** `{{TEST_FRAMEWORK}}` (Vitest / Jest / Pytest / Go test / JUnit / None)

### Key Dependencies

```json
{
  "{{DEPENDENCY_1}}": "{{VERSION_1}}",
  "{{DEPENDENCY_2}}": "{{VERSION_2}}",
  "{{DEPENDENCY_3}}": "{{VERSION_3}}"
}
```

---

## 🗂️ Project Structure

> Adapt to your framework/language. Examples shown for common patterns.

```
{{PROJECT_ROOT}}/
├── {{SOURCE_DIR}}/              # Main source code (src/ app/ lib/)
│   ├── {{COMPONENTS_DIR}}/      # UI components (if frontend)
│   ├── {{PAGES_DIR}}/           # Pages/Routes (if applicable)
│   ├── {{SERVICES_DIR}}/        # Business logic / API services
│   ├── {{UTILS_DIR}}/           # Utility functions
│   ├── {{TYPES_DIR}}/           # Type definitions (if TypeScript)
│   ├── {{STORE_DIR}}/           # State management (if applicable)
│   └── {{ENTRY_FILE}}           # Main entry point (App.tsx / main.py / main.go)
├── {{PUBLIC_DIR}}/              # Static assets (public/ static/)
├── {{TESTS_DIR}}/               # Tests (tests/ __tests__ test/)
├── {{CONFIG_DIR}}/              # Configuration files (config/)
├── {{MIGRATIONS_DIR}}/          # Database migrations (if DB used)
├── {{DOCS_DIR}}/                # Documentation (docs/)
│   └── DATABASE_CHANGELOG.md
├── {{BUILD_DIR}}/               # Build output (dist/ build/ .next/)
├── package.json                 # Dependencies (or requirements.txt / go.mod)
├── {{CONFIG_FILE}}              # Main config (tsconfig.json / pyproject.toml / go.mod)
├── README.md
├── CLAUDE.md or AGENTS.md
└── PROJECT_ARCHITECTURE.md (this file)
```

**Common Structure Examples:**

<details>
<summary>React/Vue/Frontend SPA</summary>

```
src/
├── components/       # Reusable UI components
├── pages/            # Page components
├── hooks/            # Custom hooks (React)
├── composables/      # Composables (Vue)
├── store/            # State management
├── services/         # API calls
├── utils/            # Helper functions
├── types/            # TypeScript types
└── App.tsx/vue
```
</details>

<details>
<summary>Next.js</summary>

```
app/                  # App Router (Next.js 13+)
├── api/              # API routes
├── (routes)/         # Page routes
components/           # Shared components
lib/                  # Utilities and services
public/               # Static assets
```
</details>

<details>
<summary>Python (FastAPI/Django)</summary>

```
src/
├── api/              # API routes/endpoints
├── models/           # Data models
├── schemas/          # Pydantic schemas
├── services/         # Business logic
├── db/               # Database connection
├── utils/            # Utilities
└── main.py
```
</details>

<details>
<summary>Go</summary>

```
cmd/                  # Main applications
pkg/                  # Library code (public)
internal/             # Private application code
api/                  # API definitions
configs/              # Configuration files
scripts/              # Build/deploy scripts
```
</details>

---

## 🏗️ Core Architecture Decisions

> Document your key architectural decisions here. Add more as needed.

### Template: Decision Title

**Decision:** What was decided  
**Context:** What problem were we solving  
**Date:** YYYY-MM-DD

**Alternatives Considered:**
- ❌ Alternative 1 — why rejected
- ❌ Alternative 2 — why rejected

**Rationale:**
- ✅ Reason 1
- ✅ Reason 2
- ✅ Reason 3

**Consequences:**
- Impact on codebase
- Trade-offs made
- Future considerations

---

### 1. {{DECISION_1_TITLE}}

**Decision:** `{{DECISION_1_CHOICE}}`  
**Context:** `{{DECISION_1_CONTEXT}}`  
**Date:** `{{DECISION_1_DATE}}`

**Alternatives Considered:**
- ❌ `{{DECISION_1_ALT_1}}` — `{{DECISION_1_ALT_1_REASON}}`
- ❌ `{{DECISION_1_ALT_2}}` — `{{DECISION_1_ALT_2_REASON}}`

**Rationale:**
- ✅ `{{DECISION_1_REASON_1}}`
- ✅ `{{DECISION_1_REASON_2}}`
- ✅ `{{DECISION_1_REASON_3}}`

**Consequences:**
`{{DECISION_1_CONSEQUENCES}}`

---

### 2. {{DECISION_2_TITLE}}

**Decision:** `{{DECISION_2_CHOICE}}`  
**Context:** `{{DECISION_2_CONTEXT}}`  
**Date:** `{{DECISION_2_DATE}}`

**Rationale:**
- ✅ `{{DECISION_2_REASON_1}}`
- ✅ `{{DECISION_2_REASON_2}}`

---

## 🔧 Key Services & Components

> Document your main services, components, and modules

### {{SERVICE_1_NAME}} ({{SERVICE_1_PATH}})

**Purpose:** `{{SERVICE_1_PURPOSE}}`  
**Key Methods/Functions:**

```{{LANGUAGE}}
{{SERVICE_1_METHODS}}
```

**Architectural Features:**
- `{{SERVICE_1_FEATURE_1}}`
- `{{SERVICE_1_FEATURE_2}}`
- `{{SERVICE_1_FEATURE_3}}`

---

### {{SERVICE_2_NAME}} ({{SERVICE_2_PATH}})

**Purpose:** `{{SERVICE_2_PURPOSE}}`  
**Structure:**

```{{LANGUAGE}}
{{SERVICE_2_STRUCTURE}}
```

**Key Methods/Functions:**
- `{{SERVICE_2_METHOD_1}}` → `{{SERVICE_2_METHOD_1_DESC}}`
- `{{SERVICE_2_METHOD_2}}` → `{{SERVICE_2_METHOD_2_DESC}}`

---

### {{COMPONENT_1_NAME}} ({{COMPONENT_1_PATH}})

**Purpose:** `{{COMPONENT_1_PURPOSE}}`  
**Features:**
- `{{COMPONENT_1_FEATURE_1}}`
- `{{COMPONENT_1_FEATURE_2}}`
- `{{COMPONENT_1_FEATURE_3}}`

---

## 📡 Data Flow & Integration Patterns

> Document how data flows through your application

### 1. {{FLOW_1_NAME}}

```
{{FLOW_1_DIAGRAM}}
```

**Steps:**
1. `{{FLOW_1_STEP_1}}`
2. `{{FLOW_1_STEP_2}}`
3. `{{FLOW_1_STEP_3}}`

---

### 2. {{FLOW_2_NAME}}

```
{{FLOW_2_DIAGRAM}}
```

**Steps:**
1. `{{FLOW_2_STEP_1}}`
2. `{{FLOW_2_STEP_2}}`
3. `{{FLOW_2_STEP_3}}`

---

### 3. {{FLOW_3_NAME}}

```
{{FLOW_3_DIAGRAM}}
```

---

## 🎯 Development Standards

### Code Organization

- **File naming:** `{{FILE_NAMING_CONVENTION}}` (kebab-case / camelCase / PascalCase / snake_case)
- **Component structure:** `{{COMPONENT_STRUCTURE}}` (1 component per file / co-located / feature-based)
- **Import organization:** `{{IMPORT_ORDER}}` (external → internal → relative / alphabetical)
- **Code splitting:** `{{CODE_SPLITTING_STRATEGY}}`

### Database Patterns (if applicable)

- **Primary Keys:** `{{ID_POLICY}}` (UUID / auto-increment / custom)
- **Timestamps:** `{{TIMESTAMP_POLICY}}` (created_at, updated_at / custom)
- **Soft Deletes:** `{{SOFT_DELETE}}` (Yes / No)
- **Indexing Strategy:** `{{INDEXING_POLICY}}`
- **Migrations:** All schema changes via `{{MIGRATIONS_DIR}}`
- **Naming:** `{{DB_NAMING}}` (snake_case / camelCase)

### Error Handling

- **Strategy:** `{{ERROR_HANDLING_STRATEGY}}`
- **Logging:** `{{LOGGING_STRATEGY}}`
- **User-facing errors:** `{{USER_ERROR_STRATEGY}}`
- **Error types:** `{{ERROR_TYPES}}`

### Performance Optimizations

- `{{PERFORMANCE_1}}`
- `{{PERFORMANCE_2}}`
- `{{PERFORMANCE_3}}`

### Security Practices

- **Authentication:** `{{AUTH_STRATEGY}}`
- **Authorization:** `{{AUTHZ_STRATEGY}}`
- **Data validation:** `{{VALIDATION_STRATEGY}}`
- **Secrets management:** `{{SECRETS_MANAGEMENT}}`

---

## 📋 Current Implementation Status

**🎯 THIS IS THE ACTIVE BACKLOG - SINGLE SOURCE OF TRUTH**

### ✅ Completed (v{{COMPLETED_VERSION}})

- [x] `{{COMPLETED_1}}`
- [x] `{{COMPLETED_2}}`
- [x] `{{COMPLETED_3}}`
- [x] `{{COMPLETED_4}}`

### ✅ Completed (v{{COMPLETED_VERSION_2}})

- [x] `{{COMPLETED_5}}`
- [x] `{{COMPLETED_6}}`
- [x] `{{COMPLETED_7}}`

### 🚧 In Development

- [ ] `{{IN_DEV_1}}`
- [ ] `{{IN_DEV_2}}`
- [ ] `{{IN_DEV_3}}`

### 📋 Planned (Priority Order)

1. [ ] `{{PLANNED_1}}`
2. [ ] `{{PLANNED_2}}`
3. [ ] `{{PLANNED_3}}`
4. [ ] `{{PLANNED_4}}`
5. [ ] `{{PLANNED_5}}`

### 🔮 Future Considerations

- [ ] `{{FUTURE_1}}`
- [ ] `{{FUTURE_2}}`
- [ ] `{{FUTURE_3}}`

---

## 📚 Related Documentation

### For AI Tools (Claude Code / Codex):

- **CLAUDE.md** or **AGENTS.md** — Operational guidelines, code patterns, sprint workflow

### For Developers:

- **README.md** — Project overview and setup instructions
- **DATABASE_CHANGELOG.md** — Database evolution history (if DB used)
- **CONTRIBUTING.md** — Development standards and PR process
- **{{DOCS_DIR}}/** — Additional technical documentation

### For Users:

- **User Guide** — End-user documentation (if applicable)
- **API Documentation** — API reference (if applicable)

---

## 🔄 Evolution & Migration Strategy

### Approach to Changes

1. **Document decision** in this file (Core Architecture Decisions section)
2. **Database changes** → Update DATABASE_CHANGELOG.md
3. **Code changes** → Follow patterns in CLAUDE.md/AGENTS.md
4. **Breaking changes** → Version bump, migration guide, feature flags
5. **Documentation** → Update all affected docs

### Migration Pattern

```
Planning → Implementation → Testing → Documentation → Deployment
    ↓           ↓              ↓           ↓            ↓
  This file  Code+Tests    Manual QA   Update docs   Git push
                                          ↓
                              PROJECT_ARCHITECTURE.md
                              DATABASE_CHANGELOG.md (if DB)
                              README.md (if needed)
```

### Version Numbering

- **Major (2.0):** Breaking changes, major architectural shifts
- **Minor (1.3):** New features, backward compatible
- **Patch (1.3.1):** Bug fixes, small improvements

---

## 🎓 Onboarding Guide

### New Developers Start Here:

1. **Read README.md** — Setup and quick start
2. **Read this file** — Architecture overview
3. **Read DATABASE_CHANGELOG.md** — Current DB structure (if DB used)
4. **Read CLAUDE.md or AGENTS.md** — Development workflow and patterns
5. **Run `{{SETUP_COMMAND}}`** — Setup development environment
6. **Review "Current Implementation Status"** — Active tasks and backlog

### Understanding the Codebase:

**Step 1: Entry Point**
- Start with `{{ENTRY_FILE}}` to understand application bootstrap

**Step 2: Core Services**
- Review `{{SERVICES_DIR}}/` for business logic

**Step 3: Data Layer**
- If database: Review DATABASE_CHANGELOG.md and `{{DB_DIR}}/`
- Understand data models and relationships

**Step 4: UI/API Layer**
- Frontend: Review `{{COMPONENTS_DIR}}/` and `{{PAGES_DIR}}/`
- Backend: Review API routes and endpoints

**Step 5: Integration Points**
- External APIs: `{{SERVICES_DIR}}/{{INTEGRATION_DIR}}/`
- State management: `{{STORE_DIR}}/`

---

## 📞 Getting Help

### Questions About:

- **Architecture decisions** → Review this file
- **Database structure** → DATABASE_CHANGELOG.md
- **Setup issues** → README.md
- **Development workflow** → CLAUDE.md or AGENTS.md
- **Code style** → CONTRIBUTING.md

### Contributing:

- Follow development standards above
- Update documentation when making changes
- Run tests before committing: `{{TEST_COMMAND}}`
- Follow sprint workflow (see CLAUDE.md/AGENTS.md)

### Useful Commands:

```bash
# Setup
{{PKG_MANAGER}} install

# Development
{{PKG_MANAGER}} run dev

# Build
{{PKG_MANAGER}} run build

# Test
{{PKG_MANAGER}} test

# Database (if applicable)
{{MIGRATE_CMD}}        # Run migrations
{{DB_VERIFY_CMD}}      # Verify database state

# Deploy (document your specific process)
{{PKG_MANAGER}} run deploy
# or: git push (for auto-deploy platforms)
# or: docker build && docker push
```

---

*This document is maintained to stay current for effective development*  
*Last updated: {{LAST_UPDATED}}*
