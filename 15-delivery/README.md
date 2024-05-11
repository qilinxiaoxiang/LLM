# 1. 硬件选型
## 1.1 计算卡
### 1.1.1 GPU
| 显卡 | 目标市场 | 性能 | 应用场景 | 价格 |
| :---: | :-----------: | :----: | :--------------------------------: | :----------: |
| T4 | 企业/AI 推理 | 适中 | AI 推理, 轻量级训练, 图形渲染 | 7999(14G) |
| 4090 | 消费者 | 非常高 | 通用计算, 图形渲染, 高端游戏, 4K/8K 视频编辑 | 14599(24G) |
| A10 | 企业/图形 | 适中 | 图形渲染, 轻量级计算 | 18999(24G) |
| A6000 | 企业/图形 | 适中 | 图形渲染, 轻量级计算 | 32999（48G） |
| V100 | 数据中心/AI | 高 | 深度学习训练/推理, 高性能计算 | 42999(32G) |
| A100 | 数据中心/AI | 高 | 深度学习训练/推理, 高性能计算 | 69999(40G) |
| A800 | 数据中心/AI | 中等 | 深度学习推理, 高性能计算, 大数据分析 | 110000 |
| H100 | 数据中心/AI | 高 | 深度学习训练/推理, 高性能计算, 大数据分析 | 242000 |

- 美国商务部限制 GPU 对华出口的算力不超过 4800 TOPS 和带宽不超过 600 GB/s，导致最强的 H100 和 A100 禁售。黄教主随后推出针对中国市场的 A800 和 H800。
  - TOPS, tera(10^12) operations per second
- H100 与 A100：H100 比 A100 快多少？ 16-bit 推理快约 3.5 倍，16-bit 训练快约 2.3 倍。
  - 同时还在很多HPC(High Performance Computation)任务上快很多
    - Climate Modelling, 气象建模
    - Genomics, 基因组
    - Lattice QCD(Quantum Chromodynamics), 格点量子色动力学. 使用点阵或网格来近似宇宙的连续时空。这种方法特别适用于研究强相互作用，这是四种基本力之一，负责在质子、中子和其他粒子内部将夸克和胶子粘合在一起。通过将时空离散化为网格，物理学家可以使用强大的计算方法来模拟和研究这些粒子及其相互作用的行为。
    - 8K 3D FFT(Fast Fourier Transform), 8K 3D 快速傅里叶变换. 明FFT正被应用于每个维度大约有8000个数据点的三维数据集。这种高分辨率的FFT在需要详细分析量子场论（如QCD）中发现的复杂空间结构的模拟中至关重要。

### 1.1.2 LPU
- Linear Processing Unit.
- 来自Groq公司, 千古个工程师创办. 专注于AI加速器.
- 它的特点是高性能, 低功耗, 低延迟, 尤其是在推理任务上.
- [使用文档](https://console.groq.com/docs/quickstart)
- https://console.groq.com/playground?model=llama3-70b-8192

## 1.2 服务器
### 1.2.1 生产环境
#### 国内主流

- **阿里云**：https://www.aliyun.com/product/ecs/gpu （可[申请免费试用](https://free.aliyun.com/?product=9602825&spm=5176.28055625.J_5831864660.9.e939154aYoM8ST&scm=20140722.M_9553144.P_154.MO_1802-ID_9553144-MID_9553144-CID_20080-ST_7663-V_1)）
- **腾讯云**：https://cloud.tencent.com/act/pro/gpu-study
- **火山引擎**：https://www.volcengine.com/product/gpu

#### 国外主流

- **AWS**：[https://aws.amazon.com](https://aws.amazon.com)
- **Vultr**：[https://www.vultr.com](https://www.vultr.com)
- **TPU**：[https://cloud.google.com/tpu](https://cloud.google.com/tpu?hl=zh-cn)

TPU 是 Google 专门用于加速机器学习的硬件。它特别适合大规模深度学习任务，通过高效的架构在性能和能源消耗上表现出色。

它的优点和应用场景：

1. **高性能和能效：** TPU 可以更快地完成任务，同时消耗较少的能源，降低成本。

2. **大规模训练：** TPU 适用于大规模深度学习训练，能够高效地处理大量数据。

3. **实时推理：** 适合需要快速响应的任务，如实时图像识别和文本分析。

4. **云端使用：** Google Cloud 提供 TPU 服务，允许用户根据需求使用，无需购买硬件。

适用于图像处理、自然语言处理、推荐系统等多个领域。

在国外，科研机构、大公司和初创企业普遍使用 TPU。

#### 下面是对两款 NVIDIA GPU 在他主流厂商的价格进行对比：

- A100：在云服务中，A100 是顶级的企业级 GPU，适用于高性能计算需求。
- T4：相比之下，T4 更为经济，适合日常模型微调和推理任务。

NVIDIA A100：

| 云服务提供商 | CPU 核心数 | 内存（GiB） | 价格（元/小时） |
| ------------ | ---------- | ----------- | --------------- |
| 火山引擎    | 14 核      | 245         | 40.39           |
| 阿里云     | 16 vCPU    | 125         | 34.742          |
| 腾讯云      | 16 核      | 96          | 28.64           |

NVIDIA T4：

| 云服务提供商 | CPU 核心数 | 内存（GiB）  | 价格（元/小时） |
| ------------ | ---------- | -----------  | --------------- |
| 阿里云       | 4 vCPU     | 15         | 11.63           |
| 火山引擎     | 4 核       | 16          | 11.28           |
| 腾讯云       | 8 核       | 32      | 8.68            |

#### 要点
- 对于本地个人研发项目，GeForce RTX 4090 等消费级 GPU 足以满足中等规模的需求。</li>
- 对于公司的大规模数据和复杂模型，推荐使用如 NVIDIA A100 的高性能 GPU。</li>
- 数据规模小时，可考虑预算内的 A10 或 T4 型号。</li>
- 如果追求性价比，可以选择把 4090 显卡搭建服务器使用，也可以选择市面的第三方服务，比如：AutoDL 的 4090 服务</li>

#### 参考资料
- https://gpus.llm-utils.org/cloud-gpu-guide/
- https://gpus.llm-utils.org/nvidia-h100-gpus-supply-and-demand/
- 火山引擎提供的这个[价格计算器](https://www.volcengine.com/pricing?product=ECS&tab=2)很方便，做个大概的云服务器 GPU 选型价格参考。其它服务厂商价格相差不是很多。

### 1.2.2 学习环境
主要用于学习和训练，不适合提供服务。

- **Colab**：谷歌出品，升级服务仅需 9 美金。https://colab.google.com
- **Kaggle**：免费，每周 30 小时 T4，P100 可用。https://www.kaggle.com
- **AutoDL**：价格亲民，支持 Jupyter Notebook 及 ssh，国内首选。https://www.autodl.com

# 2. 软件选型
## 2.1 大模型
1. 斗兽场: https://chat.lmsys.org/
2. 大模型介绍: https://llmmodels.org/
3. Hugging Face模型: https://huggingface.co/models
4. 大模型热度排行榜: https://llm.extractum.io/list/?trending
5. 大模型能力排行榜: https://rank.opencompass.org.cn/leaderboard-llm
   - OpenAI 的 GPT-4 在质量指标方面是明显的质量领导者。然而，包括 Gemini Pro 和 Mixtral 8x7B 在内的型号在某些方面已经达到了 GPT-3.5 的性能。
6. 国产大模型: https://github.com/wgwang/awesome-LLMs-In-China

## 2.2 UI
1. [lobe-chat](https://github.com/lobehub/lobe-chat)
2. [ChatGPT-Next-Web](https://github.com/ChatGPTNextWeb/ChatGPT-Next-Web)
3. [open-webui](https://github.com/open-webui/open-webui)

## 2.3 代理
业务代码如果放在国外会有延迟, 所以可以让业务代码调用代理服务器

### 2.3.1 开源项目
1. [agi-proxy](https://github.com/agicto/agi-proxy)
2. [openai-forward](https://github.com/KenyonY/openai-forward)
3. [one-api](https://github.com/songquanpeng/one-api)

### 2.3.2 服务器选择
| 服务商                | 访问地址                                         | 主要服务                | 特性                                               | 适用场景                             | 起始价格             |
| --------------------- | ------------------------------------------------ | ----------------------- | -------------------------------------------------- | ------------------------------------ | -------------------- |
| Cloudflare            | [cloudflare.com](https://cloudflare.com/)        | CDN, 安全服务           | 全球 CDN, DDoS 保护, 自动 HTTPS                    | 增强网站性能和安全                   | 免费计划开始         |
| Vercel                | [vercel.com](https://vercel.com/)                | 静态站点和 SSR 应用托管 | 集成 Git, 自动部署, 无服务器函数                   | 前端开发和 JAMstack 项目             | 免费计划开始         |
| Render                | [render.com](https://render.com)                 | 应用托管, 数据库托管    | 易于使用, 自动部署, 免费 SSL 证书                  | 适合所有类型的 Web 应用和数据库托管  | 免费计划开始         |
| DigitalOcean          | [digitalocean.com](https://digitalocean.com)     | 云基础设施服务          | 简单易用, SSD 存储, 数据中心选择                   | 中小型企业的 Web 应用托管            | $5/月起              |
| AWS                   | aws.amazon.com                                   | 综合云服务              | 广泛的服务选择, 可扩展性, 全球数据中心             | 适合各种规模和需求的企业             | 按使用付费，有免费层 |
| Microsoft Azure       | azure.microsoft.com                              | 综合云服务              | 多样的服务, 企业级功能, 混合云支持                 | 企业级应用和混合云解决方案           | 按使用付费，有免费层 |
| Google Cloud Platform | cloud.google.com                                 | 综合云服务              | 高性能计算服务, 数据分析, 机器学习                 | 数据密集型应用和机器学习项目         | 按使用付费，有免费层 |
| 阿里云国际版          | [intl.aliyun.com](https://www.alibabacloud.com/) | 综合云服务              | 全球化数据中心, 多语言客户支持, 丰富的云产品和服务 | 适合需要在中国以外地区扩展业务的企业 | 按使用付费           |

### 2.3.3 其他
- 限制模型
- 限制接口
- 限制速率

## 2.4 向量数据库
### 2.4.1 向量数据库的应用场景
1. **知识库/问答系统**：通过大模型对大量的文本数据进行编码，将结果存储在向量数据库中。当有新的查询进来时，可以迅速找到与查询最相似的文档或文本段落，从而快速返回答案。
2. **图像识别与搜索**：图片经过 Embedding 技术后，可以转化为一个向量。当用户上传一张图片进行搜索时，向量数据库可以快速找到与其最相似的图片。
3. **内容推荐系统**：根据用户的浏览、购买或其他行为，可以使用模型为用户生成一个向量表示，然后查询向量数据库中最相似的内容向量，从而为用户推荐相关内容。

### 2.4.2 向量数据库的选择
| 数据库   | 适用场景                                | 集成与生态系统                                                             | 性能                                 | 本地使用                               | 近期筹资               | 特异性                              |
| -------- | --------------------------------------- | -------------------------------------------------------------------------- | ------------------------------------ | -------------------------------------- |--------------------| ----------------------------------- |
| Pinecone | 适合那些寻找即插即用解决方案的企业      | 与 TensorFlow、PyTorch 和 Scikit-learn 等主要机器学习框架有良好的集成      | 与其他矢量数据库相似                 | 不可能（非开源）                       | 100M B 轮于 27/04/23 | 是唯一一个非开源的，不能本地迭代    |
| Qdrant   | 适用于要求高性能和灵活性的应用          | 主要与 DVC 集成，同时支持常见的数据版本控制工具                            | 优越（Rust 编码）；基准测试对比      | 可以（docker-compose, 磁盘文件, 内存） | 7.5M 种子轮于 24/04/23 | 高性能，本地灵活，与 DVC 集成       |
| Weaviate | 适用于需要 GraphQL 查询和本地存储的应用 | 提供开放 API 以供开发，支持 Python、JavaScript 和 Go 等多种客户端库        | 与其他矢量数据库相似                 | 可以（docker-compose, 磁盘文件）       | 50M B 轮于 21/04/23  | 支持 GraphQL 查询，本地磁盘文件使用 |
| Milvus   | 适合大型组织和需求复杂的应用            | 提供丰富的插件，如数据导入工具、数据标注工具和与其他数据库的连接器         | 与其他矢量数据库相似                 | 可以（docker-compose）                 | 60M B 轮于 24/08/22  | 经过时间验证，但微服务架构复杂      |
| ChromaDB | 适用于简单的应用和 Python 环境          | 主要集成 Python 生态，如 NumPy、Pandas 和 Scikit-learn，方便数据分析和处理 | 可能较差（完全 Python 编码，无基准） | 可以（docker-compose, 磁盘文件, 内存） | 18M 万种子轮于 06/04/23 | 简单，完全用 Python 编码，易于定制  |

### 2.4.3 要点
- 通用数据库最初不是为矢量搜索而设计的，因此不如专用矢量数据库效率高。
- 如果您使用少量向量（例如<10万）并且已经使用了其中一个数据库（根据stackoverflow 2023调查，49%的专业开发人员使用PostgreSQL），务实的选择肯定是坚持下去，以保持您的技术堆栈简单。
- 当成本和/或延迟成为问题时，请考虑使用专用的矢量数据库（如 Pinecone、Qdrant、Weaviate、Milvus）可以实现更高性能和更好的查询结果。
- 参考资料
  - https://www.sicara.fr/blog-technique/how-to-choose-your-vector-database-in-2023

# 3. 部署
## 3.1 vllm
### 3.1.1 参考资料
- 官方网址: https://vllm.ai
- 官方 github 地址：https://github.com/vllm-project/vllm
- 支持的模型：https://vllm.readthedocs.io/en/latest/models/supported_models.html

### 3.1.2 部署步骤
1. 模型下载, huggingface直接下载, 或者从网盘下载
2. 设置conda环境
3. 安装vllm, `pip install vllm`
   - 如果需要分布式推理, 还需要安装ray, `pip install ray`
4. 运行我们的模型, `python -m vllm.entrypoints.openai.api_server --model /root/autodl-tmp/Yi-6B-Chat --trust-remote-code --port 6006`
   - 如果需要分布式推理, 需要加上`--tensor-parallel-size`参数, 如`--tensor-parallel-size 2`
5. 使用, `curl https://u202774-8479-111790f4.westb.seetacloud.com:8443/v1/chat/completions - H "Content-Type: application/json" -d '{}'`

## 3.2 云服务商
1. 阿里云
   - PAI(Platform for AI)
   - 百炼
2. 腾讯云
   - HAI(Hyper Application Inventor)
3. 百度云
   - 千帆
4. 国外云
   - Paperspace
   - Lepton AI

## 3.3 实战案例
1. 部署Weaviate向量数据库, https://weaviate.io/developers/weaviate/installation/docker-compose
2. 部署基于weaviate向量数据库的RAG项目
   1. `git clone https://github.com/weaviate/Verba`
   2. `cd Verba`
   3. `pip install -e .`

# 4. 安全
## 4.1 内容安全
1. 敏感词库管理与用户输入过滤：
   - 定期更新敏感词汇和短语库，应对文化变迁和当前事件。
   - 使用第三方服务或自建工具进行实时输入过滤和提示。推荐使用：
     - 网易易盾：[https://dun.163.com/product/text-detection](https://dun.163.com/product/text-detection)
     - 百度文本内容安全：[https://ai.baidu.com/tech/textcensoring](https://ai.baidu.com/tech/textcensoring)
2. [详细链接：GPT4 内置提示词](https://chat.openai.com/share/56179c99-7a0b-4b60-a92c-3a984094c6e1)
3. OpenAI的modeeration, 对中文不友好, https://platform.openai.com/docs/guides/moderation/overview
4. 提示词破坏, 参考https://github.com/RobustNLP/CipherChat

## 4.2 备案