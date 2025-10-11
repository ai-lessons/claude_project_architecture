# Universal Files for Claude Code & Codex

This repository contains **project-agnostic** files you can copy into **any** codebase to work effectively with:
- **Codex** (CLI + VS Code extension)
- **Claude Code** (VS Code extension)

**Files:**
- `AGENTS.md` — operational policy for Codex (what to read, how to act, guardrails)
- `CLAUDE.md` — operational policy for Claude Code
- `PROJECT_ARCHITECTURE.md` — human-facing architecture, decisions, backlog
- `.codex/config.toml.sample` — sample user-level config (optional)
- `CONTRIBUTING.md` — optional team conventions
- `prompts/*` — ready prompts to adapt the files to your repo

---

## How to use in a new/existing project

1. **Copy files to the project root:**
   - `AGENTS.md`, `CLAUDE.md`, `PROJECT_ARCHITECTURE.md`, `CONTRIBUTING.md` (optional), `prompts/*`

2. **(Codex) Create a local user config (optional but recommended)**  
   Copy `.codex/config.toml.sample` to your user config location:
   - **Windows:** `C:\Users\<YOU>\.codex\config.toml`
   - **macOS/Linux:** `~/.codex/config.toml`

   > Do **not** include Markdown fences in the TOML; the file must contain only key=value lines.

3. **Open the project in VS Code**

4. **Run Codex in the terminal:**
