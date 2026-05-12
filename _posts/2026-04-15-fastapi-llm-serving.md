---
title: "FastAPI로 LLM 서빙하기: 프로덕션 레벨 가이드"
date: 2026-04-15 09:00:00 +0900
categories: [Development, Backend]
tags: [fastapi, llm, serving, python, backend, api]
---

## 왜 FastAPI인가?

LLM 서비스를 만들 때 FastAPI가 최선인 이유:

| 항목 | Flask | FastAPI |
|-----|-------|---------|
| 비동기 지원 | 별도 설정 | **기본 지원** |
| 자동 문서화 | ❌ | **Swagger/ReDoc 자동** |
| 타입 검증 | ❌ | **Pydantic 통합** |
| 성능 | 보통 | **매우 빠름** |

## 기본 구조

```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
from openai import AsyncOpenAI

app = FastAPI(title="LLM API", version="1.0.0")
client = AsyncOpenAI()

class ChatRequest(BaseModel):
    message: str
    model: str = "gpt-4o"
    max_tokens: int = 1000

class ChatResponse(BaseModel):
    response: str
    model: str
    tokens_used: int

@app.post("/chat", response_model=ChatResponse)
async def chat(request: ChatRequest):
    result = await client.chat.completions.create(
        model=request.model,
        messages=[{"role": "user", "content": request.message}],
        max_tokens=request.max_tokens
    )
    return ChatResponse(
        response=result.choices[0].message.content,
        model=result.model,
        tokens_used=result.usage.total_tokens
    )
```

## 스트리밍 응답

LLM의 핵심 기능: 실시간 스트리밍

```python
from fastapi.responses import StreamingResponse
import json

@app.post("/chat/stream")
async def chat_stream(request: ChatRequest):
    async def generate():
        stream = await client.chat.completions.create(
            model=request.model,
            messages=[{"role": "user", "content": request.message}],
            stream=True
        )
        async for chunk in stream:
            delta = chunk.choices[0].delta
            if delta.content:
                yield f"data: {json.dumps({'content': delta.content})}\n\n"
        yield "data: [DONE]\n\n"

    return StreamingResponse(generate(), media_type="text/event-stream")
```

## 미들웨어: 인증 + 로깅

```python
from fastapi import Request
import time
import logging

logger = logging.getLogger(__name__)

@app.middleware("http")
async def log_requests(request: Request, call_next):
    start = time.time()
    response = await call_next(request)
    duration = time.time() - start

    logger.info(
        f"{request.method} {request.url.path} "
        f"- {response.status_code} "
        f"- {duration:.3f}s"
    )
    return response
```

## Rate Limiting

```python
from slowapi import Limiter
from slowapi.util import get_remote_address

limiter = Limiter(key_func=get_remote_address)
app.state.limiter = limiter

@app.post("/chat")
@limiter.limit("10/minute")  # 분당 10회 제한
async def chat(request: Request, body: ChatRequest):
    ...
```

## 에러 핸들링

```python
from fastapi import HTTPException
from openai import APIError, RateLimitError

@app.exception_handler(RateLimitError)
async def rate_limit_handler(request, exc):
    raise HTTPException(status_code=429, detail="API 한도 초과. 잠시 후 다시 시도해주세요.")

@app.exception_handler(APIError)
async def api_error_handler(request, exc):
    raise HTTPException(status_code=502, detail=f"LLM API 오류: {str(exc)}")
```

## Docker로 배포

```dockerfile
FROM python:3.11-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .
EXPOSE 8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--workers", "4"]
```

```yaml
# docker-compose.yml
services:
  api:
    build: .
    ports:
      - "8000:8000"
    environment:
      - OPENAI_API_KEY=${OPENAI_API_KEY}
    restart: unless-stopped
```

## 성능 최적화 체크리스트

```
□ async/await 일관되게 사용
□ 커넥션 풀 설정 (DB, Redis)
□ 응답 캐싱 (동일 쿼리)
□ 적절한 workers 수 설정
□ 헬스체크 엔드포인트 추가
□ 모니터링 연결 (Prometheus)
```

---

다음 글: **LLM API에 캐싱 레이어 추가하기**
