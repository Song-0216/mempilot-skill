# 评测建议

MemPilot 当前不宣称固定的 Token 节省比例。推荐用以下方式进行可复现对照：

## 场景

1. 初始化项目记忆
2. 单模块功能开发
3. 跨模块开发
4. Bug 修复与经验写入
5. 版本发布与深度维护

## 对照组

- 不使用任何项目记忆
- 使用传统全文件 Memory Bank
- 使用 MemPilot

## 指标

- 输入 Token
- 输出 Token
- 读取文件数量
- 读取章节数量
- Top 1 模块命中率
- 无关模块读取率
- 整文件重写次数
- 重复解释次数
- 30 次会话后的记忆总长度
- 代码与记忆不一致数量

请在公开结果中记录模型、Agent、项目类型、任务和测量方法。

## 仓库内最小用例

- [`evals/trigger-cases.md`](../evals/trigger-cases.md)
- [`evals/routing-cases.md`](../evals/routing-cases.md)
- [`evals/maintenance-cases.md`](../evals/maintenance-cases.md)
