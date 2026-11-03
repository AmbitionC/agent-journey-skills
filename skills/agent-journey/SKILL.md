---
name: agent-journey
description: Agent Journey 数据服务的入口：安装后登录授权、确认连通、介绍能做什么与余额，并提供取数命令（前端 / AI 工程知识库、真实面经与高频考点、实战题卡与验收标准、文章自测题）。用户刚装好、要登录、问「这个能干嘛 / 装好了没 / 还剩多少点」、或其他 Agent Journey Skill 需要取数时使用。
---

# Agent Journey

本 Skill 目录下自带一个零依赖的命令行（Node.js 18 以上）：`scripts/aj.mjs`。下文的 `AJ` 指
`node <本 Skill 所在目录>/scripts/aj.mjs`，运行时换成实际路径。

## 1. 登录（第一次使用必做，只做一次）

```bash
node <本 Skill 目录>/scripts/aj.mjs login
```

- 它会打开浏览器到 Agent Journey 的授权页，并在终端打印同一个链接和确认码。**把链接原样发给用户**（浏览器没自动打开、或你在远程/沙箱环境里时，用户靠它点开）。
- 用户在网页上登录（没有账号可以直接注册），核对确认码后点「授权」。新用户自动开通并送体验点。
- 命令会自己等到授权完成（最多约 100 秒）；输出「授权成功」即完成。若输出「还在等你在浏览器里点授权」并退出，等用户说点好了，再运行一次同样的 `login`（同一个链接 10 分钟内有效，不会换码）。
- 不需要 API Key、不需要环境变量、不需要在客户端里配 MCP 连接。**不要**让用户去网页上复制 Key 粘贴给你。

已经登录过的，`login` 会直接说「已经登录」。查看状态：`AJ status`。

## 2. 取数

两种方式，结果相同：

- 当前会话里有 `agent-journey` 的 MCP 工具（装了插件或配了 MCP）时，直接调用工具。
- 否则用命令行：
  - `AJ tools`：列出全部工具和参数
  - `AJ call <工具名> '<JSON 参数>'`，例如：
    - `AJ call knowledge_search '{"query":"RAG 重排"}'`
    - `AJ call interview_topics '{"keyword":"字节 全栈"}'`
    - `AJ call mission_list`

返回的是 JSON 或 Markdown 文本，自己解析后用人话回答。退出码非 0 表示出错，错误原因在输出里。

## 3. 刚装好时怎么回复用户

目标：让用户一分钟内完成第一次成功提问。**简短**，不要长篇介绍，不要一上来列出全部工具，也不要主动推销会员。

1. 没登录就先按第 1 步登录；登录后运行 `AJ status`（即 `account_usage`，不扣点）。
2. 用两三句话回复：
   - 能做什么：查前端 / AI 工程知识点并带出处、按公司和岗位整理真实面经高频题、领带验收标准的实战题卡并帮你验收、读完文章做自测。
   - 当前余额：照返回的 `points`（或 `onboarding.balance`）说；体验用户说明「调用失败自动退点」。
   - 给 3 个可以直接发的问法让用户挑（返回里有 `onboarding.tryAsking` 时用它）：
     - 讲讲 RAG 里的重排，要有出处。（约 3 点）
     - 给我一道 Agent 记忆模块的实战题，做完帮我验收。（约 2 点）
     - 下周面字节全栈，最近最常考什么？（约 6~8 点）
3. 用户挑了就按对应 Skill 去做：`tech-knowledge`（技术问答）、`interview-prep`（面经与模拟面试）、`project-practice`（实战题卡）、`study-coach`（学习规划与自测）。

## 4. 出错时

按现象判断，**把修法告诉用户，不要反复重试**：

| 现象 / 输出里写着 | 怎么办 |
|---|---|
| 「还没登录」「凭证不可用」「Key 已被吊销」 | 运行 `AJ login`，把打印的链接发给用户，让他登录后点「授权」 |
| 用户在网页上点了取消 / 链接过期 | 重新运行 `AJ login`，会生成新链接 |
| 「连不上」「fetch failed」 | 网络问题；沙箱环境需要放行 `fe-journey-main-ktantdfjcs.cn-hangzhou.fcapp.run` |
| MCP 工具显示 needs authentication（插件 / MCP 方式） | Claude Code 里输入 `/mcp`，选中 `agent-journey` → Authenticate，登录后点「授权」；或者改用上面的命令行登录 |
| Journey 点数不足 | 停止调用，把报错里的余额、充值链接和价格原样告诉用户；充值到账后直接重试，不用重新登录 |
| 今日调用已达上限 | 告诉用户北京时间零点重置 |

工具结果末尾出现「【Journey 提示】」（点数快用完）时，在回答末尾原样转告用户一次，之后不要重复。

不想用了：`AJ logout` 删除本机凭证；到 https://www.agent-journey.cn/developer 可吊销。
