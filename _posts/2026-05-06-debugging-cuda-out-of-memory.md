---
layout: post
title: "🔥 CUDA Out of Memory? 이 8가지 방법을 시도해보세요"
date: 2026-05-06
categories: [vibing-coding]
tags: [CUDA, GPU, Debugging, PyTorch, Deep Learning]
excerpt: "GPU 메모리 부족으로 고생했던 경험과 실전 해결법을 공유합니다."
---

## 😱 CUDA Out of Memory 에러

이 에러는 AI 개발자라면 누구나 겪는 악몽입니다.

```
RuntimeError: CUDA out of memory. 
Tried to allocate X.XX GiB (GPU 0; Y.YY GiB total capacity; 
Z.ZZ GiB already allocated
```

**몇 주 전 나의 상황:**
- 🖥️ RTX 4090 (24GB) 보유
- 🤖 거대 모델 파인튜닝 시도
- 💥 50줄 코드 짠 후 크래시

---

## ✅ 실제로 도움된 8가지 방법

### 1️⃣ 배치 사이즈 줄이기 (가장 빠른 방법)

```python
# ❌ Before
batch_size = 64

# ✅ After  
batch_size = 8  # 또는 그 이하

# 2배 메모리 절감의 법칙
# 배치를 절반으로 → 메모리 거의 절반
```

**효과**: ⭐⭐⭐⭐⭐ (90% 경우 해결)

### 2️⃣ Gradient Accumulation

```python
# 작은 배치를 여러 번 누적해서 큰 배치와 같은 효과
accumulation_steps = 4
batch_size = 8  # 실제: 32와 비슷한 그래디언트

for i, batch in enumerate(dataloader):
    outputs = model(batch)
    loss = criterion(outputs, batch['labels'])
    loss.backward()
    
    if (i + 1) % accumulation_steps == 0:
        optimizer.step()
        optimizer.zero_grad()
```

**효과**: ⭐⭐⭐⭐ (배치를 크게 할 수 없을 때 필수)

### 3️⃣ Mixed Precision (자동 혼합 정밀도)

```python
from torch.cuda.amp import autocast, GradScaler

scaler = GradScaler()

for batch in dataloader:
    with autocast():  # FP16으로 계산
        outputs = model(batch)
        loss = criterion(outputs, batch['labels'])
    
    scaler.scale(loss).backward()
    scaler.step(optimizer)
    scaler.update()
```

**효과**: ⭐⭐⭐⭐ (메모리 40~50% 감소)

### 4️⃣ QLoRA (Quantized LoRA)

```python
from peft import LoraConfig, get_peft_model
from bitsandbytes.nn import Linear4bit

# 4비트 양자화
lora_config = LoraConfig(
    r=8,
    lora_alpha=16,
    target_modules=["q_proj", "v_proj"]
)

model = get_peft_model(model, lora_config)
```

**효과**: ⭐⭐⭐⭐⭐ (메모리 75% 감소!)

### 5️⃣ Gradient Checkpointing

```python
from torch.utils.checkpoint import checkpoint

class ModelWithCheckpoint(nn.Module):
    def forward(self, x):
        return checkpoint(self.heavy_layer, x, use_reentrant=False)
```

**효과**: ⭐⭐⭐ (메모리 30% 감소, 속도 약간 저하)

### 6️⃣ 메모리 캐시 비우기

```python
import torch

# 사용 후 바로
del variable_name
torch.cuda.empty_cache()

# 모든 GPU 메모리 초기화
torch.cuda.reset_peak_memory_stats()
```

**효과**: ⭐⭐ (임시방편, 근본적 해결 아님)

### 7️⃣ 데이터 로드 최적화

```python
# ❌ 나쁜 방법: 모든 데이터를 GPU로
data = data.to(device)

# ✅ 좋은 방법: 배치별로 옮기기
for batch in dataloader:
    batch = {k: v.to(device) for k, v in batch.items()}
    # 처리
```

**효과**: ⭐⭐⭐

### 8️⃣ 모니터링과 디버깅

```python
# GPU 메모리 사용량 실시간 모니터
import torch

print(f"할당됨: {torch.cuda.memory_allocated() / 1e9:.2f} GB")
print(f"예약됨: {torch.cuda.memory_reserved() / 1e9:.2f} GB")
print(f"캐시됨: {torch.cuda.memory_cached() / 1e9:.2f} GB")

# 상세 디버깅
torch.cuda.memory._dump_snapshot("memory_snapshot.pkl")
```

**효과**: ⭐⭐⭐ (원인 파악)

---

## 🎯 추천 조합 (우선순위)

### 빠르게 시도하기
1. 배치 사이즈 줄이기
2. Mixed Precision 활성화
3. Gradient Accumulation

### 여전히 부족하면
4. QLoRA 적용
5. Gradient Checkpointing
6. 데이터 로드 최적화

### 마지막 수단
- 더 작은 모델 사용
- 멀티 GPU 사용
- 더 큰 GPU 구매 😅

---

## 😂 개인적 경험

**문제**: 13B 모델을 RTX 4090에서 파인튜닝 불가능  

**시도 순서**:
```
배치 사이즈 줄이기 (실패)
  ↓
Mixed Precision (조금 도움)
  ↓
Gradient Accumulation (더 도움)
  ↓
QLoRA (성공! 이제 8GB로도 가능)
```

**결론**: QLoRA는 진짜 마법입니다. 🪄

---

혹시 다른 방법으로 해결한 경험이 있으신가요? 댓글로 공유해주세요!

다음 글: "왜 모델은 NaN을 뱉을까?"
