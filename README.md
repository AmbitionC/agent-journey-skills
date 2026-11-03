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

## 1. 安装（一句话）

在 Claude Code 里直接说：

> 帮我安装 GitHub 上的 Agent Journey 插件：AmbitionC/agent-journey-skills

或者自己在终端运行：

```bash
claude plugin marketplace add AmbitionC/agent-journey-skills && claude plugin install agent-journey@agent-journey
```

（在 Claude Code 里也可以输入 `/plugin marketplace add AmbitionC/agent-journey-skills`，再输入 `/plugin install agent-journey@agent-journey`。）

> 给 Agent 看的安装说明：运行上面那条终端命令即可，不需要 API Key、不需要设置环境变量；装好后提醒用户重启 Claude Code，第一次使用时按下面第 2 步授权。

## 2. 第一次使用：浏览器授权

**不用建 Key，不用写环境变量。** 重启 Claude Code 后输入 `/mcp`，选中 `agent-journey`（显示「needs authentication」），按提示选 **Authenticate**：
浏览器会打开 Agent Journey，登录后点「授权」，回到 Claude Code 就连上了。新用户授权时自动开通，送 **50 点体验额度**（约够跑通 5~6 次完整场景）。

授权换来的凭证由 Claude Code 自己保存；不想用了，到 https://www.agent-journey.cn/developer 「我的后台」吊销即可。

### 其他客户端

MCP 地址：`https://fe-journey-main-ktantdfjcs.cn-hangzhou.fcapp.run/mcp/agent`（Streamable HTTP）

- **只接 MCP 的 Claude Code**：`claude mcp add --transport http --scope user agent-journey https://fe-journey-main-ktantdfjcs.cn-hangzhou.fcapp.run/mcp/agent`，然后同上 `/mcp` 授权。
- **Cursor**：`~/.cursor/mcp.json` 里加 `{"mcpServers": {"agent-journey": {"url": "https://fe-journey-main-ktantdfjcs.cn-hangzhou.fcapp.run/mcp/agent"}}}`，在 MCP 设置页点登录，浏览器里授权。
- **不支持浏览器授权的客户端（如 Codex）**：到 https://www.agent-journey.cn/developer 登录后创建 Key（`jk_` 开头，只显示一次），请求头带上 `Authorization: Bearer jk_你的key`。Codex 的 `~/.codex/config.toml`：

```toml
[mcp_servers.agent_journey]
url = "https://fe-journey-main-ktantdfjcs.cn-hangzhou.fcapp.run/mcp/agent"
bearer_token_env_var = "AGENT_JOURNEY_API_KEY"
```

不支持 Skills 的客户端，可以把 `skills/*/SKILL.md` 的正文当作系统提示词使用。

## 3. 试一下

> 用 agent-journey 查一下 React 的 Fiber 是什么，带上出处

> 帮我整理最近字节前端一面的高频题

第一次用可以直接问「这个能干嘛」，Agent 会告诉你余额和几个可以直接试的问法（`getting-started` Skill，查余额不扣点）。装好后回到 https://www.agent-journey.cn/developer ，页面顶部的进度条会自动检测你的 Agent 有没有连上。

### 连不上怎么办

| 现象 | 处理 |
|---|---|
| Claude Code 里没有 agent-journey 的工具 | 装完要重启 Claude Code；再输入 `/mcp` 看 `agent-journey` 的状态 |
| `/mcp` 里显示 needs authentication | 选中它按提示选 Authenticate，在打开的页面登录并点「授权」 |
| 授权后又提示需要授权 / 报「Key 已被吊销」 | 在 `/mcp` 里重新授权即可，余额不受影响 |
| 手填 Key 的客户端报「没读到 API Key / Key 不存在」 | 确认请求头是 `Authorization: Bearer jk_…`、Key 复制完整；明文找不到就在后台新建 |

> 0.3.x 及更早版本靠环境变量 `AGENT_JOURNEY_API_KEY` 传 Key；0.4.0 起插件改为浏览器授权，升级后在 `/mcp` 里授权一次即可，原来的 Key 仍可用于手填接入。

不经客户端直接测 Key 和网络（手填 Key 的方式）：`AGENT_JOURNEY_API_KEY=jk_xxx ./scripts/call.sh tools/list`

## 工具与计量

完整工具清单见 [docs/tools.md](docs/tools.md)。当前版本只读。

## 计费

按调用扣点（1 点约 ¥0.1），调用失败自动退点；`account_usage` 可随时查余额。新用户开通（第一次授权即开通）送 **50 点体验额度**，用完后需开通会员或购买加油包才能继续调用（点数不足时工具会返回剩余点数和充值链接）。没有自动续费，不需要绑卡。

**点数与网站 Iris 共用一个余额**：在 https://www.agent-journey.cn 上用 Iris（AI 面试教练）问答、深度思考、模拟面试与复盘报告，扣的是同一份点数；在网站上邀请好友注册得到的点数，也可以用来调用这里的工具。

1. **早期用户半价（2026-11-01 起）**：按原价五折，已购会员在有效期内不受后续调价影响。
2. **正式价**：恢复原价，开始日期另行公布。

| 档位 | 半价期 | 原价 | 每月点数 | Key 数 | 每日调用上限 |
|---|---|---|---|---|---|
| 体验 | — | — | 开通送 50 点（一次性） | 1 | 200 |
| 会员 | ¥14.5/月，¥119.5/年 | ¥29/月（一天不到一块钱），¥239/年 | 400 | 2 | 1500 |

会员是 Agent Journey 网站会员：除每月点数外，还包含面经高频考点完整榜与全部原题、题单 PDF、按公司模拟面试与 Iris 复盘报告（会员专享）、**知识点 PDF 全套下载**（2026-11-30 前登录即可领）等网站权益，全部权益与开通见 https://www.agent-journey.cn/membership 。此前单独购买过 ¥9.9 PDF 的用户下载资格永久保留。加油包只加点数、不含网站权益。

加油包（不过期）：100 点 ¥5（原价 ¥10）· 500 点 ¥22.5（原价 ¥45）· 1100 点 ¥44（原价 ¥88）。

每次调用的点数：`account_usage` 查余额不扣点；`interview_topics` 每次 3 点；`knowledge_get`、`interview_get` 每次 2 点；其余每次 1 点。完整价目以 https://www.agent-journey.cn/developer 为准。

## 许可

Skill 文本与脚本采用 MIT 许可；通过 MCP 获取的内容版权归 Agent Journey 所有，仅供个人学习使用，不得批量抓取再分发。
