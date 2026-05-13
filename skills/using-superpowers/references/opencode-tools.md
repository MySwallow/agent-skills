# opencode 工具映射

Skills 使用 Claude Code 的工具名。在 skill 中遇到这些时，请使用 opencode 的等价物：

| Skill 引用 | opencode 等价物 |
|-----------------|------------------|
| `Read`（读取文件） | `read` |
| `Write`（创建文件） | `write` |
| `Edit`（编辑文件） | `edit` |
| `Bash`（运行命令） | `bash` |
| `Grep`（按内容搜索） | `grep` |
| `Glob`（按文件名搜索） | `glob` |
| `Task` 工具（调度子代理） | `task` |
| 多次 `Task` 调用（并行） | 多次 `task` 调用 |
| `TodoWrite` / `TodoRead`（任务追踪） | `todowrite` / `todoread` |
| `Skill` 工具（调用一个 skill） | `skill`（如已启用），否则直接读取 SKILL.md |
| `WebFetch` | `webfetch` |
| `WebSearch` | `websearch` |
| `EnterPlanMode` / `ExitPlanMode` | 无等价物——保持在主会话 |

## 自动加载

opencode 在会话启动时会自动加载以下文件之一（按优先级）：

1. 项目根的 `AGENTS.md`
2. `~/.config/opencode/AGENTS.md`（全局）
3. 项目根的 `CLAUDE.md`（Claude Code 兼容回退）
4. `~/.claude/CLAUDE.md`（全局回退）

最简单的接入方式：在全局 `AGENTS.md` 中加一段指向 skills 目录的引用，详见 `platforms/opencode.md`。

## 权限模型

opencode 用权限键控制工具访问，键以通配符匹配工具名：

| 权限键 | 控制的工具 |
|---|---|
| `read` | 读操作 |
| `edit` | `write`、`edit`、`apply_patch` |
| `bash` | shell 命令 |
| `glob` | 文件名匹配 |
| `grep` | 内容搜索 |
| `list` | 目录列表 |
| `task` | 子代理调度（限制可调用哪些子代理） |
| `todowrite` | 任务追踪（同时控制 `todoread`） |

可以用 `"mymcp_*": "deny"` 这样的通配符做细粒度控制。

## 自定义代理

opencode 的自定义代理（custom agent）放在：

- 全局：`~/.config/opencode/agents/*.md`
- 项目：`.opencode/agents/*.md`

文件名即代理名（`review.md` → `review` 代理）。可以把单个 skill 包装成一个 opencode 代理，然后用 `task` 工具调起。
