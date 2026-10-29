# 客服知识库问答助手

基于 LangChain、Milvus 和大模型 API 的 RAG 课程实践项目。通过检索本地客服知识库，为退款、套餐等业务问题提供参考回答。

## 实现流程

知识库文档 → 文本切分 → 向量化 → Milvus 存储 → 问题向量化与检索 → 组装上下文 → 大模型生成回答。

## 主要功能

- 使用递归文本切分器处理知识库，设置分块大小和重叠长度。
- 封装千问嵌入模型，提供 `embed_query` 和 `embed_documents` 接口，生成 2560 维向量。
- 使用 Milvus 存储文本、向量和来源信息，通过 COSINE 相似度检索相关片段。
- 接入 DeepSeek，根据检索上下文回答问题，并设置资料不足时的回答规则。
- 展示命中片段、来源和相似度，辅助检查检索效果。

## 技术栈

Python、LangChain、Milvus、DashScope、DeepSeek。

## 项目文件

- `assistant_rag.ipynb`：数据准备、检索和问答流程。
- `knowledge.txt`：课程示例知识库。
- `requirements.txt`：Python 依赖及版本。
- `.env.example`：环境变量配置示例。
- `.gitignore`：本地配置与缓存的忽略规则。

## 运行方法

1. 准备 Python 3.13 环境，安装依赖：

   ```bash
   python -m pip install -r requirements.txt
   ```

2. 启动 Milvus，确保 Notebook 中配置的服务地址可连接，默认地址为 `http://localhost:19530`。

3. 复制 `.env.example` 为 `.env`，填写模型 API Key 和服务地址。模型名称需与使用的 API 服务一致。

4. 使用支持 Jupyter Notebook 的编辑器打开 `assistant_rag.ipynb`，选择上述 Python 环境，从上到下运行代码单元格。

5. 修改末尾的测试问题，查看检索片段和最终回答。

## 说明

- 本项目为课程学习实践，使用示例知识库。
- 初始化单元格会删除并重建 `rag_tutorial` 数据库中的 `docs` 集合，运行前请确认该集合仅用于本项目练习。
- 本地 `.env` 不应提交；公开配置示例中仅保留占位内容。