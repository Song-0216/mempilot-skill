# 兼容性说明

MemPilot 是纯文本 Skill，兼容性主要取决于 Coding Agent 是否支持：

- 项目文件读取与写入
- 局部文件编辑或精确替换
- Shell / Git 命令（可选但推荐）
- Skill 或项目规则自动发现

## 设计适配

| Agent / 工具 | 项目入口建议 | 状态 |
|---|---|---|
| OpenAI Codex / GPT 编程 Agent | `AGENTS.md` | 设计支持，等待更多真实项目验证 |
| Claude Code | `CLAUDE.md` | 设计支持，等待更多真实项目验证 |
| Cursor | `.cursor/rules/项目记忆.mdc` | 设计支持，等待更多真实项目验证 |
| 其他 Coding Agent | 原生项目规则或 `AGENTS.md` 回退 | 实验性 |

## 已知差异

- 部分工具不支持按行范围读取，可能退化为读取完整短文件
- 部分工具没有可靠 Patch 能力，可能需要精确章节替换
- Agent 对 Skill 自动触发的规则不同
- Git 不可用时，维护基线会写明原因并退化为文件时间和项目结构检查

欢迎通过 Issue 提交你的兼容性测试结果。

## 原生入口示例

Codex、Claude Code 和 Cursor 的最小入口示例见 [`examples/agent-entries`](../examples/agent-entries/README.md)。
