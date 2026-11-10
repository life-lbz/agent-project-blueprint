# GitHub 实例调研操作手册

调研目标：找到 **3-5 个和本项目最像的开源项目**，用来支撑架构选型的论据。调研结果必须写进"需求分析文档 → 参考实例调研"章节。

## 搜索关键词模板

按项目类型组合（每个方向选 1-2 个，再加项目自己的领域关键词）：

| 项目类型 | 关键词组合 |
|---|---|
| RAG 问答 / 文档助手 | `"document QA agent RAG github example"` + 领域词 |
| 多 Agent 协作 | `"multi-agent framework example langgraph"` + 领域词 |
| Tool-use Agent | `"function calling agent example github"` + 领域词 |
| 数据处理 / ETL Agent | `"data processing agent pipeline example"` + 领域词 |
| 代码 Agent | `"code generation agent example github"` + 领域词 |
| 客服 / 聊天 Agent | `"customer service chatbot agent example"` + 领域词 |

领域词 = 用户项目的具体领域，比如"法律"、"医疗"、"论文"、"电商"。

同时用 GitHub 的搜索语法在站点里搜：`site:github.com <关键词组合> stars:>200 pushed:>2025-01-01`

## 筛选门槛

同时满足以下 3 条才算有效调研对象：

- ⭐ Star ≥ 200（或领域内公认的小而美项目，比如某个 LangGraph 官方 example 目录）
- 📦 最近 3 个月内有 commit（`git clone` 后看 `git log --since="3 months ago"`，或 GitHub 页面的"Activity"标签）
- 📖 README 里有 demo、架构图、或生产部署说明

## 反例排除

以下情况**直接跳过**，不要浪费篇幅：

- 纯课程 demo（比如"LangChain 入门教程"配套的极简仓库）
- 只展示单个技术点，不是完整项目（比如只有 embedding 脚本，没有 Agent 主流程）
- 大量 Fork 但原仓库停更的
- 没有 license、或 license 是 AGPL 但项目要商用的（记在许可证审计里，不作为选型参考）

## 调研结果落表

找到后按以下表头写进需求分析文档：

```
| 项目名 | 链接 | Star | 最近 commit | 核心架构 | 技术栈 | 可复用点 | 不适用点 |
|---|---|---|---|---|---|---|---|
| LangGraph-RAG-Example | https://... | 320 | 2026-09 | 状态图编排 + 向量检索 | LangGraph / Chroma | 分块策略可参考 | 缺少重排 |
```

每个项目必须配一段 **"对本项目的启示"**（1-3 句），比如：
> X 项目的混合检索方案（BM25 + 向量）在领域垂直问答上召回率比纯向量高 12%，但引入 Elasticsearch 增加运维成本。若本项目目标用户对召回率敏感，可以考虑类似方案，但用 Milvus 的 hybrid search 替代。

## 调研失败的退路

如果搜不到足够项目（< 3 个），直接在需求分析文档里写：
> 未找到同类开源完整项目，参考方向转为：LangGraph 官方 example、Dify 社区模板、以及本项目的技术选型决策表中逐条对比候选方案。

不要硬凑低质量项目进来。
