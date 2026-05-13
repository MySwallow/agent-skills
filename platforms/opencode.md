# Install on opencode

Status: 🔬 Compatible — not extensively tested. PRs welcome.

## How skills work in opencode

opencode auto-loads instructions from `AGENTS.md` at session start (project root or `~/.config/opencode/AGENTS.md`). It also falls back to `CLAUDE.md` for Claude Code compatibility, so if you already have skills installed at `~/.claude/skills/`, opencode can be pointed at them from a single line in `AGENTS.md`.

Tool naming is close to Claude Code's: `read`, `write`, `edit`, `bash`, `glob`, `grep`, `task`, `todowrite`, `webfetch`, `websearch`. See `skills/using-superpowers/references/opencode-tools.md` for the full mapping.

## Install (recommended: reference via AGENTS.md)

1. Clone this repo somewhere stable (e.g. `~/dev/superpowers-lite`).
2. Create or edit `~/.config/opencode/AGENTS.md` and add:

   ```markdown
   # Skills

   When the user asks about brainstorming, planning, debugging, or implementing
   features, follow the methodology in the SKILL.md files under
   `~/dev/superpowers-lite/skills/` (or `skills-en/` for English).

   Always start by reading `using-superpowers/SKILL.md` — it explains how to
   find and apply the other skills.

   Tool-name mapping: see `using-superpowers/references/opencode-tools.md`.
   ```

3. Restart opencode (or start a new session).

## Install (alternative: per-project)

Commit an `AGENTS.md` to your project root with the same content, scoped to that project.

## Install (alternative: custom agents)

opencode supports custom agents in `~/.config/opencode/agents/` (global) or `.opencode/agents/` (per-project), where each markdown file becomes a named agent. You can wrap individual skills as agents:

```bash
mkdir -p ~/.config/opencode/agents
cp skills/systematic-debugging/SKILL.md ~/.config/opencode/agents/debug.md
cp skills/writing-plans/SKILL.md        ~/.config/opencode/agents/plan.md
# ... etc
```

The filename becomes the agent name (`debug`, `plan`, etc.).

## Tool-name mapping

opencode's tool names closely mirror Claude Code's. The complete mapping is in `skills/using-superpowers/references/opencode-tools.md`. Notable equivalents:

- `Task` → `task`
- `TodoWrite` → `todowrite`
- `WebFetch` → `webfetch`
- `Read` / `Write` / `Edit` / `Bash` / `Glob` / `Grep` — same names (lowercase)

## Verify

Start an opencode session and trigger a skill condition (e.g., "let's debug this test failure" or "plan this feature"). opencode should follow the methodology from the matching SKILL.md.
