## 1. What is AI Programming?
就是让AI辅助我们编程. 目前还做不到直接编程, 但可以做到辅助编程. 比如给出提示, 给出代码片段等.

## 2. How to DO AI Programming?
### 2.1 GitHub Copilot
- 模型层：最初使用 OpenAI Codex 模型，它也是 GPT-3.5、GPT-4 的「一部分」。[现在已经完全升级，模型细节未知](https://github.blog/2023-07-28-smarter-more-efficient-coding-github-copilot-goes-beyond-codex-with-improved-ai-model/)。

- 应用层： prompt engineering。Prompt 中包含：

  1. 组织上下文：光标前和光标后的代码片段
  2. 获取代码片段：其它相关代码片段。当前文件和其它打开的 tab 里的代码被切成每个 60 行的片段，用 [Jaccard 相似度](https://zh.wikipedia.org/wiki/%E9%9B%85%E5%8D%A1%E5%B0%94%E6%8C%87%E6%95%B0)评分，取高分的
     - 为什么是打开的 tabs
     - 多少个 tabs 是有效的呢？
  3. 修饰相关上下文：被取用的代码片段的路径。用注释的方式插入，例如：`# filepath: foo/bar.py`，或者 `// filepath: foo.bar.js`
  4. 优先级：根据一些代码常识判断补全输入内容的优先级
  5. 补全格式：在函数定义、类定义、if-else 等之后，会补全整段代码，其它时候只补全当前行

### 2.2 其他工具
1. [Bito](https://bito.ai/) - 比 Copilot 还多些创新
2. [DevChat](https://www.devchat.ai/) -- 前端开源，同时卖 GPT 服务
3. [Cursor](https://www.cursor.so/) - AI first 的 IDE。
4. [Tabnine](https://www.tabnine.com/) - 代码补全，个人基础版免费
5. [Tongyi Lingma](https://tongyi.aliyun.com/lingma) -- 代码补全，免费。阿里云相关。
6. [CodeGeex](https://codegeex.cn/) -- 清华智谱 CodeGeex3Pro 免费可用
7. [Comate](https://comate.baidu.com/zh) -- 百度有免费试用版
8. [Amazon CodeWhisperer](https://aws.amazon.com/codewhisperer/) - 代码补全，免费。AWS 相关的编程能力卓越。其它凑合

### 2.3 前沿尝试
#### 2.3.1 MetaGPT：多智能体元编程框架

https://github.com/geekan/MetaGPT

它不只写代码，而且写文档、画图。详见讲座课里 MetaGPT 核心工程师的分享。

核心 prompts：https://github.com/geekan/MetaGPT/tree/main/metagpt/prompts

评价：

- 让 agent 模拟岗位这个思路挺有意思。未来的公司就是人和 agent 混合的，这样的系统架构更匹配公司治理
- 所以 MetaGPT 其实是个多 Agent 开发框架，而不是单纯的编程工具

#### 2.3.2 GPT Engineer

https://github.com/AntonOsika/gpt-engineer

指定您想要它构建的内容，AI 会要求澄清，然后构建它。

只需三步操作：

```bash
pip install gpt-engineer
vim prompt
gpt-engineer .
```

核心 prompts：https://github.com/AntonOsika/gpt-engineer/tree/main/gpt_engineer/preprompts

一句话评价：什么都能干，所以还什么都干不好。

有个专门开发 Web App 的，可用性好一些：https://gptengineer.app/

#### 2.3.3 MAGE - GPT Web App Generator

主页：https://usemage.ai/

源代码：https://github.com/wasp-lang/wasp

用 Wasp, React, Node.js 和 Prisma 生成全栈 Web 应用程序。

纯在线操作，跟着提示下载到本地执行。

核心 prompts：https://github.com/wasp-lang/wasp/blob/main/waspc/src/Wasp/AI/GenerateNewProject/Operation.hs

一句话评价：限定了技术栈，用参数做配置，提供框架代码，成品率更高。各种框架都该效仿。

#### 2.3.4 Devin

主页：https://www.cognition-labs.com/introducing-devin

一句话评价：还在内测，存在争议
