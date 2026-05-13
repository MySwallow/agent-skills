# opencode Tool Mapping

Skills use Claude Code tool names. When you encounter these in a skill, use the opencode equivalent:

| Skill references | opencode equivalent |
|-----------------|----------------------|
| `Read` (file reading) | `read` |
| `Write` (file creation) | `write` |
| `Edit` (file editing) | `edit` |
| `Bash` (run commands) | `bash` |
| `Grep` (search file content) | `grep` |
| `Glob` (search files by name) | `glob` |
| `Task` tool (dispatch subagent) | `task` |
| Multiple `Task` calls (parallel) | Multiple `task` calls |
| `TodoWrite` / `TodoRead` (task tracking) | `todowrite` / `todoread` |
| `Skill` tool (invoke a skill) | `skill` (when enabled); otherwise read the SKILL.md directly |
| `WebFetch` | `webfetch` |
| `WebSearch` | `websearch` |
| `EnterPlanMode` / `ExitPlanMode` | No equivalent — stay in the main session |

## Auto-load

opencode automatically loads one of these files at session start (in priority order):

1. `AGENTS.md` in the project root
2. `~/.config/opencode/AGENTS.md` (global)
3. `CLAUDE.md` in the project root (Claude Code compatibility fallback)
4. `~/.claude/CLAUDE.md` (global fallback)

The simplest integration is to add a pointer to the skills directory in your global `AGENTS.md` — see `platforms/opencode.md`.

## Permission model

opencode uses permission keys to gate tools, matched as wildcard patterns against tool names:

| Permission key | Tools controlled |
|---|---|
| `read` | read operations |
| `edit` | `write`, `edit`, `apply_patch` |
| `bash` | shell commands |
| `glob` | filename matching |
| `grep` | content search |
| `list` | directory listing |
| `task` | subagent dispatch (which subagents can be invoked) |
| `todowrite` | task tracking (also gates `todoread`) |

Wildcards like `"mymcp_*": "deny"` enable fine-grained control.

## Custom agents

opencode's custom agents live in:

- Global: `~/.config/opencode/agents/*.md`
- Per-project: `.opencode/agents/*.md`

The filename becomes the agent name (`review.md` → `review` agent). You can wrap individual skills as opencode agents and invoke them via the `task` tool.
