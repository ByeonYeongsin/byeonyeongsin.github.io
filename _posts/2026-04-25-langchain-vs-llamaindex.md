---
title: "LangChain vs LlamaIndex: 어떤 걸 써야 할까?"
date: 2026-04-25 09:00:00 +0900
categories: [AI Development, Framework]
tags: [langchain, llamaindex, rag, llm, framework]
---

## 시작하며

RAG 시스템을 처음 구축할 때 가장 많이 하는 질문:

> "LangChain 써요? LlamaIndex 써요?"

둘 다 써본 경험을 바탕으로 솔직하게 비교합니다.

## 🔵 LangChain

**목적**: LLM 기반 애플리케이션의 **체인/파이프라인** 구성

```python
from langchain.chains import RetrievalQA
from langchain.llms import OpenAI

qa = RetrievalQA.from_chain_type(
    llm=OpenAI(),
    retriever=vectorstore.as_retriever()
)
response = qa.run("질문")
```

**강점**: 에이전트, 100+ 외부 도구 통합, 큰 커뮤니티

## 🟠 LlamaIndex

**목적**: 데이터를 LLM에게 효율적으로 제공하는 **인덱싱/검색**

```python
from llama_index import VectorStoreIndex, SimpleDirectoryReader

documents = SimpleDirectoryReader("data/").load_data()
index = VectorStoreIndex.from_documents(documents)
response = index.as_query_engine().query("질문")
# 4줄로 끝!
```

**강점**: RAG 특화, 코드 간결, 하이브리드 검색 내장

## ⚖️ 코드량 비교 (동일 RAG 구현)

| | LangChain | LlamaIndex |
|--|---------|-----------|
| 코드 줄 수 | ~12줄 | ~4줄 |
| 유연성 | 매우 높음 | 보통 |
| RAG 품질 | 보통 | 높음 (기본값) |
| 에이전트 | 매우 강함 | 보통 |
| 학습 곡선 | 가파름 | 완만함 |

## 🎯 언제 뭘 쓸까?

```
LangChain ✅
├─ 복잡한 에이전트 시스템
├─ 여러 외부 API 연동
└─ 유연한 파이프라인 필요

LlamaIndex ✅
├─ RAG가 핵심인 프로젝트
├─ 빠른 프로토타이핑
└─ 문서 검색 품질이 중요
```

## 🏆 솔직한 결론

저는 **상황에 따라 둘 다 씁니다**.

| 프로젝트 | 선택 | 이유 |
|---------|------|-----|
| 고객 지원 챗봇 | LangChain | 다양한 도구 연동 |
| 문서 Q&A | LlamaIndex | RAG 품질이 핵심 |
| 복잡한 에이전트 | LangGraph | 상태 관리 필요 |
| 빠른 PoC | LlamaIndex | 코드가 적음 |

> **초보자라면**: LlamaIndex 먼저  
> **에이전트 만든다면**: LangChain  
> **모르겠다면**: 둘 다 해보고 판단 😄
