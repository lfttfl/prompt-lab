# 提示词模板库

> 可直接复用的提示词模板，将 `{花括号}` 替换为实际内容即可使用

## 模板列表

| 模板 | 适用场景 | 核心技术 |
|------|---------|---------|
| [basic-template.md](./basic-template.md) | 日常通用任务 | 六要素结构（RTCFCE）|
| [cot-template.md](./cot-template.md) | 复杂推理分析 | 思维链（CoT）|
| [role-template.md](./role-template.md) | AI角色/助手设计 | BEKSCO角色框架 |
| [rag-template.md](./rag-template.md) | 知识库问答系统 | RAG提示词链 |

## 使用指南

1. 选择最接近你场景的模板
2. 将 `{变量名}` 替换为实际内容
3. 根据你的需求调整约束和格式部分
4. 用3-5个测试用例验证效果
5. 迭代优化（参考模块06方法论）

## 变量命名规范

本模板库使用以下变量命名约定：
- `{user_input}` — 用户的实际输入
- `{context}` — 背景信息或检索结果
- `{output_format}` — 期望的输出格式说明
- `{examples}` — Few-shot 示例
