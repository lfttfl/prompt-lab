# RAG 提示词链模板

> 适用场景：知识库问答、企业文档搜索、基于文档的 AI 助手
> 核心技术：查询改写 + 上下文注入 + 引用格式 + 幻觉控制

---

## 完整 RAG 三步提示词链

### 步骤1：查询改写

```
你是搜索查询优化专家。将用户的问题改写为更适合在专业知识库中检索的查询词。

改写原则：
- 扩展同义词和相关概念（如"怎么请假"→"请假流程"、"休假申请"）
- 将口语化表达改为书面/专业表达
- 如果问题包含多个独立子问题，拆分为独立查询
- 每行一个查询，不编号，不解释

输出3个查询词，每行一个。

用户问题：{user_question}
改写后的查询：
```

---

### 步骤2：上下文注入与回答生成

```
你是{应用名称}的知识库助手。请基于以下参考资料回答用户问题。

【参考资料】
{retrieved_chunks}

【用户问题】
{user_question}

【回答规则】
1. 只使用参考资料中的信息，不添加外部知识
2. 如果参考资料不足以回答问题，明确说明："根据现有资料，无法完整回答此问题。
   建议您[替代方案，如：联系相关部门/查看完整文档]"
3. 对不确定或模糊的信息，加上"（根据资料，可能...）"
4. 在回答末尾标注引用：[来源：{文档名}，第{X}段]
5. 回答长度：100-300字，除非问题需要详细说明

【回答】
```

---

### 步骤3：引用验证（可选，用于高准确率场景）

```
检查以下AI回答是否与参考资料一致。

【参考资料】
{retrieved_chunks}

【AI回答】
{generated_answer}

逐句检查回答中的每个关键信息点：
- 准确：[信息点] → 来源：[具体段落]
- 不准确：[信息点] → 与资料冲突：[说明]
- 无依据：[信息点] → 资料中未提及

最终评级：
- 高置信：所有关键信息均有资料支持
- 中置信：部分信息有支持，部分来自推断
- 低置信：存在不准确或无依据的信息，建议人工核实
```

---

## 完整 Python 实现示例

```python
import anthropic

client = anthropic.Anthropic()

def rag_pipeline(user_question: str, knowledge_base_search_fn) -> dict:
    """
    完整的RAG提示词链实现
    knowledge_base_search_fn: 接受查询字符串，返回相关文档列表的函数
    """
    
    # 步骤1：查询改写
    rewrite_response = client.messages.create(
        model="claude-sonnet-4-6",
        max_tokens=256,
        messages=[{
            "role": "user",
            "content": f"""将以下用户问题改写为3个更精确的搜索查询，每行一个：

用户问题：{user_question}
改写后的查询："""
        }],
        temperature=0
    )
    
    queries = rewrite_response.content[0].text.strip().split('\n')
    queries = [q.strip() for q in queries if q.strip()]
    
    # 步骤2：检索（使用传入的搜索函数）
    all_chunks = []
    for query in queries:
        chunks = knowledge_base_search_fn(query)
        all_chunks.extend(chunks)
    
    # 去重并格式化
    unique_chunks = list(dict.fromkeys(all_chunks))
    context = "\n\n---\n\n".join(unique_chunks[:5])  # 取前5个最相关结果
    
    # 步骤3：生成回答
    answer_response = client.messages.create(
        model="claude-sonnet-4-6",
        max_tokens=1024,
        system="你是企业知识库助手，只基于提供的参考资料回答问题，不添加外部知识。",
        messages=[{
            "role": "user",
            "content": f"""【参考资料】
{context}

【用户问题】
{user_question}

请基于以上资料回答问题，并在末尾标注来源。
如果资料不足，明确说明无法完整回答并建议替代方案。"""
        }],
        temperature=0
    )
    
    return {
        "queries": queries,
        "context_used": context,
        "answer": answer_response.content[0].text
    }
```

---

## 常见优化点

| 问题现象 | 可能原因 | 优化方向 |
|---------|---------|---------|
| 回答包含资料外的信息 | 上下文注入规则不够强 | 加强"只使用参考资料"的指令，增加验证步骤 |
| 无法找到相关内容 | 查询改写不够充分 | 增加同义词扩展，尝试关键词提取 |
| 引用格式不一致 | 未明确引用格式 | 在提示词中提供引用格式示例 |
| 回答过长 | 未限制长度 | 加入字数限制；或分"摘要版"和"详细版"模式 |
| 幻觉率高 | 缺少引用验证 | 启用步骤3的验证提示词 |
