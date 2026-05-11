---
layout: post
title: "LangChain vs LlamaIndex: 어떤 걸 써야 할까?"
date: 2026-04-25
categories: [ai-development]
tags: [LangChain, LlamaIndex, RAG, LLM Framework, 비교]
excerpt: "LangChain과 LlamaIndex를 실제 사용 경험 기반으로 비교합니다."
---

## 시작하며

RAG 시스템을 처음 구축할 때 가장 많이 하는 질문 중 하나:

> "LangChain 써요? LlamaIndex 써요?"

둘 다 써본 경험을 바탕으로 솔직하게 비교해드리겠습니다.

---

## 🔵 LangChain 소개

**목적**: LLM 기반 애플리케이션의 **체인/파이프라인** 구성

```python
from langchain import OpenAI
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain

llm = OpenAI(temperature=0.7)
prompt = PromptTemplate(
    input_variables=["product"],
    template="{product}의 장점 5가지를 알려줘"
)

chain = LLMChain(llm=llm, prompt=prompt)
result = chain.run("아이폰")
```

### LangChain의 강점

| 항목 | 설명 |
|-----|------|
| 생태계 | 가장 큰 커뮤니티, 예제 풍부 |
| 유연성 | 거의 모든 LLM/도구 연결 가능 |
| 에이전트 | LangGraph로 복잡한 에이전트 구현 |
| 통합 | 100+ 외부 도구 기본 지원 |

---

## 🟠 LlamaIndex 소개

**목적**: 데이터를 LLM에게 효율적으로 제공하는 **인덱싱/검색**

```python
from llama_index import VectorStoreIndex, SimpleDirectoryReader

# 문서 로드 및 인덱싱
documents = SimpleDirectoryReader("data/").load_data()
index = VectorStoreIndex.from_documents(documents)

# 쿼리
query_engine = index.as_query_engine()
response = query_engine.query("문서의 핵심 내용은?")
```

### LlamaIndex의 강점

| 항목 | 설명 |
|-----|------|
| RAG 특화 | 검색/인덱싱에 최적화 |
| 데이터 처리 | 다양한 파일 형식 자동 처리 |
| 구조화된 데이터 | SQL, 그래프 등 지원 |
| 평가 도구 | 내장 RAG 평가 기능 |

---

## ⚖️ 직접 비교

### 1. 코드 양

```python
# LangChain - 동일 RAG 구현
from langchain.document_loaders import DirectoryLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain.embeddings import OpenAIEmbeddings
from langchain.vectorstores import FAISS
from langchain.chains import RetrievalQA
from langchain.llms import OpenAI

loader = DirectoryLoader("data/")
documents = loader.load()
text_splitter = RecursiveCharacterTextSplitter(chunk_size=1000)
chunks = text_splitter.split_documents(documents)
embeddings = OpenAIEmbeddings()
vectorstore = FAISS.from_documents(chunks, embeddings)
retriever = vectorstore.as_retriever()
qa = RetrievalQA.from_chain_type(llm=OpenAI(), retriever=retriever)
response = qa.run("질문")
# 약 12줄

# LlamaIndex - 동일 RAG 구현
from llama_index import VectorStoreIndex, SimpleDirectoryReader

documents = SimpleDirectoryReader("data/").load_data()
index = VectorStoreIndex.from_documents(documents)
response = index.as_query_engine().query("질문")
# 약 4줄 ← 훨씬 간단
```

### 2. 유연성

```python
# LangChain: 에이전트 + 여러 도구 조합
from langchain.agents import initialize_agent, Tool
from langchain.tools import DuckDuckGoSearchRun

tools = [
    Tool(name="Search", func=DuckDuckGoSearchRun().run),
    Tool(name="Calculator", func=lambda x: eval(x)),
    # 커스텀 도구 추가 가능
]
agent = initialize_agent(tools, llm, agent_type="zero-shot-react-description")

# LlamaIndex: 이런 커스텀 에이전트 구현이 더 복잡함
```

### 3. RAG 품질

```python
# LlamaIndex의 고급 RAG 기능들
from llama_index.retrievers import BM25Retriever
from llama_index.postprocessor import SentenceTransformerRerank

# 하이브리드 검색 (벡터 + BM25)
retriever = index.as_retriever(
    retriever_mode="hybrid",
    alpha=0.5  # 벡터:BM25 비율
)

# Reranking으로 검색 품질 향상
reranker = SentenceTransformerRerank(top_n=3)
```

---

## 🎯 언제 뭘 쓸까?

```
LangChain을 선택하세요, 만약:
✅ 복잡한 에이전트 시스템 구축
✅ 여러 외부 도구/API 연동
✅ 유연한 파이프라인 필요
✅ 큰 커뮤니티/레퍼런스 필요

LlamaIndex를 선택하세요, 만약:
✅ RAG에 집중
✅ 문서 검색 품질이 중요
✅ 빠른 프로토타이핑
✅ 데이터 파이프라인 구축
```

---

## 🏆 솔직한 결론

저는 **상황에 따라 둘 다 씁니다**.

| 프로젝트 | 선택 | 이유 |
|---------|------|-----|
| 고객 지원 챗봇 | LangChain | 다양한 도구 연동 필요 |
| 문서 Q&A 시스템 | LlamaIndex | RAG 품질이 핵심 |
| 복잡한 AI 에이전트 | LangChain + LangGraph | 상태 관리, 다중 에이전트 |
| 빠른 PoC | LlamaIndex | 코드 양이 적음 |

**초보자라면**: LlamaIndex 먼저  
**에이전트 구축한다면**: LangChain (LangGraph)  
**RAG가 중요하다면**: LlamaIndex  
**모르겠다면**: 둘 다 해보고 판단 😄

---

**다음 글**: LangGraph로 복잡한 AI 에이전트 만들기  
**관련 글**: [RAG 시스템 완벽 가이드](/yeongsin.github.io/ai-development/2026/05/10/rag-system-guide/)
