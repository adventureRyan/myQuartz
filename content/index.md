---
title: Welcome to MyHome
---
# 事件

## Work

### 组会汇报
周五重新设计了 Milvus 数据库的创建流程，使其根据配置文件自动完成初始化。已实现初步的相关文本召回功能,将项目代码上传到了 github 上.今天的计划是增加一个基于关键词的 BM25 召回方法，并部署 rerank 模型以优化排序效果。
### 计划
- [ ] 加一个 BM25 的召回方法
- [ ] 使用 rerank 模型进行重排
- [ ] 测试下 google 的新项目
## Personal
- [ ] 写下第一篇笔记,关于整个项目的部署



```python
    # 用于构建 BM25 检索器的索引
    def build(self, txt_list: List[str]):
        self.data_list = txt_list
        self.tokenized_corpus = []
        for doc in tqdm(self.data_list, desc="bm25 build "):
            # 对每个文档用 self.tokenize 方法进行分词，并将分词结果加入 tokenized_corpus。
            self.tokenized_corpus.append(self.tokenize(doc))
        # 初始化 BM25Okapi 实例
        self.bm25 = BM25Okapi(self.tokenized_corpus)

    def tokenize(self,  text: str) -> List[str]:
        """ 使用jieba进行中文分词。
        """
        return list(jieba.cut_for_search(text))
```