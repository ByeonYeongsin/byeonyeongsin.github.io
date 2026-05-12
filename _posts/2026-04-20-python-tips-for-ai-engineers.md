---
title: "AI 엔지니어를 위한 파이썬 꿀팁 10가지"
date: 2026-04-20 09:00:00 +0900
categories: [Tools & Tips, Python]
tags: [python, tips, productivity, clean-code, pydantic]
---

## AI 개발에서 파이썬을 더 잘 쓰는 법

매일 쓰면서 습관이 된 팁들을 모았습니다.

## 1️⃣ dataclass로 설정 관리

```python
# ❌ 딕셔너리: 오타 있어도 에러 없음
config = {"model": "gpt-4", "temperature": 0.7}

# ✅ dataclass: 자동완성 + 타입 안전
from dataclasses import dataclass

@dataclass
class ModelConfig:
    model: str = "gpt-4"
    temperature: float = 0.7
    max_tokens: int = 2048
```

## 2️⃣ Pydantic으로 데이터 검증

```python
from pydantic import BaseModel, field_validator

class ChatRequest(BaseModel):
    message: str
    max_length: int = 500

    @field_validator("max_length")
    def check_length(cls, v):
        if v > 4096:
            raise ValueError("너무 깁니다!")
        return v

ChatRequest(message="안녕", max_length=5000)  # ValidationError!
```

## 3️⃣ functools.cache로 API 비용 절감

```python
from functools import lru_cache

@lru_cache(maxsize=100)
def get_embedding(text: str) -> list:
    """같은 텍스트는 API 호출 안 함"""
    return openai.embeddings.create(input=text).data[0].embedding

# 첫 호출: API 호출 (비용 발생)
emb1 = get_embedding("안녕하세요")

# 두 번째: 캐시 사용 (비용 없음!)
emb2 = get_embedding("안녕하세요")
```

## 4️⃣ contextlib으로 타이머

```python
from contextlib import contextmanager
import time

@contextmanager
def timer(name: str):
    start = time.time()
    yield
    print(f"{name}: {time.time()-start:.2f}초")

with timer("RAG 검색"):
    results = retriever.get_relevant_docs(query)
# → "RAG 검색: 0.43초"
```

## 5️⃣ 제너레이터로 메모리 절약

```python
# ❌ 전체 로드 (RAM 위험)
texts = [line.strip() for line in open("huge.txt")]

# ✅ 스트리밍
def stream_texts(path):
    with open(path, encoding="utf-8") as f:
        for line in f:
            yield line.strip()

for text in stream_texts("huge.txt"):
    embed_and_store(text)
```

## 6️⃣ 비동기로 속도 10배 향상

```python
import asyncio

# ❌ 순차: 10개 × 1초 = 10초
for text in texts:
    result = call_api(text)

# ✅ 비동기: 10개 동시 = ~1초
async def process_all(texts):
    tasks = [call_api_async(text) for text in texts]
    return await asyncio.gather(*tasks)
```

## 7️⃣ Loguru로 로깅

```python
from loguru import logger

logger.add("logs/{time}.log", level="DEBUG")

logger.info("학습 시작")
logger.warning("GPU 메모리 90%")
logger.error("에러!", exc_info=True)

@logger.catch
def risky():
    ...  # 에러 발생 시 자동 로그
```

## 8️⃣ 환경 변수 관리 (pydantic-settings)

```python
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    openai_api_key: str
    model_name: str = "gpt-4o"

    class Config:
        env_file = ".env"

settings = Settings()  # .env 자동 읽기 + 타입 검증!
```

## 9️⃣ 타입 힌팅 적극 활용

```python
from typing import Optional, List

# ❌ 이건 뭘 리턴하는지 모름
def process(data):
    pass

# ✅ 명확함
def process_docs(
    documents: List[str],
    chunk_size: int = 512,
) -> dict[str, List[str]]:
    ...
```

## 🔟 자주 쓰는 한 줄 코드

```python
# 배치로 나누기
def batches(lst, n):
    for i in range(0, len(lst), n): yield lst[i:i+n]

# None 필터링
valid = [x for x in items if x is not None]

# 가장 자주 나오는 값
from collections import Counter
most_common = Counter(labels).most_common(3)

# 딕셔너리 역전
inverted = {v: k for k, v in original.items()}
```

---

> **바로 적용해볼 팁 1순위**: Pydantic 설정 관리 + `lru_cache`  
> 이 두 가지만 써도 코드 품질이 눈에 띄게 좋아집니다!
