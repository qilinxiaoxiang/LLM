# 1. What is MLLM?
- 模态(modal), 是指在某种特定情况下的特定形式. 在自然语言处理中, 模态通常指的是文本、图片、音频、视频等不同的数据形式.
- MLLM, Multimodal Language Model, 多模态大语言模型. 由LLM扩展而来的具有接收与推理多模态信息能力的模型.
- 发展历程
  1. ViT(Vision Transformer): 2020年, Google 提出了 Vision Transformer, 用于图像分类任务. 图像表示的token化.
  2. 基于Transformer架构的图像-文本联合建模, 如VisualBert.
  3. 大规模图-文Token对其模型, 如CLIP. 能做开域下的图像分类-目标检测-图像分割.
  4. MLLM, 用于处理多模态信息的大语言模型出现.
- 示例
  - OpenAI GPT4v(GPT-4 with Vision).
    1. 遵循文字提示
    2. 理解视觉指向和参考
    3. 支持视觉+文本联合提示
    4. 少样本上下文学习
    5. 强大的视觉认知能力. 如识人, 识地, 识菜, 识Logo, 医疗图像描述, 通用场景分析, 文字识别, 图表文档理解, 计数, 目标定位.
    6. 不支持视频, 但支持传入多长图片, 按时序进行视觉信号理解.
  - Google Gemini
    1. 支持多模态内容输出
    2. 复杂图像理解与代码生成
- 应用
  - 工业
  - 医疗
  - 视觉内容认知与编辑
  - 具身智能
  - 新一代人机交互

# 2. Why do We Need MLLM?
- 传统LLM只能处理文本信息, 无法处理多模态信息.
- 现实世界中, 信息不仅仅是文本, 还有图片、音频、视频等多种形式.
- MLLM能够处理多模态信息, 使得模型能够更好地理解和处理现实世界中的信息.

# 3. How to Implement MLLM?
## 3.1 LLaVA-v1.5-13B
### 3.1.1 训练
1. 阶段一: 特征对齐的预训练. 仅更新特征映射矩阵. 用于对齐不同模态的特征表示. 通过对齐特征表示, 使得不同模态的特征表示在同一空间中更加接近. 
    - 输入图像分辨率336px, 8张A100(80G)耗时5.5h.
2. 阶段二: 端到端微调. 特征投影矩阵和LLM都进行更新. 用于在特定任务上进行端到端的微调. 通过端到端微调, 使得模型能够更好地适应特定任务. 
    - 输入图像分辨率336px, 8张A100(80G)耗时20h.

### 3.1.2 部署
1. 启动API server
2. 启动WebUI
3. 启动Worker

## 3.2 改进

1. LLaVA1.6(LLaVA-Next)
   - 支持3种更高分辨率的图像输入
   - 更好的视觉推理和OCR能力
   - 更多场景下进行更好的视觉对话
   - 更好的世界知识和逻辑推理能力.
2. Fuyu-8B
   - 改进Vision Encoder, 支持任意分辨率图像输入
3. InternLM-XComposer2
   - 改进Projection机制
4. X-LLM
   - 把多模态信息当做一种外语
5. Next-GPT
    - Any-to-Any Multimodal LLM
    - 三阶段训练
        1. 阶段一: 以LLM为中心的Encoder特征对齐, 只更新input projection layer
        2. 阶段二: Decoder输出结果与指令对齐, 只更新output projection layer
        3. 阶段三: 指令微调, LLM Lora微调, 适应特定任务, 更新LLM、input projection layer、output projection layer.
6. Multimodal Agents
    - Chaining Multimodal Experts with LLMs

## 3.3 效果评估

- 多模态大模型榜单: https://github.com/BradyFU/Awesome-Multimodal-Large-Language-Models/tree/Evaluation
- 多模态大模型拓展信息: https://github.com/BradyFU/Awesome-Multimodal-Large-Language-Models/