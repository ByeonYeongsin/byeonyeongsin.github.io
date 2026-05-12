---
title: "CUDA Out of Memory? 이 8가지 방법을 시도해보세요"
date: 2026-05-06 09:00:00 +0900
categories: [Vibe Coding, Debugging]
tags: [cuda, gpu, debugging, pytorch, oom]
---

## 😱 CUDA Out of Memory 에러

이 에러는 AI 개발자라면 누구나 겪는 악몽입니다.

```
RuntimeError: CUDA out of memory.
Tried to allocate X.XX GiB (GPU 0; Y.YY GiB total capacity;
Z.ZZ GiB already allocated
```

## ✅ 실제로 도움된 8가지 방법

### 1️⃣ 배치 사이즈 줄이기

```python
batch_size = 64  # → 8 또는 그 이하
```

**효과**: ⭐⭐⭐⭐⭐

### 2️⃣ Gradient Accumulation

```python
accumulation_steps = 4
for i, batch in enumerate(dataloader):
    loss = criterion(model(batch), batch["labels"])
    (loss / accumulation_steps).backward()
    if (i + 1) % accumulation_steps == 0:
        optimizer.step()
        optimizer.zero_grad()
```

**효과**: ⭐⭐⭐⭐

### 3️⃣ Mixed Precision (FP16)

```python
from torch.cuda.amp import autocast, GradScaler

scaler = GradScaler()
with autocast():
    loss = criterion(model(batch), batch["labels"])
scaler.scale(loss).backward()
scaler.step(optimizer)
scaler.update()
```

**효과**: ⭐⭐⭐⭐ (메모리 40~50% 감소)

### 4️⃣ QLoRA

```python
from peft import LoraConfig, get_peft_model

model = get_peft_model(base_model, LoraConfig(r=8, lora_alpha=16))
```

**효과**: ⭐⭐⭐⭐⭐ (메모리 75% 감소!)

### 5️⃣ Gradient Checkpointing

```python
model.gradient_checkpointing_enable()
```

**효과**: ⭐⭐⭐

### 6️⃣ 캐시 비우기

```python
import torch
del unused_tensor
torch.cuda.empty_cache()
```

**효과**: ⭐⭐

### 7️⃣ 배치별 GPU 전송

```python
# ❌ 전체를 GPU로
data = dataset.to(device)

# ✅ 배치마다
for batch in dataloader:
    batch = {k: v.to(device) for k, v in batch.items()}
```

**효과**: ⭐⭐⭐

### 8️⃣ 메모리 모니터링

```python
print(f"할당: {torch.cuda.memory_allocated()/1e9:.2f} GB")
print(f"예약: {torch.cuda.memory_reserved()/1e9:.2f} GB")
```

## 🎯 추천 순서

```
배치 사이즈 줄이기
  → Mixed Precision 켜기
  → Gradient Accumulation
  → QLoRA 적용   ← 대부분 여기서 해결됨!
  → Gradient Checkpointing
  → 더 작은 모델 고려
```

> **결론**: QLoRA는 진짜 마법입니다 🪄  
> 13B 모델을 RTX 4090 없이 8GB GPU에서 돌릴 수 있게 해줍니다.
