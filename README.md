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

目前为内测，Key 由人工发放（格式 `jk_` 开头）。联系作者获取后：

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

完整工具清单见 [docs/tools.md](docs/tools.md)。当前版本只读、不扣点，每个 Key 每日 2000 次调用上限。

## 许可

Skill 文本与脚本采用 MIT 许可；通过 MCP 获取的内容版权归 Agent Journey 所有，仅供个人学习使用，不得批量抓取再分发。
