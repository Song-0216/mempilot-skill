# Agent 原生入口示例

MemPilot 只为当前正在使用的 Coding Agent 生成极短入口。入口负责指向项目记忆，不复制完整 Skill。

- `AGENTS.md`：Codex / GPT 编程 Agent
- `CLAUDE.md`：Claude Code
- `.cursor/rules/项目记忆.mdc`：Cursor

这些文件只是最小示例。实际初始化时，MemPilot 必须保留项目已有的工具专属规则，并在合适位置合并项目记忆入口。
