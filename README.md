# Prompt Lab 🧪

> 从基础原理到高级思维链策略的提示词设计系统教程与案例研究

## 📚 关于本仓库

提示词工程（Prompt Engineering）是与大语言模型（LLM）高效协作的核心技能。本仓库提供一套系统化学习路径，目标是 **3个月内** 让你能够独立设计并优化复杂任务的提示词。

---

## 🗺️ 八大核心知识模块

| # | 模块名称 | 难度 | 学习周期 | 核心应用场景 |
|---|---------|------|---------|------------|
| [01](./modules/01-fundamentals/) | 基础原理与核心概念 | ⭐ 入门 | 第1-2周 | 建立认知框架，理解模型工作机制 |
| [02](./modules/02-basic-structure/) | 提示词基础结构设计 | ⭐⭐ 初级 | 第3-4周 | 日常任务、内容生成、格式精确控制 |
| [03](./modules/03-few-shot-learning/) | Few-shot 与示例驱动学习 | ⭐⭐ 初级 | 第5-6周 | 文本分类、数据提取、风格转换 |
| [04](./modules/04-chain-of-thought/) | 思维链与复杂推理 | ⭐⭐⭐ 中级 | 第7-8周 | 数学推理、逻辑分析、多步决策 |
| [05](./modules/05-role-persona/) | 角色设计与人格注入 | ⭐⭐⭐ 中级 | 第9-10周 | 专家顾问、客服机器人、教育辅导 |
| [06](./modules/06-optimization/) | 提示词系统性优化 | ⭐⭐⭐⭐ 中高级 | 第10-11周 | 生产环境调优、A/B测试、质量评估 |
| [07](./modules/07-advanced-techniques/) | 高级技术：RAG / Agent / 工具调用 | ⭐⭐⭐⭐⭐ 高级 | 第11-12周 | 知识库问答、自动化工作流、多步 Agent |
| [08](./modules/08-safety-alignment/) | 安全、对齐与生产部署 | ⭐⭐⭐⭐ 高级 | 第12周 | 防提示注入、企业合规、安全部署 |

---

## 📂 仓库结构

```
prompt-lab/
├── README.md                      # 总览与模块导航（本文件）
├── ROADMAP.md                     # 3个月详细学习计划
├── resources.md                   # 精选外部学习资源
├── modules/                       # 8大核心知识模块
│   ├── 01-fundamentals/           # ⭐ 基础原理
│   │   ├── README.md              # 模块教程
│   │   ├── examples.md            # 实践示例
│   │   └── exercises.md           # 练习题与参考答案
│   ├── 02-basic-structure/        # ⭐⭐ 结构设计
│   ├── 03-few-shot-learning/      # ⭐⭐ 示例学习
│   ├── 04-chain-of-thought/       # ⭐⭐⭐ 思维链
│   ├── 05-role-persona/           # ⭐⭐⭐ 角色设计
│   ├── 06-optimization/           # ⭐⭐⭐⭐ 优化方法
│   ├── 07-advanced-techniques/    # ⭐⭐⭐⭐⭐ 高级技术
│   └── 08-safety-alignment/       # ⭐⭐⭐⭐ 安全对齐
├── case-studies/                  # 5个真实场景案例研究
│   ├── README.md
│   ├── case-01-content-generation.md
│   ├── case-02-data-extraction.md
│   ├── case-03-code-assistant.md
│   ├── case-04-customer-service.md
│   └── case-05-complex-reasoning.md
└── templates/                     # 可复用提示词模板库
    ├── README.md
    ├── basic-template.md
    ├── cot-template.md
    ├── role-template.md
    └── rag-template.md
```

---

## 🚀 快速开始

**第一次来？** 按以下顺序：

1. 阅读 [ROADMAP.md](./ROADMAP.md) 了解完整3个月计划
2. 从 [模块01](./modules/01-fundamentals/) 开始，按顺序学习
3. 完成每个模块的 `exercises.md` 巩固理解
4. 参考 [templates/](./templates/) 快速应用到实际任务
5. 通过 [case-studies/](./case-studies/) 学习完整设计过程

---

## 📈 完成后你将能够

- ✅ 理解 LLM 核心工作原理，知道"为什么"而非只知道"怎么做"
- ✅ 用结构化方法设计可维护、可复用的提示词系统
- ✅ 运用 Few-shot、CoT 等技术解决复杂推理任务
- ✅ 构建具有稳定人格的 AI 角色和智能助手
- ✅ 建立科学的提示词评估和迭代体系
- ✅ 为 RAG 系统和 AI Agent 设计高效提示词
- ✅ 识别并防范提示词注入等安全风险

---

*最后更新：2026-04 | 基于 Claude Sonnet 4.6 实践验证*
