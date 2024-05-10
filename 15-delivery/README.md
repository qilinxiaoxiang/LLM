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