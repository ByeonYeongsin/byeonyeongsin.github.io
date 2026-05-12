---
title: "AI 엔지니어 필수 도구 정리: 2026년 추천 스택"
date: 2026-05-03 09:00:00 +0900
categories: [Tools & Tips, Productivity]
tags: [tools, ai-stack, development, productivity, vscode]
---

## 🛠️ AI 개발 도구 스택 (2026년 기준)

매일 사용하는 도구들을 카테고리별로 정리했습니다.

## 1️⃣ IDE & 편집기

**VS Code** (메인)
```
추천 확장:
- Pylance         (Python 정적 분석)
- Jupyter         (노트북 통합)
- Remote - SSH    (원격 서버 개발)
- GitLens         (Git 시각화)
- Better Comments (주석 하이라이트)
```

## 2️⃣ AI/ML 프레임워크 추천 조합

```python
# 핵심 스택
torch >= 2.0
transformers >= 4.40
langchain >= 0.2
pydantic >= 2.0

# 데이터 처리
pandas >= 2.0
polars >= 0.20       # 빠른 DataFrame

# 실험 관리
wandb               # 실험 추적
ragas               # RAG 평가
deepeval            # LLM 자동 평가
```

## 3️⃣ 모델 호스팅 & API

```python
# OpenAI
from openai import OpenAI
client = OpenAI()

# Anthropic (Claude)
from anthropic import Anthropic
client = Anthropic()

# HuggingFace (오픈소스)
from transformers import pipeline
pipe = pipeline("text-generation", model="meta-llama/Llama-3-8B")
```

## 4️⃣ 벡터 데이터베이스 추천

| 도구 | 용도 | 특징 |
|-----|------|------|
| **Pinecone** | 프로덕션 | 관리형, 쉬움 |
| **FAISS** | 로컬/리서치 | 빠르고 경량 |
| **Weaviate** | 하이브리드 검색 | 벡터+키워드 |
| **pgvector** | PostgreSQL 통합 | SQL과 함께 |

## 5️⃣ 실험 추적: Weights & Biases

```python
import wandb

wandb.init(project="my-llm-project")

for epoch in range(10):
    loss = train()
    wandb.log({"loss": loss, "epoch": epoch})
```

**Why WandB?** 실험 비교, 하이퍼파라미터 관리, 팀 공유가 한 번에

## 6️⃣ 서빙: FastAPI + Docker

```python
# main.py
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Query(BaseModel):
    text: str

@app.post("/generate")
async def generate(q: Query):
    return {"result": model.predict(q.text)}
```

```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

## 7️⃣ 생산성 팁

```bash
# Makefile로 자동화
make install    # 패키지 설치
make train      # 학습 실행
make evaluate   # 평가
make deploy     # 배포
```

```python
# .env로 API 키 관리
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    openai_api_key: str
    model_name: str = "gpt-4o"

    class Config:
        env_file = ".env"

settings = Settings()
```

## 📋 셋업 체크리스트

```
□ Python 3.11+ 가상환경
□ VS Code + 확장 설치
□ Git 설정
□ .env 파일로 API 키 관리
□ WandB 연결
□ Docker 설치
□ pre-commit hooks 설정
```

> **팁**: 도구를 너무 많이 쓰는 것보다 핵심 도구를 깊이 아는 게 더 중요합니다.

다음 글: **효율적인 개발을 위한 Git 워크플로우**
