# UI 总览

欢迎使用 **DeepExtension 用户界面 (UI)** — 这是一个基于 Web 的模块化工作空间，旨在帮助领域专家与 AI 开发者协作完成模型开发的全生命周期工作。

本章节将为您提供对所有核心 UI 模块的实用概览，展示它们如何协同工作，使您无需编写代码即可完成端到端的 AI 流程。按照 DeepExtension 界面中的功能区域进行组织，帮助您了解每一部分的作用及其使用方式，主要包括以下几个部分：

### Dashboard（总览）
实时查看项目状态、训练任务、模型部署、使用统计和最近活动，一目了然。

- **基础数据统计概览**：集中展示模型训练、数据集、知识库、模型及评估等核心数据指标。
- **微调任务统计面板**：通过柱状图直观呈现不同类型的模型训练任务分布情况。
- **基础模型分布图**：环状图形式展示已训练模型中基础模型的占比情况。
- **模型评估分析视图**：面积占比图形式展示评估任务中各模式的数量分布。
- **第三方模型资源图谱**：环状图呈现系统内第三方模型的厂商分布及类型占比。

### DeepPrompt
使用结构化提示模板引导 LLM 行为，非常适合业务逻辑对齐和构建可重复的 AI 任务。

相比传统的 prompt 工作台，**DeepPrompt** 提供了与数据和模型更深度的集成能力，允许用户：

- 在提示中直接嵌入和引用基于文档的知识
- 对 **训练阶段的适配器或 PEFT 检查点** 直接进行推理
- 利用部分训练结果模拟生产行为，加速评估周期

### 模型训练
启动训练任务，使用基础模型，结合微调方法（如 **SFT**、**GRPO**），可选择是否启用参数高效微调（如 **LoRA**），并支持自定义超参数。所有训练任务都通过 UI 完成，无需编程。

亮点功能包括：

- **“复制训练”按钮**：一键复制先前的训练任务配置，仅需更改少数参数（如基础模型、数据集、LoRA rank、学习率）即可快速创建对比实验。
- **训练日志与评估数据可视化**：实时查看 Loss 曲线、奖励分数和关键指标，训练过程一目了然。
- **多训练对比**：可一次性选择多个训练任务进行并列对比，包括性能、配置、输入输出等。

### 数据集管理
可以上传、版本化、标注和管理数据集，支持 JSONL 和 JSON 格式。

### 文档嵌入（RAG）
将大规模文档嵌入到向量空间，用于 RAG（检索增强生成）场景，支持知识库创建与索引管理。

### 模型评估

DeepExtension 提供了强大的 **后来处理模型评估框架**，可使用真实数据集对比多个模型输出效果。

关键特性包括：

- 自动评估数据集中的 **问题样本** 
- 提供四种灵活的评估模式
- 每次评估前可进行 **预览检查**（模型、数据集、评分 prompt 等）
- 后台处理运行，支持大规模模型评估
- 支持导出结果到本地文件，亦可直接在 UI 中查看
- **支持任意模型**：包括第三方 API、本地训练模型或已部署的内部模型

该系统可帮助团队自信地对比模型、评估对齐程度并建立标准化评估流程。

### 模型管理
通过以下模块追踪系统中所有模型：

- **第三方模型**：您连接的外部模型（如 OpenAI、Anthropic、ModelScope 等）
- **基础模型**：用于微调或推理的预训练模型
- **训练模型**：训练过程产生的中间产物，通常是 PEFT adapter 或 checkpoint（又称训练产物）
- **保存模型**：将训练模型合并至基础模型，生成的独立版本快照，可部署或用于实验
- **已部署模型**：已部署运行的模型，支持 API 调用或工具集成，可实现实时推理，类似于一个基础模型

每类模型代表训练生命周期中从初步训练到正式部署的每一个阶段。用户可以通过 UI 上的一键操作推进模型生命周期：

- 将 **训练模型** 转换为 **保存模型**
- 将 **保存模型** 部署为 **已部署模型**
- 删除任意阶段不再需要的模型

此结构帮助用户掌控版本、发布和清理流程，确保系统中保留的都是有价值的模型。

### 设置

- **部署工具配置**：维护与推理部署工具的集成配置  
  当前仅支持 **Ollama**，当部署保存模型时，系统将根据此配置连接本地 Ollama 环境。未来将支持更多如 **LM Studio** 的本地部署工具。
- **训练方法管理**：配置和注册自定义微调策略（如 SFT、GRPO）
- **用户管理**：管理团队成员、权限和项目访问控制

---

## 适用人群

本指南适合：

- **领域专家**：无需编程也可参与模型训练与评估
- **数据科学家 / ML 工程师**：配置训练策略并实现训练逻辑
- **项目管理者**：掌控 AI 流程、团队权限和部署状态

---

## 下一步建议

您可以继续阅读以下章节了解详情：

- [DeepPrompt](deep-prompt.zh.md)  
- [模型训练](model-training.zh.md)  
- [数据集管理](dataset-management.zh.md)  
- [文档嵌入](document-embedding.zh.md)  
- [模型评估](model-assessment.zh.md)  
- [模型管理](thirdparty-models.zh.md)  
- [设置](deployment-tool-configuration.zh.md)

---

*DeepExtension — 为现实 AI 场景打造的统一工作空间*