---
title: "AI 엔지니어를 위한 Docker 핵심 가이드"
date: 2026-04-05 09:00:00 +0900
categories: [Development, DevOps]
tags: [docker, devops, deployment, python, container]
---

## AI 개발자에게 Docker가 필요한 이유

```
"내 컴퓨터에서는 되는데요..."
```

이 말을 없애주는 게 Docker입니다.

## 핵심 개념

```
이미지 (Image): 설계도 (불변)
컨테이너 (Container): 이미지로 실행된 인스턴스 (동작)
레지스트리 (Registry): 이미지 저장소 (Docker Hub, ECR)
```

## ML 프로젝트용 Dockerfile

```dockerfile
# ===== GPU 지원 이미지 =====
FROM nvidia/cuda:12.1-cudnn8-runtime-ubuntu22.04

# Python 설치
RUN apt-get update && apt-get install -y python3.11 python3-pip && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

# 의존성 먼저 (캐시 최적화)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 소스 코드
COPY . .

EXPOSE 8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

## .dockerignore (필수!)

```
# .dockerignore
__pycache__/
*.pyc
.env              ← API 키 절대 포함 금지!
*.pth             ← 모델 파일 (크면 제외)
data/raw/         ← 대용량 데이터
.git/
notebooks/
tests/
```

## GPU 컨테이너 실행

```bash
# GPU 사용
docker run --gpus all \
  -v $(pwd)/models:/app/models \
  -p 8000:8000 \
  my-llm-app

# 특정 GPU만 사용
docker run --gpus '"device=0"' my-llm-app
```

## docker-compose로 전체 스택 관리

```yaml
services:
  api:
    build: .
    ports:
      - "8000:8000"
    environment:
      - OPENAI_API_KEY=${OPENAI_API_KEY}
    depends_on:
      - redis
      - postgres
    deploy:
      resources:
        reservations:
          devices:
            - capabilities: [gpu]

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"

  postgres:
    image: pgvector/pgvector:pg16
    environment:
      POSTGRES_PASSWORD: ${DB_PASSWORD}
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```

```bash
docker compose up -d      # 백그라운드 실행
docker compose logs -f    # 로그 확인
docker compose down       # 종료
```

## 이미지 크기 줄이기

```dockerfile
# ❌ 큰 이미지 (2GB+)
FROM python:3.11

# ✅ 작은 이미지 (500MB)
FROM python:3.11-slim

# 멀티스테이지 빌드
FROM python:3.11-slim AS builder
RUN pip install --user -r requirements.txt

FROM python:3.11-slim
COPY --from=builder /root/.local /root/.local
COPY . .
```

## 자주 쓰는 명령어

```bash
# 빌드
docker build -t my-app:v1 .

# 실행
docker run -d --name my-app -p 8000:8000 my-app:v1

# 컨테이너 내부 접속
docker exec -it my-app bash

# 로그
docker logs -f my-app

# 리소스 사용량
docker stats my-app

# 정리
docker system prune -af  # 사용 안 하는 것 모두 삭제
```

> **핵심**: `requirements.txt`를 먼저 복사하고, 소스 코드를 나중에 복사하면 Docker 레이어 캐시를 최대한 활용할 수 있습니다.
