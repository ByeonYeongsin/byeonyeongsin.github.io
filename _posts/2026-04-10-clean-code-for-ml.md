---
title: "ML 프로젝트를 위한 클린 코드 원칙"
date: 2026-04-10 09:00:00 +0900
categories: [Development, Software Engineering]
tags: [clean-code, python, ml, software-engineering, refactoring]
---

## ML 코드가 지저분해지는 이유

노트북에서 시작한 코드가 프로덕션에 가면 이렇게 됩니다:

```python
# 실제로 본 ML 코드 (익명 처리)
def f(x, y, z, a=0.1, b=True):
    # TODO: 나중에 정리
    temp = []
    for i in range(len(x)):
        if b:
            temp.append(x[i] * a + y[i])
        else:
            temp.append(x[i] + y[i] * z)
    return temp  # 이게 뭘 리턴하는 거지?
```

이런 코드는 2주 후 본인도 이해 못 합니다.

---

## 원칙 1: 의도를 드러내는 이름

```python
# ❌ 나쁜 예
def f(x, e=10, lr=0.001):
    for i in range(e):
        ...

# ✅ 좋은 예
def train_model(
    training_data: Dataset,
    num_epochs: int = 10,
    learning_rate: float = 0.001
) -> TrainedModel:
    for epoch in range(num_epochs):
        ...
```

## 원칙 2: 단일 책임 원칙 (SRP)

```python
# ❌ 모든 걸 하는 함수
def process(data):
    # 전처리
    data = data.dropna()
    data = (data - data.mean()) / data.std()
    # 학습
    model = RandomForest()
    model.fit(data)
    # 평가 + 저장 + 로깅...

# ✅ 책임 분리
def preprocess(raw_data: pd.DataFrame) -> pd.DataFrame:
    return raw_data.dropna().pipe(normalize)

def train(data: pd.DataFrame) -> Model:
    model = RandomForest()
    return model.fit(data)

def evaluate(model: Model, test_data: pd.DataFrame) -> Metrics:
    predictions = model.predict(test_data)
    return compute_metrics(predictions, test_data.labels)
```

## 원칙 3: 설정을 코드에서 분리

```python
# ❌ 하드코딩
model = BertModel.from_pretrained("bert-base-uncased")
optimizer = Adam(lr=0.00003, weight_decay=0.01)
trainer.train(epochs=3, batch_size=32)

# ✅ 설정 파일 활용
from dataclasses import dataclass

@dataclass
class TrainingConfig:
    model_name: str = "bert-base-uncased"
    learning_rate: float = 3e-5
    weight_decay: float = 0.01
    num_epochs: int = 3
    batch_size: int = 32

config = TrainingConfig()
model = BertModel.from_pretrained(config.model_name)
```

## 원칙 4: 불변성 선호

```python
# ❌ 원본 데이터 변경
def add_features(df):
    df["new_col"] = df["a"] + df["b"]  # 원본 수정!
    return df

# ✅ 새 객체 반환
def add_features(df: pd.DataFrame) -> pd.DataFrame:
    return df.assign(new_col=df["a"] + df["b"])  # 원본 유지
```

## 원칙 5: 재현 가능성 보장

```python
import random
import numpy as np
import torch

def set_seed(seed: int = 42) -> None:
    """모든 랜덤 시드를 고정해서 재현 가능한 실험을 보장합니다."""
    random.seed(seed)
    np.random.seed(seed)
    torch.manual_seed(seed)
    torch.cuda.manual_seed_all(seed)

# 항상 실험 시작 시 호출
set_seed(42)
```

## 원칙 6: 타입 힌팅 + 문서화

```python
from typing import Optional
import torch

def compute_embeddings(
    texts: list[str],
    model: torch.nn.Module,
    batch_size: int = 32,
    normalize: bool = True
) -> torch.Tensor:
    """
    텍스트 리스트를 임베딩 벡터로 변환합니다.

    Args:
        texts: 임베딩할 텍스트 리스트
        model: 임베딩 모델 (SentenceTransformer 등)
        batch_size: 배치 크기 (메모리에 따라 조정)
        normalize: L2 정규화 여부

    Returns:
        shape (len(texts), embedding_dim)의 텐서
    """
    embeddings = []
    for i in range(0, len(texts), batch_size):
        batch = texts[i:i + batch_size]
        with torch.no_grad():
            batch_emb = model.encode(batch)
        embeddings.append(batch_emb)

    result = torch.cat(embeddings)
    if normalize:
        result = torch.nn.functional.normalize(result, p=2, dim=1)
    return result
```

## ML 프로젝트 구조 템플릿

```
my-ml-project/
├── data/
│   ├── raw/           # 원본 데이터 (절대 수정 금지)
│   └── processed/     # 전처리된 데이터
├── src/
│   ├── data/          # 데이터 로딩/전처리
│   ├── models/        # 모델 정의
│   ├── training/      # 학습 루프
│   └── evaluation/    # 평가 코드
├── notebooks/         # 탐색용 노트북 (실험적)
├── tests/             # 단위 테스트
├── configs/           # 설정 파일
├── scripts/           # 실행 스크립트
└── requirements.txt
```

## 핵심 요약

| 나쁜 습관 | 좋은 습관 |
|---------|---------|
| 모호한 변수명 (`x`, `tmp`) | 의미 있는 이름 |
| 하나의 긴 함수 | 단일 책임 함수 |
| 하드코딩된 설정값 | 설정 파일/dataclass |
| 원본 데이터 수정 | 불변 변환 |
| 랜덤 시드 없음 | `set_seed()` 고정 |
| 타입 없는 함수 | 타입 힌팅 + 문서화 |

> "코드는 한 번 쓰고 열 번 읽는다." - 읽기 좋은 코드가 최고입니다.
