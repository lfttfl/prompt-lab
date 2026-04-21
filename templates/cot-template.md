# 思维链模板（Chain-of-Thought）

> 适用场景：复杂推理、多步分析、逻辑判断、数学计算
> 核心技术：Standard CoT + Zero-shot CoT + Self-consistency

---

## 模板1：Zero-shot CoT（最简版）

```
{任务描述}

{user_input}

请一步一步思考，列出每个推理步骤，然后给出最终答案。
```

**适用**：一次性分析任务，快速提升推理准确率

---

## 模板2：Standard CoT（带示例版）

```
{任务描述}

---示例---
输入：{示例输入}
推理过程：
步骤1：{第一步分析}
步骤2：{第二步分析}
步骤3：{第三步分析（根据需要增减）}
结论：{最终答案}
---示例结束---

现在请分析：
输入：{user_input}
推理过程：
```

**适用**：需要稳定推理格式的重复性任务

---

## 模板3：结构化推理报告（完整版）

```
你是{专业角色}，需要对以下问题进行深度分析。

分析框架（按顺序执行，每步都要输出）：

【第一步：问题理解】
- 核心问题是什么？
- 涉及哪些关键变量或因素？
- 有哪些已知信息，哪些信息缺失？

【第二步：逐因素分析】
对每个关键因素：
- 当前状态是什么？
- 如何影响最终结论？
- 证据支持程度（强/中/弱）？

【第三步：综合判断】
- 综合以上分析，最可能的结论是什么？
- 主要不确定性在哪里？
- 结论的置信度（高/中/低）？

【第四步：最终建议】
- 明确的行动建议（如果适用）
- 需要进一步调查的关键问题

---
待分析的问题/情况：
{user_input}
```

---

## 模板4：对比分析 CoT

```
对以下{X个}选项进行系统性比较分析，帮助做出决策。

评估维度（按重要性排序）：
1. {维度1}（权重：{X}%）
2. {维度2}（权重：{X}%）
3. {维度3}（权重：{X}%）

分析步骤：
第一步：逐一评估每个选项在每个维度上的表现（1-5分+说明）
第二步：计算加权总分
第三步：考虑定性因素（难以量化的优劣势）
第四步：给出推荐意见和理由

输出格式：
| 评估维度 | 选项A | 选项B | 选项C |
|---------|------|------|------|
...加权总分表...
推荐结论：[X选项]
核心理由：...

待比较的选项：
{options_and_descriptions}
```

---

## 模板5：Self-consistency 实现

```python
# 概念性实现（需要根据你的API进行调整）

import anthropic
from collections import Counter

def self_consistent_analysis(question: str, n_runs: int = 5) -> str:
    """
    对同一问题运行多次，取多数投票结果
    适用于有明确答案的推理任务
    """
    client = anthropic.Anthropic()
    answers = []
    
    prompt = f"""
{question}

请一步一步推理，在最后一行用"最终答案："格式给出结论。
    """
    
    for i in range(n_runs):
        response = client.messages.create(
            model="claude-sonnet-4-6",
            max_tokens=1024,
            messages=[{"role": "user", "content": prompt}],
            temperature=0.7  # 适当随机性以获得多样推理路径
        )
        
        text = response.content[0].text
        # 提取最终答案
        if "最终答案：" in text:
            answer = text.split("最终答案：")[-1].strip().split("\n")[0]
            answers.append(answer)
    
    # 多数投票
    if answers:
        most_common = Counter(answers).most_common(1)[0]
        return f"最终答案（{n_runs}次投票，{most_common[1]}票）：{most_common[0]}"
    return "无法确定答案"
```

---

## 选择指南

| 场景 | 推荐模板 | 原因 |
|------|---------|------|
| 一次性分析 | 模板1（Zero-shot CoT）| 简单有效，成本低 |
| 重复性推理任务 | 模板2（Standard CoT）| 格式稳定，便于自动化 |
| 复杂商业分析 | 模板3（结构化报告）| 全面系统，可审阅 |
| 多选项决策 | 模板4（对比分析）| 量化比较，减少主观 |
| 高准确率需求 | 模板5（Self-consistency）| 代价高但最准确 |
