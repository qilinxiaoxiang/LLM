## 1. What is Function Calling?
就是让大模型有调用外部接口的能力.

## 2. Why do We Need Function Calling?
### 2.1 大模型两大缺陷
1. 并非知晓一切
   1. 训练数据不可能什么都有。垂直、非公开数据必有欠缺
   2. 不知道最新信息。大模型的训练周期很长，且更新一次耗资巨大，还有越训越傻的风险。所以 ta 不可能实时训练。GPT-3.5 的知识截至 2021 年 9 月，GPT-4 是 2023 年 12 月。
2. 没有「真逻辑」。它表现出的逻辑、推理，是训练文本的统计规律，而不是真正的逻辑，所以有幻觉。

所以：大模型需要连接真实世界，并对接真逻辑系统。

### 2.2 不用重复造轮子
- 现实世界中, 通过前辈们的努力, 已经有大量现成的成熟能力以API的形式提供给人们使用.
  - 比如获取时间, 获取地理位置, 获取天气, 获取股票信息等等.
- 人们当然可以手工调用这些API然后把返回结果贴给大模型, 但与其这样, 不如让大模型自己调用这些API.

## 3. How to Implement Function Calling?
### 3.1 OpenAI Function Calling
Function Calling 官方文档: https://platform.openai.com/docs/guides/function-calling

1. Function Calling 中的函数与参数的描述也是一种 Prompt
2. 这种 Prompt 也需要调优，否则会影响函数的召回、参数的准确性，甚至让 GPT 产生幻觉
3. 只有 gpt-3.5-turbo-1106 和 gpt-4-1106-preview 及更高版本的模型可用本次课介绍的方法
4. 使用模型别名 gpt-3.5-turbo 和 gpt-4-turbo 会调用最新模型，但要防范模型升级带来的负面效果，做好充足测试
5. 函数声明是消耗 token 的。要在功能覆盖、省钱、节约上下文窗口之间找到最佳平衡
6. Function Calling 不仅可以调用读函数，也能调用写函数。但官方强烈建议，在写之前，一定要有真人做确认


### 3.2 OpenAI Actions
Actions 官方文档：https://platform.openai.com/docs/actions

### 3.3 OpenAI GPTs
1. 无需编程，就能定制个性对话机器人的平台
2. 可以放入自己的知识库，实现 RAG（后面会讲）
3. 可以通过 actions 对接专有数据和功能
4. 内置 DALL·E 3 文生图和 Code Interpreter 能力
5. 只有 ChatGPT Plus 会员可以使用
