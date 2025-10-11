# Placeholders Reference

**Purpose:** Complete reference of all `{{PLACEHOLDERS}}` used across project template files  
**Last Updated:** 2025-10-11

> This file helps maintain consistency across CLAUDE.md, AGENTS.md, PROJECT_ARCHITECTURE.md, and DATABASE_CHANGELOG.md

---

## 📋 How to Use

When adapting template files to your project:
1. **Find** the placeholder in this reference
2. **Replace** with your actual value
3. **Keep consistent** across all files

**Adaptation prompts** (in `prompts/` folder) use this reference to know which placeholders to replace.

---

## 🌐 Universal Placeholders

Used in **all or most** template files.

| Placeholder | Description | Examples | Used In |
|-------------|-------------|----------|---------|
| `{{PROJECT_NAME}}` | Your project name | "ChatApp", "E-commerce API", "Analytics Dashboard" | All files |
| `{{LANGUAGE}}` | Primary programming language | TypeScript, JavaScript, Python, Go, Java, Rust | All files |
| `{{PKG_MANAGER}}` | Package/dependency manager | npm, pnpm, yarn, bun, poetry, pip, go mod, maven, gradle | All files |
| `{{VERSION}}` | Current project version | 1.0.0, 2.5.3, 0.1.0-alpha | PROJECT_ARCHITECTURE |
| `{{LAST_UPDATED}}` | Last update date | 2025-10-11, YYYY-MM-DD | All files |
| `{{STATUS}}` | Project status | Planning, Active Development, Maintenance, Production | PROJECT_ARCHITECTURE |

---

## 🗂️ File & Directory Placeholders

Project structure and file locations.

| Placeholder | Description | Examples | Used In |
|-------------|-------------|----------|---------|
| `{{PROJECT_ROOT}}` | Root directory | ./, /app, /workspace | PROJECT_ARCHITECTURE |
| `{{SOURCE_DIR}}` | Main source code directory | src/, app/, lib/, cmd/ | All files |
| `{{COMPONENTS_DIR}}` | UI components directory | components/, views/, widgets/ | PROJECT_ARCHITECTURE |
| `{{PAGES_DIR}}` | Pages/routes directory | pages/, routes/, screens/ | PROJECT_ARCHITECTURE |
| `{{SERVICES_DIR}}` | Business logic/services | services/, api/, domain/, core/ | All files |
| `{{UTILS_DIR}}` | Utility functions | utils/, helpers/, lib/ | PROJECT_ARCHITECTURE |
| `{{TYPES_DIR}}` | Type definitions | types/, interfaces/, models/ | PROJECT_ARCHITECTURE |
| `{{STORE_DIR}}` | State management | store/, state/, redux/, context/ | PROJECT_ARCHITECTURE |
| `{{TESTS_DIR}}` | Test files | tests/, __tests__, test/, spec/ | All files |
| `{{MIGRATIONS_DIR}}` | Database migrations | migrations/, supabase/migrations/, prisma/migrations/, db/migrations/ | All files |
| `{{DOCS_DIR}}` | Documentation | docs/, documentation/ | All files |
| `{{PUBLIC_DIR}}` | Static assets | public/, static/, assets/ | PROJECT_ARCHITECTURE |
| `{{BUILD_DIR}}` | Build output | dist/, build/, out/, .next/, target/ | PROJECT_ARCHITECTURE |
| `{{CONFIG_DIR}}` | Configuration files | config/, configs/, settings/ | PROJECT_ARCHITECTURE |
| `{{ENTRY_FILE}}` | Main entry point | App.tsx, main.py, main.go, index.ts, server.js | PROJECT_ARCHITECTURE |
| `{{CONFIG_FILE}}` | Main config file | tsconfig.json, pyproject.toml, go.mod, package.json | PROJECT_ARCHITECTURE |

---

## 🎨 Frontend Placeholders

For web/mobile frontend projects.

| Placeholder | Description | Examples | Used In |
|-------------|-------------|----------|---------|
| `{{FRONTEND_FRAMEWORK}}` | Frontend framework | React 18, Vue 3, Svelte, Angular, Next.js 14, Nuxt 3 | PROJECT_ARCHITECTURE |
| `{{BUILD_TOOL}}` | Build/bundler tool | Vite, Webpack, Turbopack, esbuild, Rollup, Parcel | PROJECT_ARCHITECTURE |
| `{{STATE_LIB}}` | State management library | Zustand, Redux, Context API, Pinia, Vuex, MobX, Signals, Jotai | All files |
| `{{UI_FRAMEWORK}}` | UI/CSS framework | Tailwind CSS, MUI, Chakra UI, Bootstrap, Ant Design, shadcn/ui | PROJECT_ARCHITECTURE |
| `{{ICON_LIB}}` | Icon library | Lucide React, Heroicons, Font Awesome, Material Icons, Tabler Icons | PROJECT_ARCHITECTURE |
| `{{ROUTING_LIB}}` | Routing library | React Router, Vue Router, Next.js routing, TanStack Router | PROJECT_ARCHITECTURE |

---

## ⚙️ Backend Placeholders

For backend/server projects.

| Placeholder | Description | Examples | Used In |
|-------------|-------------|----------|---------|
| `{{RUNTIME}}` | Runtime environment | Node.js 20, Python 3.12, Go 1.21, JVM 17, .NET 8, Deno, Bun | All files |
| `{{BACKEND_FRAMEWORK}}` | Backend framework | Express, Fastify, NestJS, FastAPI, Django, Flask, Gin, Fiber, Spring Boot | PROJECT_ARCHITECTURE |
| `{{API_STYLE}}` | API architecture | REST, GraphQL, tRPC, gRPC, WebSocket | PROJECT_ARCHITECTURE |

---

## 🗄️ Database & Storage Placeholders

Database and file storage related.

| Placeholder | Description | Examples | Used In |
|-------------|-------------|----------|---------|
| `{{DB_ENGINE}}` | Database system | PostgreSQL, MySQL, SQLite, MongoDB, Supabase, Firebase, None | All files |
| `{{ORM}}` | ORM/Query builder | Prisma, TypeORM, Drizzle, SQLAlchemy, GORM, Sequelize, Mongoose, Raw SQL | PROJECT_ARCHITECTURE |
| `{{ID_POLICY}}` | Primary key strategy | UUIDv4, UUIDv7, auto-increment, ULID, nanoid, custom | CLAUDE.md, PROJECT_ARCHITECTURE |
| `{{JSON_POLICY}}` | JSON field indexing | JSONB + GIN, JSON, Not used | CLAUDE.md |
| `{{FILES_BACKEND}}` | File storage | AWS S3, OpenAI Files API, Cloudflare R2, Supabase Storage, Local filesystem, None | All files |
| `{{CACHE}}` | Caching system | Redis, Memcached, In-memory, Upstash, None | PROJECT_ARCHITECTURE |
| `{{SCHEMA_CHANGELOG_PATH}}` | Path to database changelog | docs/DATABASE_CHANGELOG.md, supabase/docs/DATABASE_CHANGELOG.md, db/CHANGELOG.md | CLAUDE.md, AGENTS.md |
| `{{TABLE_NAME}}` | Database table name (example) | users, products, orders, posts | CLAUDE.md, DATABASE_CHANGELOG |
| `{{CURRENT_VERSION}}` | DB schema version | v1.0, 2024-10-11, 001 | DATABASE_CHANGELOG |
| `{{TABLE_COUNT}}` | Number of tables | 5, 12, 25 | DATABASE_CHANGELOG |

---

## 🔐 Auth & Security Placeholders

Authentication and security related.

| Placeholder | Description | Examples | Used In |
|-------------|-------------|----------|---------|
| `{{AUTH_PROVIDER}}` | Auth service | Supabase Auth, Auth0, Clerk, NextAuth, Firebase Auth, Keycloak, JWT, Custom | PROJECT_ARCHITECTURE |
| `{{AUTHZ_STRATEGY}}` | Authorization approach | RBAC, ABAC, RLS, Custom policies | PROJECT_ARCHITECTURE |
| `{{SECRETS_MANAGEMENT}}` | Secrets handling | .env.local, Vault, AWS Secrets Manager, Doppler, Environment variables | PROJECT_ARCHITECTURE |

---

## 🔌 External Services Placeholders

Third-party integrations.

| Placeholder | Description | Examples | Used In |
|-------------|-------------|----------|---------|
| `{{APIS}}` | External APIs used | OpenAI, Stripe, Twilio, SendGrid, Google Maps, Anthropic Claude | All files |
| `{{ANALYTICS}}` | Analytics service | Google Analytics, Posthog, Mixpanel, Plausible, None | PROJECT_ARCHITECTURE |
| `{{MONITORING}}` | Monitoring service | Sentry, DataDog, New Relic, Grafana, LogRocket, None | PROJECT_ARCHITECTURE |

---

## 🛠️ DevOps & Deployment Placeholders

Development and deployment related.

| Placeholder | Description | Examples | Used In |
|-------------|-------------|----------|---------|
| `{{VCS}}` | Version control | Git, GitHub, GitLab, Bitbucket | PROJECT_ARCHITECTURE |
| `{{CI}}` | CI/CD system | GitHub Actions, GitLab CI, CircleCI, Jenkins, Travis CI, None | All files |
| `{{DEPLOYMENT}}` | Deployment platform | Vercel, Netlify, AWS, Render, Fly.io, Railway, Docker, Kubernetes, VPS | All files |
| `{{MONOREPO}}` | Is monorepo? | Yes, No | AGENTS.md, PROJECT_ARCHITECTURE |
| `{{PACKAGES}}` | Monorepo packages | @app/web, @app/api, @app/shared | AGENTS.md, PROJECT_ARCHITECTURE |
| `{{TEST_FRAMEWORK}}` | Testing framework | Vitest, Jest, Pytest, Go test, JUnit, Mocha, Cypress, Playwright | PROJECT_ARCHITECTURE |

---

## 📟 Command Placeholders

Command-line operations.

| Placeholder | Description | Examples | Used In |
|-------------|-------------|----------|---------|
| `{{MIGRATE_CMD}}` | Run migrations | npm run migrate, supabase db push, prisma migrate deploy, python manage.py migrate | All files |
| `{{DB_VERIFY_CMD}}` | Verify database | npm run db:verify, psql check, custom script | CLAUDE.md, AGENTS.md |
| `{{REQUIRES_LATIN}}` | Latin-only identifiers | true, false | CLAUDE.md |
| `{{API_HOST_FRAGMENT}}` | API host for debugging | api.example.com, /api/, localhost:3000 | CLAUDE.md |

---

## 🏗️ Architecture Decision Placeholders

For documenting architectural decisions in PROJECT_ARCHITECTURE.md.

| Placeholder | Description | Examples |
|-------------|-------------|----------|
| `{{DECISION_N_TITLE}}` | Decision name | "Database Choice", "State Management Approach" |
| `{{DECISION_N_CHOICE}}` | What was chosen | "PostgreSQL with Supabase", "Zustand for state" |
| `{{DECISION_N_CONTEXT}}` | Why the decision was needed | "Need scalable relational database with real-time features" |
| `{{DECISION_N_DATE}}` | When decided | 2025-10-11 |
| `{{DECISION_N_ALT_1}}` | Alternative option 1 | "MongoDB", "Redux" |
| `{{DECISION_N_ALT_1_REASON}}` | Why rejected | "No relational queries", "Too much boilerplate" |
| `{{DECISION_N_REASON_1}}` | Rationale point 1 | "Built-in auth and real-time", "Simpler API" |
| `{{DECISION_N_CONSEQUENCES}}` | Impact/trade-offs | "Vendor lock-in, but faster development" |

Replace `N` with numbers: `{{DECISION_1_TITLE}}`, `{{DECISION_2_TITLE}}`, etc.

---

## 🔧 Service & Component Placeholders

For documenting code architecture in PROJECT_ARCHITECTURE.md.

| Placeholder | Description | Examples |
|-------------|-------------|----------|
| `{{SERVICE_N_NAME}}` | Service name | "OpenAI Service", "Auth Service", "Payment Service" |
| `{{SERVICE_N_PATH}}` | File path | src/lib/openai.ts, src/services/auth.py |
| `{{SERVICE_N_PURPOSE}}` | What it does | "Handles all OpenAI API interactions" |
| `{{SERVICE_N_METHODS}}` | Key methods code | createAssistant(), sendMessage() |
| `{{SERVICE_N_FEATURE_1}}` | Feature description | "Automatic retry with backoff" |
| `{{COMPONENT_N_NAME}}` | Component name | "FileDropZone", "ChatArea", "UserProfile" |
| `{{COMPONENT_N_PATH}}` | File path | src/components/FileDropZone.tsx |
| `{{COMPONENT_N_PURPOSE}}` | What it does | "Reusable drag & drop file upload" |
| `{{COMPONENT_N_FEATURE_1}}` | Feature description | "Visual hover states" |

Replace `N` with numbers: `{{SERVICE_1_NAME}}`, `{{SERVICE_2_NAME}}`, etc.

---

## 📊 Data Flow Placeholders

For documenting data flows in PROJECT_ARCHITECTURE.md.

| Placeholder | Description | Examples |
|-------------|-------------|----------|
| `{{FLOW_N_NAME}}` | Flow name | "User Login Flow", "File Upload Flow", "Chat Message Flow" |
| `{{FLOW_N_DIAGRAM}}` | ASCII diagram | User → API → DB → Response |
| `{{FLOW_N_STEP_1}}` | Flow step description | "User enters credentials" |

Replace `N` with numbers: `{{FLOW_1_NAME}}`, `{{FLOW_2_NAME}}`, etc.

---

## 📋 Status & Backlog Placeholders

For tracking implementation status in PROJECT_ARCHITECTURE.md.

| Placeholder | Description | Examples |
|-------------|-------------|----------|
| `{{COMPLETED_VERSION}}` | Version of completed items | v1.0, v1.2, v2.0 |
| `{{COMPLETED_N}}` | Completed item | "Basic authentication", "File upload feature" |
| `{{IN_DEV_N}}` | In development item | "Real-time sync", "Payment integration" |
| `{{PLANNED_N}}` | Planned item | "Mobile app", "Advanced search" |
| `{{FUTURE_N}}` | Future consideration | "AI recommendations", "Multi-language support" |

Replace `N` with numbers: `{{COMPLETED_1}}`, `{{IN_DEV_1}}`, etc.

---

## 🎨 Naming & Convention Placeholders

For code style documentation in PROJECT_ARCHITECTURE.md.

| Placeholder | Description | Examples |
|-------------|-------------|----------|
| `{{FILE_NAMING_CONVENTION}}` | File naming style | kebab-case, camelCase, PascalCase, snake_case |
| `{{COMPONENT_STRUCTURE}}` | Component organization | 1 per file, co-located, feature-based |
| `{{IMPORT_ORDER}}` | Import sorting | external → internal → relative, alphabetical |
| `{{CODE_SPLITTING_STRATEGY}}` | Code splitting approach | Route-based, component-based, manual |
| `{{DB_NAMING}}` | Database naming | snake_case, camelCase |
| `{{TIMESTAMP_POLICY}}` | Timestamp fields | created_at + updated_at, timestamps, custom |
| `{{SOFT_DELETE}}` | Soft delete approach | Yes (deleted_at), No, Custom |
| `{{INDEXING_POLICY}}` | Indexing strategy | Foreign keys + search fields, All queries, Selective |

---

## 🛡️ Standards Placeholders

Development practices in PROJECT_ARCHITECTURE.md.

| Placeholder | Description | Examples |
|-------------|-------------|----------|
| `{{ERROR_HANDLING_STRATEGY}}` | Error handling approach | Try/catch with custom errors, Result types, Exceptions |
| `{{LOGGING_STRATEGY}}` | Logging approach | Structured JSON, Console, Winston, Pino, Python logging |
| `{{USER_ERROR_STRATEGY}}` | User-facing errors | Friendly messages, Error codes, Detailed messages |
| `{{ERROR_TYPES}}` | Error type system | Custom error classes, Standard errors, Error codes |
| `{{VALIDATION_STRATEGY}}` | Input validation | Zod, Joi, Yup, class-validator, Manual |
| `{{PERFORMANCE_N}}` | Performance practice | "Lazy loading components", "Database query optimization" |

Replace `N` with numbers: `{{PERFORMANCE_1}}`, `{{PERFORMANCE_2}}`, etc.

---

## 🎯 Quick Reference by File

### CLAUDE.md
Primary: `{{PROJECT_NAME}}`, `{{PKG_MANAGER}}`, `{{SCHEMA_CHANGELOG_PATH}}`, `{{DB_ENGINE}}`, `{{STATE_LIB}}`, `{{FILES_BACKEND}}`, `{{LANGUAGE}}`, `{{MIGRATIONS_DIR}}`, `{{APIS}}`, `{{ID_POLICY}}`, `{{JSON_POLICY}}`, `{{REQUIRES_LATIN}}`, `{{TABLE_NAME}}`, `{{API_HOST_FRAGMENT}}`, `{{MIGRATE_CMD}}`, `{{DB_VERIFY_CMD}}`

### AGENTS.md
Primary: `{{PROJECT_NAME}}`, `{{LANGUAGE}}`, `{{PKG_MANAGER}}`, `{{CI}}`, `{{RUNTIME}}`, `{{DB_ENGINE}}`, `{{MIGRATIONS_DIR}}`, `{{MONOREPO}}`, `{{PACKAGES}}`, `{{MIGRATE_CMD}}`, `{{DB_VERIFY_CMD}}`

### PROJECT_ARCHITECTURE.md
Uses: Most placeholders from all categories above (see each section)

### DATABASE_CHANGELOG.md
Primary: `{{PROJECT_NAME}}`, `{{DB_ENGINE}}`, `{{MIGRATIONS_DIR}}`, `{{CURRENT_VERSION}}`, `{{TABLE_COUNT}}`, `{{TABLE_NAME}}`

---

## 📝 Notes for Adaptation Prompts

When creating adaptation prompts:

1. **Scan project files** to detect technology stack
2. **Ask clarifying questions** for ambiguous choices
3. **Replace placeholders** consistently across all files
4. **Validate** that related placeholders are coherent (e.g., if `{{DB_ENGINE}}` = "None", remove DB sections)
5. **Document decisions** in PROJECT_ARCHITECTURE.md

---

*Keep this file updated when adding new placeholders to template files*  
*Last updated: 2025-10-11*
