## 1. What is LangChain?
- LangChain 也是一套面向大模型的开发框架（SDK）
- LangChain 是 AGI 时代软件工程的一个探索和原型
- LangChain 迭代速度快，几乎每天一个版本
- 学习 Langchain 要关注接口变更

## 2. Why Do We Need LangChain?
所有开发框架（SDK）的核心价值，都是降低开发、维护成本。

大语言模型开发框架的价值，是让开发者可以更方便地开发基于大语言模型的应用。主要提供两类帮助：

1. 第三方能力抽象。比如 LLM、向量数据库、搜索引擎等
2. 常用工具、方案封装
3. 底层实现封装。比如流式接口、超时重连、异步与并行等

好的开发框架，需要具备以下特点：

1. 可靠性、鲁棒性
2. 可维护性高
3. 高内聚、低耦合
4. 易用

举些通俗的例子：

- 与外部功能解依赖
  - 比如可以随意更换 LLM 而不用大量重构代码
  - 更换三方工具也同理
- 经常变的部分要在外部维护而不是放在代码里
  - 比如 Prompt 模板
- 各种环境下都适用
  - 比如线程安全
- 方便调试和测试
  - 至少要能感觉到用了比不用方便吧
  - 合法的输入不会引发框架内部的报错

选对了框架，事半功倍；反之，事倍功半。

## 3. How to Use LangChain?
### 3.1 LangChain的核心组件
1. 模型 I/O 封装
   - LLMs：大语言模型
   - Chat Models：一般基于 LLMs，但按对话结构重新封装
   - PromptTemple：提示词模板
   - OutputParser：解析输出
2. 数据连接封装
   - Document Loaders：各种格式文件的加载器
   - Document Transformers：对文档的常用操作，如：split, filter, translate, extract metadata, etc
   - Text Embedding Models：文本向量化表示，用于检索等操作（啥意思？别急，后面详细讲）
   - Vector Stores: （面向检索的）向量的存储
   - Retrievers: 向量的检索
3. 记忆封装
   - Memory：这里不是物理内存，从文本的角度，可以理解为“上文”、“历史记录”或者说“记忆力”的管理
4. 架构封装
   - Chain：实现一个功能或者一系列顺序功能组合
   - Agent：根据用户输入，自动规划执行步骤，自动选择每步需要的工具，最终完成用户指定的功能
     - Tools：调用外部功能的函数，例如：调 google 搜索、文件 I/O、Linux Shell 等等
     - Toolkits：操作某软件的一组工具集，例如：操作 DB、操作 Gmail 等等
5. Callbacks


