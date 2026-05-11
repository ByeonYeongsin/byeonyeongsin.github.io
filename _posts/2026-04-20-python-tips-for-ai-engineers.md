---
layout: post
title: "AI 엔지니어를 위한 파이썬 꿀팁 10가지"
date: 2026-04-20
categories: [tools-and-tips]
tags: [Python, Tips, Productivity, Clean Code]
excerpt: "실제로 매일 쓰는 파이썬 꿀팁들을 정리했습니다. 코드가 훨씬 깔끔해집니다."
---

## AI 개발에서 파이썬을 더 잘 쓰는 법

매일 파이썬 코드를 짜면서 습관이 된 팁들을 모았습니다.

---

## 1️⃣ dataclass로 설정 관리

```python
# ❌ 딕셔너리로 하면
config = {
    "model": "gpt-4",
    "temperature": 0.7,
    "max_tokens": 2048
}
# 오타가 있어도 에러 없음. 자동완성도 없음.

# ✅ dataclass로 하면
from dataclasses import dataclass

@dataclass
class ModelConfig:
    model: str = "gpt-4"
    temperature: float = 0.7
    max_tokens: int = 2048

config = ModelConfig(temperature=0.5)
print(config.model)  # 자동완성 됨!
```

---

## 2️⃣ Pydantic으로 데이터 검증

```python
from pydantic import BaseModel, validator

class ChatRequest(BaseModel):
    message: str
    max_length: int = 500

    @validator("max_length")
    def check_length(cls, v):
        if v > 4096:
            raise ValueError("너무 깁니다!")
        return v

# 자동 검증
req = ChatRequest(message="안녕", max_length=5000)
# ValidationError 발생!
```

---

## 3️⃣ 타입 힌팅 적극 활용

```python
from typing import Optional, List, Dict

# ❌ 이건 뭘 리턴하는지 모름
def process(data):
    pass

# ✅ 명확함
def process_documents(
    documents: List[str],
    chunk_size: int = 512,
    overlap: int = 50
) -> Dict[str, List[str]]:
    """문서를 청크로 나눠서 딕셔너리로 반환"""
    result = {}
    for doc in documents:
        chunks = split_text(doc, chunk_size, overlap)
        result[doc[:20]] = chunks
    return result
```

---

## 4️⃣ contextlib으로 리소스 관리

```python
from contextlib import contextmanager
import time

@contextmanager
def timer(name: str):
    start = time.time()
    yield
    elapsed = time.time() - start
    print(f"{name}: {elapsed:.2f}초")

# 사용
with timer("모델 추론"):
    result = model.predict(input_data)
# → "모델 추론: 0.43초"

with timer("임베딩 생성"):
    embeddings = embed(texts)
# → "임베딩 생성: 1.23초"
```

---

## 5️⃣ functools.cache로 캐싱

```python
from functools import lru_cache, cache

# API 호출 비용이 비쌀 때 캐싱
@lru_cache(maxsize=100)
def get_embedding(text: str) -> list:
    """같은 텍스트는 API 호출 안 함"""
    response = openai.embeddings.create(
        model="text-embedding-ada-002",
        input=text
    )
    return response.data[0].embedding

# 첫 호출: API 호출
embedding1 = get_embedding("안녕하세요")

# 두 번째 호출: 캐시에서 가져옴 (비용 없음!)
embedding2 = get_embedding("안녕하세요")
```

---

## 6️⃣ enumerate & zip 제대로 쓰기

```python
documents = ["doc1", "doc2", "doc3"]
embeddings = [[0.1, 0.2], [0.3, 0.4], [0.5, 0.6]]

# ❌ 이런 코드 쓰지 마세요
for i in range(len(documents)):
    doc = documents[i]
    emb = embeddings[i]
    print(f"{i}: {doc} -> {emb}")

# ✅ 이렇게
for i, (doc, emb) in enumerate(zip(documents, embeddings)):
    print(f"{i}: {doc} -> {emb}")
```

---

## 7️⃣ 제너레이터로 메모리 절약

```python
# ❌ 대용량 데이터를 한 번에 로드 (메모리 폭발)
def load_all_texts(file_path):
    return [line.strip() for line in open(file_path)]

texts = load_all_texts("huge_dataset.txt")  # RAM 위험!

# ✅ 제너레이터로 하나씩 처리
def stream_texts(file_path):
    with open(file_path, encoding="utf-8") as f:
        for line in f:
            yield line.strip()

for text in stream_texts("huge_dataset.txt"):
    process(text)  # 메모리 안전!
```

---

## 8️⃣ 로깅 제대로 하기

```python
from loguru import logger
import sys

# 설정 (한 번만)
logger.remove()
logger.add(sys.stdout, level="INFO", colorize=True)
logger.add("logs/{time:YYYY-MM-DD}.log", level="DEBUG", rotation="1 day")

# 사용
logger.info("학습 시작")
logger.debug(f"배치 크기: {batch_size}")
logger.warning("GPU 메모리 90% 사용 중")
logger.error("에러 발생!", exc_info=True)

# 함수 실행 시간 자동 기록
@logger.catch
def risky_function():
    # 에러 발생 시 자동으로 로그에 기록
    ...
```

---

## 9️⃣ 환경 변수 관리

```python
# .env 파일 (절대 git에 올리지 마세요!)
OPENAI_API_KEY=sk-...
MODEL_NAME=gpt-4
DEBUG=false

# config.py
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    openai_api_key: str
    model_name: str = "gpt-4"
    debug: bool = False

    class Config:
        env_file = ".env"

settings = Settings()
# 자동으로 .env 파일 읽음 + 타입 검증!
print(settings.model_name)  # "gpt-4"
```

---

## 🔟 비동기 처리로 속도 향상

```python
import asyncio
import aiohttp

# ❌ 순차 처리: 10초
for text in texts:
    result = call_api(text)  # 각 1초씩

# ✅ 비동기 처리: 1초 (병렬)
async def process_all(texts):
    async with aiohttp.ClientSession() as session:
        tasks = [call_api_async(session, text) for text in texts]
        results = await asyncio.gather(*tasks)
    return results

results = asyncio.run(process_all(texts))
```

---

## 보너스: 자주 쓰는 한 줄 코드

```python
# 리스트 평탄화
flat = [item for sublist in nested_list for item in sublist]

# 딕셔너리 역전
inverted = {v: k for k, v in original.items()}

# None 필터링
valid = list(filter(None, potentially_none_list))

# 가장 자주 나오는 값
from collections import Counter
most_common = Counter(items).most_common(3)

# 배치로 나누기
def batches(lst, n):
    for i in range(0, len(lst), n):
        yield lst[i:i+n]
```

---

이 팁들을 적용하면 코드가 더 읽기 쉽고, 버그도 줄어듭니다!

**가장 바로 적용해볼 팁**: Pydantic 설정 관리 + 타입 힌팅

다음 글: "파이썬 디버깅 마스터하기"
