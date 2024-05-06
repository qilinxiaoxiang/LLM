## 1. What is LLM Application Maintenance?
维护一个生产级的 LLM 应用，我们需要做什么？

1. 各种指标监控与统计：访问记录、响应时长、Token 用量、计费等等
2. 调试 Prompt
3. 测试/验证系统的相关评估指标
4. 数据集管理（便于回归测试）
5. Prompt 版本管理（便于升级/回滚）

## 2. LLM App Maintenance Platform 
1. LangSmith: LangChain 的官方平台，SaaS 服务（付费），非开源
2. LangFuse: 开源 + SaaS（免费/付费），LangSmith 平替，可集成 LangChain 也可直接对接 OpenAI API
3. Prompt Flow：微软开发，开源 + Azure AI 云服务