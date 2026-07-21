# MemPilot

> 中文优先、Markdown 原生、低 Token 的 Coding Agent 项目记忆 Skill。

**项目状态：`v0.1.2-alpha`**

MemPilot 面向个人开发者和 1～3 人小团队的中型长期 Vibe Coding 项目。它让 AI 根据真实代码结构创建中文项目记忆，并通过模块语义路标、章节级读取、局部 Patch 和定期维护，减少跨会话失忆、重复解释和上下文浪费。

MemPilot 是一个纯 Skill：不需要数据库、后台服务、向量检索或常驻进程。

## 它解决什么问题

长期使用 Coding Agent 时，常见问题包括：

- 新会话忘记项目当前进度和既有决策
- 为了找一个模块，先读取大量无关文档
- 更新一行状态，却重写整份记忆文件
- Bug 经验没有沉淀，同类问题反复排查
- 项目结构改变后，旧记忆逐渐失真
- 记忆越写越长，反过来污染上下文

MemPilot 的目标不是“保存更多”，而是：

> 只读取当前任务需要的最少记忆，只写入未来仍有价值的最小变化。

## 核心特性

- **中文优先**：目录、模块、决策、调试记录和报告使用中文
- **项目自适应**：根据真实业务边界生成模块，不套固定模板
- **Top 1 语义路由**：通过触发关键词优先命中一个模块
- **章节级读取**：按 `##` 标题读取目标章节，不默认全文加载
- **增量写入**：优先 Patch、Search/Replace 或精确章节替换
- **三问写入法**：只记录状态变化、长期认知和可复用难题
- **Git 驱动维护**：根据差异增量更新，不重复扫描整个项目
- **主动维护**：达到阈值时说明证据并询问是否立即快速维护
- **定期治理**：支持快速维护、深度整理、压缩、路标重建和健康报告
- **非 Git 兼容**：没有 Git 时使用会话文件记录与定向检查降级
- **腐烂抽查**：检查代码路径、关键标识，并定向验证少量高影响语义陈述
- **提醒抑制**：同一维护信号默认 7 天内不重复打扰，基线或严重度变化时再提醒
- **能力降级**：弱模型或低置信场景只创建高置信模块，禁止用空洞内容补齐
- **历史默认休眠**：版本记录和归档不会进入日常上下文
- **零基础设施**：Markdown 是唯一事实源，无额外服务依赖

## 30 秒开始

1. 将整个 MemPilot Skill 目录放入你的 Coding Agent 可读取的 Skills 位置。
2. 在项目中说：

```text
帮我建记忆
```

3. MemPilot 会轻量分析项目，生成类似结构：

```text
项目记忆/
├── 当前状态.md
├── 项目索引.md
├── 调试记忆.md
├── 接口契约.md        # 仅需要时创建
├── 模块/
│   ├── 用户管理.md
│   ├── 产品管理.md
│   └── 认证与权限.md
├── 决策/
├── 版本记录/
└── 归档/
```

4. 日常开发结束时说：

```text
记一下
```

## 在不同 Agent 中使用

请复制或提供**完整的 MemPilot Skill 目录**，不要只复制 `SKILL.md`，因为主文件会按需读取 `references/` 和 `assets/`。

### Codex / GPT 编程 Agent

把完整目录放入当前环境支持的 Skills 位置，然后在项目中说：

```text
帮我建记忆
```

初始化后，MemPilot 会为项目生成一个极短的 `AGENTS.md` 入口。

### Claude Code

把完整目录放入 Claude Code 可读取的 Skill 位置。若当前环境不能自动发现 Skill，可以让 Claude 直接读取本仓库的 `SKILL.md`，再执行：

```text
帮我建记忆
```

初始化后，MemPilot 会生成或更新极短的 `CLAUDE.md` 入口，并保留项目原有的 Claude 专属规则。

### Cursor

把完整目录作为项目 Skill 或上下文提供给 Cursor，然后说：

```text
帮我建记忆
```

初始化后，MemPilot 会优先创建 `.cursor/rules/项目记忆.mdc`。

不同版本和客户端的 Skill 路径可能变化，请以所用工具的当前文档为准。三种入口的最小示例见 [`examples/agent-entries`](examples/agent-entries/README.md)。

## 口语命令

| 你可以直接说 | MemPilot 模式 |
|---|---|
| “帮我建记忆” | 初始化 |
| “记一下” / “保存进度” | 日常增量 |
| “检查一下” / “看看记忆” | 快速维护 |
| “大扫除” / “整理归档” | 深度维护 |
| “它又搞错模块了” | 重建语义路标 |
| “太费钱了” / “瘦身” | 压缩记忆 |
| “生成版本记录” | 里程碑整理 |
| “检查记忆和代码是否一致” | 一致性检查 |

## Skill 结构

```text
mempilot-skill/
├── SKILL.md
├── references/
│   ├── 初始化.md
│   ├── 日常增量.md
│   ├── 快速维护.md
│   ├── 深度维护.md
│   ├── 一致性与路标.md
│   ├── 结构演化.md
│   ├── 版本与压缩.md
│   └── Agent入口.md
├── assets/
│   ├── 当前状态模板.md
│   ├── 项目索引模板.md
│   ├── 模块模板.md
│   ├── ADR模板.md
│   ├── 调试记忆模板.md
│   ├── 接口契约模板.md
│   └── 维护报告模板.md
├── examples/
├── docs/
└── .github/
```

主 `SKILL.md` 只负责模式路由与硬规则。进入具体模式后，只加载一个对应的 `references/*.md`，减少固定上下文占用。

## 示例

查看 [`examples/vue-admin-demo`](examples/vue-admin-demo/README.md)，可以看到一个 Vue 管理系统在初始化前后的目录和记忆文件示例。

## Agent 兼容性

MemPilot 的设计目标包括：

- OpenAI Codex / GPT 编程 Agent
- Claude Code
- Cursor
- 其他支持 Skill 或项目规则文件的 Coding Agent

不同工具和模型对 Skill 自动发现、代码理解、局部编辑和规则遵循能力不同。推荐使用具备较强代码理解、检索和工具调用能力的模型；中等或轻量模型会进入更保守的低置信模式。详细分级见 [`docs/compatibility.md`](docs/compatibility.md)。当前版本属于 Alpha，欢迎提交真实兼容性测试结果。

MemPilot 会根据当前工具生成极短的原生项目入口，例如：

- Codex / GPT 编程 Agent：`AGENTS.md`
- Claude Code：`CLAUDE.md`
- Cursor：`.cursor/rules/项目记忆.mdc`

## 与传统 Memory Bank 的区别

| 维度 | 常见 Memory Bank | MemPilot |
|---|---|---|
| 模块结构 | 固定文件模板 | 根据真实项目自动生成中文模块 |
| 读取策略 | 经常读取多个完整文件 | Top 1 路由 + 章节级读取 |
| 写入策略 | 常见整文件覆盖 | 局部 Patch + 写入预算 |
| 历史管理 | 容易持续堆积 | 版本记录与归档默认休眠 |
| 维护方式 | 主要依靠日常手工更新 | 快速维护、深度维护、压缩和健康报告 |
| 基础设施 | 部分依赖数据库或服务 | 纯 Markdown，无后台服务 |
| 目标用户 | 通用或团队平台 | 中文个人开发者与小团队长期项目 |

## 最小评测与回归检查

仓库提供了三组人工可执行的最小用例：

- [`evals/trigger-cases.md`](evals/trigger-cases.md)：Skill 是否在正确的用户表达下触发
- [`evals/routing-cases.md`](evals/routing-cases.md)：是否命中正确模块并避免读取无关模块
- [`evals/maintenance-cases.md`](evals/maintenance-cases.md)：是否采用局部写入、维护预算和安全确认

这些用例不是自动化基准，但能帮助不同 Agent 使用同一套场景进行回归测试。完整评测建议见 [`docs/evaluation.md`](docs/evaluation.md)。

## 隐私与安全

MemPilot 明确禁止把以下内容写入项目记忆：

- 密码、API Key、Token
- 数据库连接串
- PEM 私钥
- 用户隐私数据
- 未经验证的猜测
- 完整聊天记录与模型思考过程

使用前仍建议检查 Agent 的文件权限和项目仓库内容。详见 [`SECURITY.md`](SECURITY.md)。

## 当前限制

- MemPilot 主要依靠 Agent 遵循 Skill 规则，不是确定性程序
- 语义漂移仅做定向抽查，不等同于完整静态分析或形式化验证
- 模块识别质量取决于项目结构和模型能力
- 各 Agent 对局部读取、Patch 和 Skill 发现的支持不完全一致
- 当前尚无大规模公开 Token 基准和长期项目统计
- Alpha 阶段可能调整目录、触发语和模板

## 路线图

- [ ] 增加更多真实项目示例
- [ ] 建立跨 Agent 兼容性测试矩阵
- [ ] 发布模块路由与 Token 对照评测
- [ ] 收集连续 30+ 会话的长期使用数据
- [ ] 提供英文文档和社区翻译
- [ ] 优化 Skill 触发准确率

## 贡献

欢迎提交：

- 不同 Agent 的测试结果
- 模块路由失败案例
- Token 使用前后对比
- 长期项目的记忆膨胀案例
- 文档、模板和兼容性改进

提交前请阅读 [`CONTRIBUTING.md`](CONTRIBUTING.md)。

## 许可证

MemPilot 使用 [MIT License](LICENSE)。
