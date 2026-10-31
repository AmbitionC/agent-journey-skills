# Agent Journey Skills

把 [Agent Journey](https://www.agent-journey.cn) 的**前端 / AI 工程学习数据**接进你自己的 Agent：
知识体系、真实面经、实战题卡与验收标准、文章自测题。

AI 在你自己的 Agent 里（Claude Code、Cursor、Cherry Studio……），我们只提供数据和能力。

| Skill | 用途 |
|---|---|
| `tech-knowledge` | 技术问题先查知识库、带出处回答 |
| `interview-prep` | 按公司/岗位检索真实面经，归纳高频题，模拟面试 |
| `project-practice` | 挑实战题卡，按验收标准逐条检查你的实现 |
| `study-coach` | 学习路径规划 + 文章配套自测 |

## 1. 获取 API Key

在 https://www.agent-journey.cn/developer 登录后点「开通」，免费送 100 点体验额度，然后自助创建 Key（格式 `jk_` 开头，只显示一次）。Agent Journey 与 Invest Journey 共用同一个 Key 和点数余额。拿到后：

```bash
export AGENT_JOURNEY_API_KEY=jk_你的key
```

写进 `~/.zshrc` / `~/.bashrc` 以便长期生效。

## 2. 安装

### Claude Code（推荐，MCP + Skills 一起装）

```text
/plugin marketplace add AmbitionC/agent-journey-skills
/plugin install agent-journey@agent-journey
```

重启 Claude Code，`/mcp` 里看到 `agent-journey` 已连接即可。

### 只接 MCP（任何支持远程 MCP 的客户端）

```bash
claude mcp add --transport http agent-journey \
  https://fe-journey-main-ktantdfjcs.cn-hangzhou.fcapp.run/mcp/agent \
  --header "Authorization: Bearer $AGENT_JOURNEY_API_KEY"
```

Cursor / 其他客户端的 `mcp.json`：

```json
{
  "mcpServers": {
    "agent-journey": {
      "url": "https://fe-journey-main-ktantdfjcs.cn-hangzhou.fcapp.run/mcp/agent",
      "headers": { "Authorization": "Bearer jk_你的key" }
    }
  }
}
```

不支持 Skills 的客户端，可以把 `skills/*/SKILL.md` 的正文当作系统提示词使用。

## 3. 试一下

> 用 agent-journey 查一下 React 的 Fiber 是什么，带上出处

> 帮我整理最近字节前端一面的高频题

排查 Key 或网络问题：`./scripts/call.sh tools/list`

## 工具与计量

完整工具清单见 [docs/tools.md](docs/tools.md)。当前版本只读。

## 计费

按调用扣点（1 点约 ¥0.1），调用失败自动退点；`account_usage` 可随时查余额。收费分三个阶段：

1. **公测免费（2026-10-31 ～ 2026-11-30）**：所有工具调用不扣点，无需购买，开通即可用（每日调用上限照常）。
2. **早期用户半价（2026-12-01 起）**：按原价五折，已购会员在有效期内不受后续调价影响。
3. **正式价**：恢复原价，开始日期另行公布。

| 档位 | 半价期 | 原价 | 每月点数 | Key 数 | 每日调用上限 |
|---|---|---|---|---|---|
| 体验 | 免费 | 免费 | 开通送 100 点 | 1 | 200 |
| 会员 | ¥14.5/月，¥119.5/年 | ¥29/月（一天不到一块钱），¥239/年 | 400 | 2 | 1500 |

会员另含 **知识点 PDF 全套下载**（Agent Journey 知识库按目录整理、随更新，在 https://www.agent-journey.cn/services 领取；公测免费期登录即可领）。此前单独购买过 ¥9.9 PDF 的用户下载资格永久保留。

加油包（不过期）：100 点 ¥5（原价 ¥10）· 500 点 ¥22.5（原价 ¥45）· 1100 点 ¥44（原价 ¥88）。

每次调用的点数（收费阶段起）：口径类工具（`indicator_list`、`methodology_get`、`account_usage`）免费；`interview_topics` 每次 3 点；`knowledge_get`、`interview_get`、`market_snapshot`、`fear_series`、`bias_series` 每次 2 点；其余每次 1 点。完整价目以 https://www.agent-journey.cn/developer 为准。

## 许可

Skill 文本与脚本采用 MIT 许可；通过 MCP 获取的内容版权归 Agent Journey 所有，仅供个人学习使用，不得批量抓取再分发。
