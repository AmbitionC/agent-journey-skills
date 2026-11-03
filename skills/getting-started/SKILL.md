---
name: getting-started
description: Agent Journey 刚装好、第一次使用，或用户问「这个能干嘛 / 怎么用 / 装好了没 / 还剩多少点」时使用：确认连通、简短介绍能力与余额、给出可以直接试的问法；工具不可用、需要授权或调用报 Key 相关错误时带用户排查。
---

# 第一次使用 Agent Journey

目标：让用户在一分钟内完成第一次成功提问。**简短**，不要长篇介绍。

## 步骤

1. 调 `account_usage`（不扣点）。成功即说明已经连通。
2. 用两三句话回复用户：
   - 能做什么：查前端 / AI 工程知识点并带出处、按公司和岗位整理真实面经高频题、领带验收标准的实战题卡并帮你验收、读完文章做自测。
   - 当前余额：照 `account_usage` 返回的 `points`（或 `onboarding.balance`）说；体验用户说明「调用失败自动退点」。
   - 给 3 个可以直接发的问法，让用户挑一个（返回里有 `onboarding.tryAsking` 时用它，没有就用下面的）：
   - 讲讲 RAG 里的重排，要有出处。（约 3 点）
   - 给我一道 Agent 记忆模块的实战题，做完帮我验收。（约 2 点）
   - 下周面字节全栈，最近最常考什么？（约 6~8 点）
3. 用户挑了就直接按对应 Skill 去做：`tech-knowledge`（技术问答）、`interview-prep`（面经与模拟面试）、`project-practice`（实战题卡）、`study-coach`（学习规划与自测）。

不要一上来就列出全部工具，也不要主动推销会员。

## 工具不可用 / 调用报错时

按现象判断，**把修法告诉用户，不要反复重试**：

| 现象 / 报错里写着 | 让用户做 |
|---|---|
| 工具列表里根本没有 `agent-journey` 的工具 | 装完插件要重启 Claude Code；然后输入 `/mcp` 看 `agent-journey` 的状态 |
| `/mcp` 里显示 needs authentication，或报「缺少 API Key，还没授权」 | 输入 `/mcp`，选中 `agent-journey`，选 Authenticate；浏览器会打开 Agent Journey，登录后点「授权」，回到这里即可（不需要建 Key、不需要环境变量，新用户自动送体验点） |
| Key 已被吊销 | 浏览器授权接入的：在 `/mcp` 里重新授权；手填 Key 的：到 https://www.agent-journey.cn/developer 新建一个替换，余额不受影响 |
| 没读到 API Key / 环境变量没有生效 / Key 格式不对 / Key 不存在（手填 Key 的客户端才会遇到） | 建议改用浏览器授权；坚持手填的，核对请求头 `Authorization: Bearer jk_…`、Key 复制完整，改完重启客户端 |
| Journey 点数不足 | 停止调用，把报错里的余额、充值链接和价格原样告诉用户；充值到账后直接重试，不用重新授权 |
| 今日调用已达上限 | 告诉用户北京时间零点重置 |

## 点数提醒

工具结果末尾出现「【Journey 提示】」时，在回答末尾原样转告用户一次，之后不要重复。
