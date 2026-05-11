---
layout: post
title: "AI 엔지니어 필수 도구 정리: 2026년 추천 스택"
date: 2026-05-03
categories: [tools-and-tips]
tags: [Tools, AI Stack, Development, Productivity]
excerpt: "실제로 사용하고 있는 AI 개발 필수 도구들과 팁을 정리했습니다."
---

## 🛠️ AI 개발 도구 스택

매일 사용하는 도구들을 카테고리별로 정리했습니다.

## 1️⃣ IDE & 편집기

### VS Code (필수)
```
장점:
- 확장 프로그램 풍부
- 원격 개발 쉬움
- Git 통합 우수

추천 확장:
- Pylance (Python 코드 분석)
- Jupyter (노트북 통합)
- Remote - SSH (원격 서버)
- Better Comments (주석 하이라이트)
```

### PyCharm Professional
```
추천 이유:
- Python 최고의 IDE
- 강력한 디버거
- 리팩토링 기능

단점: 유료
```

## 2️⃣ 프레임워크 & 라이브러리

### 추천 구성

```python
# 핵심
torch >= 2.0
transformers >= 4.30.0
langchain >= 0.1.0

# 데이터 처리
pandas >= 2.0
numpy >= 1.24
polars >= 0.19  # 최근 핫함

# 평가 & 모니터링
wandb  # 실험 추적
ragas  # RAG 평가
deepeval  # 자동 평가

# 유틸리티
python-dotenv  # 환경 변수
pydantic  # 데이터 검증
loguru  # 로깅
```

### 버전 고정하기

```bash
# requirements.txt
torch==2.0.1
transformers==4.30.2
```

**팁**: 항상 버전을 고정하세요! (재현성)

## 3️⃣ 모델 호스팅 & API

### OpenAI API
```python
from openai import OpenAI

client = OpenAI(api_key="sk-...")
response = client.chat.completions.create(
    model="gpt-4",
    messages=[...]
)
```

**팁**: `OPENAI_API_KEY` 환경 변수 설정

### Anthropic (Claude)
```python
from anthropic import Anthropic

client = Anthropic()
message = client.messages.create(
    model="claude-3-opus-20240229",
    max_tokens=1024,
    messages=[...]
)
```

### Hugging Face
```python
from huggingface_hub import login
login(token="hf_...")

# 또는 ~/.huggingface/token 파일에 저장
```

## 4️⃣ 데이터베이스 & 벡터 스토어

### 추천 조합

| 용도 | 도구 | 이유 |
|-----|------|------|
| 벡터 검색 | Pinecone | 관리형, 쉬움 |
| 로컬 벡터 | FAISS | 빠르고 경량 |
| 하이브리드 | Weaviate | 유연함 |
| 메타데이터 | PostgreSQL | 안정적 |

### 로컬 개발 설정

```bash
# Docker로 PostgreSQL + pgvector 실행
docker run --name postgres \
  -e POSTGRES_PASSWORD=password \
  -p 5432:5432 \
  pgvector/pgvector:pg15
```

## 5️⃣ 모니터링 & 로깅

### Weights & Biases (강력 추천)

```python
import wandb

wandb.init(project="my-ai-project", name="exp-1")

for epoch in range(10):
    loss = train()
    wandb.log({"loss": loss, "epoch": epoch})
    
wandb.finish()
```

**장점**:
- 실험 자동 추적
- 모델 비교
- 대시보드
- 공유 가능

### 로깅 라이브러리

```python
from loguru import logger

logger.add("logs/{time}.log")
logger.info("학습 시작")
logger.debug("디버그 정보")
logger.error("에러 발생")
```

## 6️⃣ 배포 & 서빙

### FastAPI (추천)

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Query(BaseModel):
    text: str

@app.post("/predict")
async def predict(query: Query):
    result = model.generate(query.text)
    return {"result": result}

# 실행: uvicorn main:app --reload
```

### Streamlit (프로토타입)

```python
import streamlit as st

st.title("AI 앱")
user_input = st.text_input("입력:")

if user_input:
    output = model.predict(user_input)
    st.write(output)
```

### Docker

```dockerfile
FROM python:3.10

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
CMD ["uvicorn", "main:app", "--host", "0.0.0.0"]
```

## 7️⃣ 생산성 도구

### Jupyter Lab (필수)

```bash
# 설치
pip install jupyterlab

# 실행
jupyter lab

# 팁: Dark 테마 설정
# Settings → Themes → Dark
```

### DVC (Data Version Control)

```bash
# 데이터 버전 관리
dvc add data.csv
dvc push  # 원격 저장소에 저장

# 특정 버전으로 복원
git checkout v1.0
dvc checkout
```

### Make (자동화)

```makefile
install:
	pip install -r requirements.txt

train:
	python train.py

evaluate:
	python evaluate.py

deploy:
	docker build -t my-ai-app .
	docker push my-registry/my-ai-app
```

```bash
make install
make train
```

## 8️⃣ 편리한 팁들

### 환경 변수 관리

```python
# .env 파일
OPENAI_API_KEY=sk-...
HUGGINGFACE_TOKEN=hf_...
MODEL_NAME=gpt-4

# Python에서 사용
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv("OPENAI_API_KEY")
```

### 성능 측정

```python
import time

start = time.time()
result = model.predict(input_data)
elapsed = time.time() - start

print(f"처리 시간: {elapsed:.2f}초")
```

### 메모리 모니터링

```python
import psutil
import torch

process = psutil.Process()
mem_info = process.memory_info()

print(f"RAM: {mem_info.rss / 1024**3:.2f} GB")
print(f"GPU: {torch.cuda.memory_allocated() / 1e9:.2f} GB")
```

## 📋 완벽한 셋업 체크리스트

```
□ Python 3.10+ 설치
□ Virtual environment 생성
□ Git & GitHub 설정
□ 주요 라이브러리 설치
□ IDE 설정 (VS Code)
□ API 키 환경변수 등록
□ Wandb 연결
□ Docker 설치
□ Git pre-commit hooks 설정
```

---

**당신의 필수 도구는 뭔가요?**  
댓글로 공유해주세요! 🚀

**다음 글**: "효율적인 개발을 위한 Git 워크플로우"
