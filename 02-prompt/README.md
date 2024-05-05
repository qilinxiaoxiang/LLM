## 1. What is Prompt Engineering?

提示工程也叫「指令工程」。

- Prompt 就是你发给大模型的指令，比如「讲个笑话」、「用 Python 编个贪吃蛇游戏」、「给男/女朋友写封情书」等
- 貌似简单，但意义非凡
  - 「Prompt」 是 AGI 时代的「编程语言」
  - 「Prompt 工程」是 AGI 时代的「软件工程」
  - 「提示工程师」是 AGI 时代的「程序员」
- 学会提示工程，就像学用鼠标、键盘一样，是 AGI 时代的基本技能
- 提示工程「门槛低，天花板高」，所以有人戏称 prompt 为「咒语」
- 提示工程其实就是自然语言编程
  - 最简单: 任务指令=定义角色+背景信息+任务目标+输出要求
  - 稍微复杂一点: https://sites.google.com/view/automatic-prompt-engineer
  - 最复杂: 通过输出格式约束+python代码形成复杂功能

### 提示工程示例
提示工程可以非常复杂.

- [哄哄模拟器](https://weibo.com/1727858283/ND9pOzB0K)
- 后面我们还可以看到agent等, 基础都是提示工程.

## 2. How to Do Prompt Engineering?
### 2.1 提示语构成
不要固守「模版」。模版的价值是提醒我们别漏掉什么，而不是必须遵守模版才行。

- **角色**：给 AI 定义一个最匹配任务的角色，比如：「你是一位软件工程师」「你是一位小学老师」
- **指示**：对任务进行描述
- **上下文**：给出与任务相关的其它背景信息（尤其在多轮交互中）
- **例子**：必要时给出举例，学术中称为 one-shot learning, few-shot learning 或 in-context learning；实践证明其对输出正确性有很大帮助
- **输入**：任务的输入信息；在提示词中明确的标识出输入
- **输出**：输出的格式描述，以便后继模块自动解析模型的输出结果，比如（JSON、XML）

### 2.2 对话系统基本模块
1. 语音识别(ASR)
2. 语义理解(NLU)
3. 对话管理(DM)
   1. 状态跟踪(DST)
   2. 对话策略(DP)
4. 语言生成(NLG)
5. 语音合成(TTS)

### 2.3 调优
#### 2.3.1 基础调优
- OpenAI 官方出了 [Prompt Engineering 教程](https://platform.openai.com/docs/guides/prompt-engineering)
- 具体、丰富、少歧义. 
- **大模型不是你肚子里的蛔虫.**

#### 2.3.2 进阶调优
1. 思维链（Chain of Thoughts, CoT）, 提示模型一步一步做, 通过先分析后执行, 逐步引导模型完成复杂任务
2. 自洽性（Self-Consistency）, 同样 prompt 跑多次, 通过投票选出最终结果
3. 思维树（Tree-of-thought, ToT）, 在思维链的每一步，采样多个分支.

### 2.4 安全
#### 2.4.1 防范Prompt攻击
1. Prompt注入分类器: 先判断prompt是否安全, 然后再执行后续步骤
2. 直接在输入中防御: 将安全提示词附加在用户输入的前面

#### 2.4.2 内容审核
1. OpenAI的Moderation API
2. 网易网盾