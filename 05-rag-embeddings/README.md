## 1. What is RAG?
RAG, Retrieval-Augmented Generation. 是一种结合了检索和生成的模型. 通过检索到的信息来辅助生成. 也就是说, RAG会先检索到相关信息, 然后再生成回答.

## 2. Why do we need RAG?
1. LLM 的知识不是实时的
2. LLM 可能不知道你私有的领域/业务知识

## 3. How to Implement RAG?
### 3.1 搭建过程

1. 文档加载，并按一定条件**切割**成片段
2. 将切割的文本片段灌入**检索引擎**
3. 封装**检索接口**
4. 构建**调用流程**：Query -> 检索 -> Prompt -> LLM -> 回复

#### 3.1.1 离线步骤
1. 文档加载
2. 文档切分
3. 向量化
4. 灌入向量数据库

#### 3.1.2 在线步骤
1. 获得用户问题
2. 用户问题向量化
3. 检索向量数据库
4. 将检索结果和用户问题填入 Prompt 模版
5. 用最终获得的 Prompt 调用 LLM
6. 由 LLM 生成回复

#### 3.1.3 Debug
1. 检查预处理效果：文档加载是否正确，切割的是否合理
2. 测试检索效果：问题检索回来的文本片段是否包含答案
3. 测试大模型能力：给定问题和包含答案文本片段的前提下，大模型能不能正确回答问题

### 3.2 检索原理
#### 3.2.1 关键词检索
1. 通过Elasticsearch这样的工具进行检索
2. 通过谷歌/百度这样的搜索引擎服务进行检索

局限性是显而易见的, 同一个语义，用词不同，可能导致检索不到有效的结果. 

优点是简单快速.

#### 3.2.2 向量检索
1. 通过embedding模型，将文本转换成向量. 
   1. 我们可以把人类能表达的所有语义看做一个高维空间, 任何文本都可以转化成这个高维空间中的一个向量.
   2. 这个模型需要进行训练, 让语义相关的文本在这个高维空间中距离更近, 让语义无关的文本在这个高位空间中距离更远.
   3. 很多第三方API提供将文本映射成向量的能力. 好的API可以跨语言, 将语言不同但语义相近的文本映射成相近的向量.
2. 通过向量相似度计算，找到最相似的文本.
   1. 相似度定义
      1. 欧氏距离
      2. 余弦距离
   2. 向量数据库
      1. 向量数据库的意义是快速的检索
      2. 向量数据库本身不生成向量，向量是由 Embedding 模型产生的
      3. 向量数据库与传统的关系型数据库是互补的，不是替代关系，在实际应用中根据实际需求经常同时使用。

### 3.3 进阶
#### 3.3.1 文本分割的粒度
1. 粒度太大可能导致检索不精准，粒度太小可能导致信息不全面
2. 问题的答案可能跨越两个片段

按一定粒度，部分重叠式的切割文本，使上下文更完整

#### 3.3.2 检索后排序
- 有时，最合适的答案不一定排在检索的最前面
  - 检索时可以过招回一部分文本, 通过一个排序模型对 query 和 document 重新打分排序
  - 传统的关键字检索（稀疏表示）与向量检索（稠密表示）各有优劣。比如文档中包含很长的专有名词，关键字检索往往更精准而向量检索容易引入概念混淆。有时候我们需要结合不同的检索算法，来达到比单一检索算法更优的效果。这就是混合检索。 混合检索的核心是，综合文档 
 在不同检索算法下的排序名次（rank），为其生成最终排序。 一个最常用的算法叫 Reciprocal Rank Fusion（RRF）.

#### 3.3.3 PDF中表格的处理
1. 将每页PDF转成图片
2. 识别文档(图片)中的表格
3. 基于GPT-4 Vision API做表格文档
4. 用GPT-4 Vision生成表格（图像）描述，并向量化用于检索