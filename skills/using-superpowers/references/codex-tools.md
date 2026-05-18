# Codex 工具映射

Skills 使用 Claude Code 的工具名。在 skill 中遇到这些时，请使用你平台的等价物：

| Skill 引用 | Codex 等价物 |
|-----------------|------------------|
| `Task` 工具（调度子代理） | `spawn_agent`（见[子代理调度需要多代理支持](#subagent-dispatch-requires-multi-agent-support)） |
| 多次 `Task` 调用（并行） | 多次 `spawn_agent` 调用 |
| Task 返回结果 | `wait_agent` |
| Task 自动完成 | `close_agent` 以释放 slot |
| `TodoWrite`（任务追踪） | `update_plan` |
| `Skill` 工具（调用一个 skill） | Skills 原生加载——直接遵循指令即可 |
| `Read`、`Write`、`Edit`（文件） | 使用你的原生文件工具 |
| `Bash`（运行命令） | 使用你的原生 shell 工具 |

## 子代理调度需要多代理支持

在 Codex 配置（`~/.codex/config.toml`）中添加：

```toml
[features]
multi_agent = true
```

这会启用 `spawn_agent`、`wait_agent` 和 `close_agent`，供 `dispatching-parallel-agents` 和 `subagent-driven-development` 等 skill 使用。

历史注：`rust-v0.115.0` 之前的 Codex 构建将"等待已派生代理"暴露为 `wait`。当前的 Codex 使用 `wait_agent` 等待已派生代理。`wait` 这个名字现在归属 code-mode 的 `exec/wait`——按 `cell_id` 恢复一个已 yield 的 exec cell；它不是已派生代理的结果工具。

## 工作目录与分支

superpowers-lite 不依赖 git worktree——所有 skill 直接在当前分支工作。implementer 只 `git add` 暂存变更，**不自动 commit / push / 开 PR**，由用户审阅后自行处理。

如果你在 Codex 沙箱里发现 git 写操作（branch / push / PR）受限，也不需要绕开——把变更暂存好，告诉用户在自己本机操作即可。
