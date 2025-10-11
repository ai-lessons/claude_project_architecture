# CONTRIBUTING

## 1) Commits
Use **Conventional Commits**:
- `feat:`, `fix:`, `docs:`, `chore:`, `refactor:`, `test:`, `build:`, `ci:`
- Scope optional: `feat(ui): …`
- Imperative, present tense. Keep messages short; add context in body if needed.

## 2) Pull Requests
- Keep scope **focused**; describe **intent**, **risk**, and **rollback**.
- Link issues/tasks. Provide screenshots/logs for UI/bugfixes when helpful.
- PR title should reflect the main change: `feat: add X`, `fix: handle Y`.

### PR Checklist
- [ ] Type-check + tests + lint pass locally
- [ ] Docs updated (PROJECT_ARCHITECTURE / README / changelog as applicable)
- [ ] Risk & rollback noted (if risky)
- [ ] CI is green

## 3) Code Style
- Follow repo linters/formatters (e.g., ESLint/Prettier, Black/Ruff, gofmt, ktlint).
- Small, cohesive functions; clear module boundaries; no silent errors.
- Use structured logging; **never** log secrets.
- Naming: `camelCase` vars/functions, `PascalCase` types/classes/components, `SCREAMING_SNAKE_CASE` constants.

## 4) Tests
- **Unit** for core logic; **integration** at boundaries (DB/HTTP); **smoke/e2e** where needed.
- Make tests deterministic; avoid flaky external calls (mock/fake).
- Aim for meaningful coverage; prioritize critical paths over raw %.

## 5) Commands (fill for your repo)
- Install: `{{PKG_MANAGER}} install`
- Dev: `{{PKG_MANAGER}} run dev`
- Build: `{{PKG_MANAGER}} run build`
- Start: `{{PKG_MANAGER}} run start`
- Type-check: `{{PKG_MANAGER}} run type-check`
- Lint: `{{PKG_MANAGER}} run lint --fix`
- Tests: `{{PKG_MANAGER}} test` (and `{{PKG_MANAGER}} run test:watch`)

> Update these commands to match your project. Tools like Codex/Claude will use them.

## 6) Database & Migrations (if applicable)
- **All schema changes via migrations** in `{{MIGRATIONS_DIR}}` (no ad-hoc DDL in code).
- Prefer additive, backward-compatible changes; backfill data where needed.
- Verify after migration: `{{DB_VERIFY_CMD}}` (or sanity queries).
- Provide rollback (down migration or documented procedure).

## 7) Security
- Do not commit `.env*` or credentials; use local `.env.local` (git-ignored) and CI secrets.
- Redact secrets in logs and error messages.
- Review third-party deps; pin/lock as appropriate.

## 8) CI/CD
- Pipelines must be green before merge.
- Required checks (adapt): type-check, tests, lint, build, coverage ≥ `{{COVERAGE_TARGET}}%` (if enforced).

## 9) Documentation
- Treat docs as part of the deliverable.
- Update **PROJECT_ARCHITECTURE.md** when architecture or behavior changes.
- Keep **README.md** commands accurate; maintain changelogs if present.

## 10) Tooling Assist (Codex/Claude)
- Tools may propose diffs; **review before applying**.
- Large/refactor changes should include a plan and a verification step.
- Ask for approval before running commands that install/migrate/modify data.

---
