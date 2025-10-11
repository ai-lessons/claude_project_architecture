# Universal Files for Claude Code & Codex

This repository contains **project-agnostic** files you can copy into **any** codebase to work effectively with:
- **Codex** (CLI + VS Code extension)
- **Claude Code** (VS Code extension)

**Files:**
- `AGENTS.md` — operational policy for Codex (what to read, how to act, guardrails)
- `CLAUDE.md` — operational policy for Claude Code
- `PROJECT_ARCHITECTURE.md` — human-facing architecture, decisions, backlog
- `config.toml.sample` — sample user-level config (optional)
- `CONTRIBUTING.md` — optional team conventions
- `prompts/*` — ready prompts to adapt the files to your repo
- `.gitignore` — список файлов и папок, которые не должны попадать в репозиторий Git (кэш, артефакты сборки, секреты, локальные настройки)


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
Then copy-paste the prompt from `prompts/codex_adapt.txt` to auto-fill placeholders in `AGENTS.md` and `PROJECT_ARCHITECTURE.md`. Approve the diffs.

5. **Open Claude Code panel** and paste the prompt from `prompts/claude_adapt.txt`. It will adapt `CLAUDE.md` (and can cross-check `AGENTS.md`/`PROJECT_ARCHITECTURE.md`).

6. **Commit the updated files** once you’re happy.

---

## Troubleshooting

- **Codex not found:** install the CLI and ensure it’s on PATH.  
- **TOML parse error:** remove Markdown code fences from `~/.codex/config.toml`.  
- **Repo is unusual:** let the tools scan and propose a minimal structure; refine.

Happy building!
