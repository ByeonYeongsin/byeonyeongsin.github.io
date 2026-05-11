---
layout: post
title: "어텐션 메커니즘 완벽 이해하기: Transformer의 핵심"
date: 2026-05-08
categories: [ai-study]
tags: [Attention, Transformer, NLP, Deep Learning]
excerpt: "Transformer의 핵심인 어텐션 메커니즘을 수식과 코드로 완벽하게 이해해봅시다."
---

## 어텐션이란?

어텐션 메커니즘은 모델이 입력 시퀀스의 어느 부분에 집중해야 하는지를 학습하는 기법입니다.

### 핵심 아이디어

"모든 단어가 동일하게 중요한 것은 아니다"

예를 들어:
- "은행(bank)에 돈을 입금했다" → "은행"이 금융기관
- "강(river)의 언덕(bank)에 앉았다" → "은행"이 강둑

같은 단어도 맥락에 따라 의미가 다릅니다. 어텐션은 이를 인식합니다.

## Self-Attention의 3가지 요소

### 1. Query (Q), Key (K), Value (V)

```python
import torch
import torch.nn as nn

# 입력 시퀀스: (batch_size, seq_length, d_model)
x = torch.randn(2, 10, 512)

# 가중치 행렬
W_q = nn.Linear(512, 512)
W_k = nn.Linear(512, 512)
W_v = nn.Linear(512, 512)

# Q, K, V 계산
Q = W_q(x)  # Query
K = W_k(x)  # Key
V = W_v(x)  # Value
```

### 2. 유사도 계산 (Scaled Dot-Product)

```python
# 유사도 점수 계산
d_k = 512
scores = torch.matmul(Q, K.transpose(-2, -1)) / math.sqrt(d_k)
# Shape: (batch_size, seq_length, seq_length)
```

### 3. 주의 가중치 (Softmax)

```python
attention_weights = torch.softmax(scores, dim=-1)
# 각 위치의 가중치 합 = 1
```

### 4. 가중합 (Weighted Sum)

```python
output = torch.matmul(attention_weights, V)
# Shape: (batch_size, seq_length, d_model)
```

## 수식으로 표현

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

## Multi-Head Attention

여러 개의 어텐션을 병렬로 실행:

```python
class MultiHeadAttention(nn.Module):
    def __init__(self, d_model=512, num_heads=8):
        super().__init__()
        self.d_model = d_model
        self.num_heads = num_heads
        self.d_k = d_model // num_heads
        
        self.W_q = nn.Linear(d_model, d_model)
        self.W_k = nn.Linear(d_model, d_model)
        self.W_v = nn.Linear(d_model, d_model)
        self.W_o = nn.Linear(d_model, d_model)
    
    def forward(self, Q, K, V):
        batch_size = Q.shape[0]
        
        # 8개의 헤드로 분할
        Q = self.W_q(Q).view(batch_size, -1, self.num_heads, self.d_k).transpose(1, 2)
        K = self.W_k(K).view(batch_size, -1, self.num_heads, self.d_k).transpose(1, 2)
        V = self.W_v(V).view(batch_size, -1, self.num_heads, self.d_k).transpose(1, 2)
        
        # 각 헤드에서 어텐션 계산
        scores = torch.matmul(Q, K.transpose(-2, -1)) / math.sqrt(self.d_k)
        attention_weights = torch.softmax(scores, dim=-1)
        context = torch.matmul(attention_weights, V)
        
        # 다시 결합
        context = context.transpose(1, 2).contiguous()
        context = context.view(batch_size, -1, self.d_model)
        
        return self.W_o(context)
```

## 시각화

```
입력: "강의 언덕"

Attention Weights:
        [강]  [의]  [언덕]
[강]    0.8   0.1   0.1
[의]    0.2   0.6   0.2
[언덕]  0.1   0.2   0.7

→ 각 단어는 자신과 관련된 단어에 더 높은 가중치
```

## 핵심 포인트

✅ **병렬 처리**: RNN과 달리 시퀀스 전체를 한 번에 처리  
✅ **장거리 의존성**: 멀리 떨어진 단어도 직접 비교  
✅ **해석 가능성**: 어텐션 가중치로 모델의 판단 이유 파악  

---

다음 포스트: Transformer의 구조를 자세히 살펴보겠습니다!
