# 精选学习资源

## 必读论文

| 论文 | 核心贡献 | 对应模块 |
|------|---------|--------|
| Chain-of-Thought Prompting Elicits Reasoning (Wei et al., 2022) | 思维链提示的原始论文 | 模块04 |
| Self-Consistency Improves Chain of Thought Reasoning (Wang et al., 2022) | 自洽性采样提升推理准确率 | 模块04 |
| Large Language Models are Zero-Shot Reasoners (Kojima et al., 2022) | "Let's think step by step"的理论基础 | 模块04 |
| Tree of Thoughts (Yao et al., 2023) | 树状推理结构 | 模块04 |
| Lost in the Middle (Liu et al., 2023) | 上下文位置影响模型注意力 | 模块01 |
| ReAct: Synergizing Reasoning and Acting (Yao et al., 2022) | Reasoning + Acting Agent框架 | 模块07 |
| Constitutional AI (Bai et al., 2022) | AI安全与对齐的实践方法 | 模块08 |
| Prompt Injection Attacks (Perez & Ribeiro, 2022) | 提示词注入攻击分析 | 模块08 |

---

## 官方文档与教程

| 资源 | 特点 | 对应模块 |
|------|------|--------|
| Anthropic Prompt Engineering Guide | Claude专属技巧，权威实用 | 全部 |
| OpenAI Prompt Engineering Guide | GPT系列最佳实践 | 全部 |
| Learn Prompting (learnprompting.org) | 系统完整，适合入门到进阶，有中文版 | 全部 |
| Prompt Engineering Guide (dair-ai) | 中文支持好，覆盖最新技术 | 全部 |
| DeepLearning.AI ChatGPT Prompt Engineering | 吴恩达出品，面向开发者，免费 | 模块02-04 |

---

## 测试与开发工具

| 工具 | 用途 |
|------|------|
| Claude.ai | 主力对话测试 |
| OpenAI Playground | 参数可视化调试（temperature/top-p实时调节）|
| Google AI Studio | Gemini系列测试 |
| OpenAI Tokenizer | 可视化分析文本的Token分割 |
| LangSmith | 提示词链追踪与评估 |
| Helicone | API调用监控与分析 |
| PromptLayer | 提示词版本管理 |

---

## 推荐博客与社区

| 资源 | 内容特点 |
|------|---------|
| Anthropic Research Blog | 最新AI安全与技术研究 |
| Lilian Weng's Blog (lilianweng.github.io) | 深度技术解析，质量极高 |
| Simon Willison's Blog (simonwillison.net) | LLM实践经验，更新频繁 |
| r/PromptEngineering | Reddit社区，案例分享 |
| The Prompt Report (2024) | 目前最全面的提示词技术综述论文 |

---

## 配套本课程的阅读顺序

```
第1-2周  → Anthropic官方文档基础部分
第3-4周  → Learn Prompting 结构化章节
第5-6周  → dair-ai Prompt Engineering Guide Few-shot部分
第7-8周  → Wei et al. 2022 CoT原论文（值得精读）
第9-10周 → OpenAI Prompt Engineering Guide
第11周   → ReAct论文 + LangChain Agent文档
第12周   → Constitutional AI + Prompt Injection论文
```

---

*资源持续更新，建议收藏本页面*
