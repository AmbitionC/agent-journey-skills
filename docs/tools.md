# 工具清单（v0.1 · 只读）

端点：`https://fe-journey-main-ktantdfjcs.cn-hangzhou.fcapp.run/mcp/agent`（MCP Streamable HTTP）

| 工具 | 参数 | 返回 |
|---|---|---|
| `knowledge_tree` | `module`: knowledge / interview | 目录树（章节 → 文章，叶子带 articleKey） |
| `knowledge_search` | `query`，可选 `module`、`limit`(≤20) | 命中文章：标题、articleKey、正文片段 |
| `knowledge_get` | `module`、`articleKey` | 文章 Markdown 全文（超过 6 万字截断并标 truncated） |
| `interview_search` | 可选 `keyword`、`page`、`pageSize`(≤30) | 面经摘要列表，按时间倒序 |
| `interview_get` | `id` | 面经原文 + 整理后的题目要点 |
| `mission_list` | 可选 `tier`: small / medium / large | 已发布的实战题卡 |
| `mission_get` | `slug` | 题卡背景、需求、约束、验收标准、前置文章 |
| `quiz_get` | `module`、`articleKey` | 文章配套自测题（不含答案） |
| `account_usage` | 无 | 当前 Key 今日调用次数与上限 |

计量：每次 `tools/call` 按工具扣点（价目见 README「计费」节，调用失败自动退点），另有按会员档的每日调用上限（体验 200 / 入门 1000 / Pro 5000，北京时间零点重置）。管理员发放的 Key 不扣点。
`initialize`、`tools/list` 不计次。
