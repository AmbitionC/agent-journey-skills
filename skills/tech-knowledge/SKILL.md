---
name: tech-knowledge
description: 回答前端、浏览器、JavaScript、React、工程化、AI 应用开发等技术问题时，先从 Agent Journey 知识库检索并引用原文。用户问技术概念、原理、对比、最佳实践，或让你讲解某个知识点时使用。
---

# 技术知识问答（Agent Journey 知识库）

用 `agent-journey` MCP 工具给出**有出处**的回答，而不是凭记忆泛泛而谈。

## 步骤

1. `knowledge_search`：用用户的问题或 2~4 个关键词检索（中文关键词效果更好）。
   - 结果为空时换同义词再试一次（如「事件循环」↔「Event Loop」）。
2. 挑 1~3 篇最相关的，用 `knowledge_get(module, articleKey)` 读全文。
3. 基于原文回答：
   - 先给一句话结论，再展开原理；代码示例优先用原文里的。
   - 原文没覆盖的部分可以补充，但要说明「以下为补充，非原文内容」。
4. 末尾列「延伸阅读」：文章标题 + module/articleKey，告诉用户可在 agent-journey.cn 阅读。

## 想系统学一个方向时

用 `knowledge_tree(module="knowledge")` 拿完整目录，按章节顺序给出学习路径，
每章挑 1~2 篇关键文章，不要一次性罗列全部。

## 注意

- 不要编造检索结果里没有的文章标题。
- 工具返回「Key 无效」时，提示用户按插件 README 配置 `AGENT_JOURNEY_API_KEY`。
