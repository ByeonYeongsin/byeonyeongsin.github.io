---
title: "어텐션 메커니즘 완벽 이해하기: Transformer의 핵심"
date: 2026-05-08 09:00:00 +0900
categories: [AI Study, Deep Learning]
tags: [attention, transformer, nlp, deep-learning, pytorch]
---

## 어텐션이란?

어텐션 메커니즘은 모델이 입력 시퀀스의 어느 부분에 집중해야 하는지를 학습하는 기법입니다.

### 핵심 아이디어

"모든 단어가 동일하게 중요한 것은 아니다"

예를 들어:
- `"은행(bank)에 돈을 입금했다"` → "은행"이 금융기관
- `"강(river)의 언덕(bank)에 앉았다"` → "은행"이 강둑

같은 단어도 맥락에 따라 의미가 다릅니다. 어텐션은 이를 인식합니다.

## Self-Attention의 3가지 요소

### Query (Q), Key (K), Value (V)

```python
import torch
import torch.nn as nn
import math

x = torch.randn(2, 10, 512)  # (batch, seq_len, d_model)

W_q = nn.Linear(512, 512)
W_k = nn.Linear(512, 512)
W_v = nn.Linear(512, 512)

Q = W_q(x)
K = W_k(x)
V = W_v(x)
```

### Scaled Dot-Product Attention

```python
d_k = 512
scores = torch.matmul(Q, K.transpose(-2, -1)) / math.sqrt(d_k)
attention_weights = torch.softmax(scores, dim=-1)
output = torch.matmul(attention_weights, V)
```

## 수식으로 표현

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

## Multi-Head Attention

```python
class MultiHeadAttention(nn.Module):
    def __init__(self, d_model=512, num_heads=8):
        super().__init__()
        self.num_heads = num_heads
        self.d_k = d_model // num_heads
        self.W_q = nn.Linear(d_model, d_model)
        self.W_k = nn.Linear(d_model, d_model)
        self.W_v = nn.Linear(d_model, d_model)
        self.W_o = nn.Linear(d_model, d_model)

    def forward(self, Q, K, V):
        B = Q.shape[0]
        Q = self.W_q(Q).view(B, -1, self.num_heads, self.d_k).transpose(1, 2)
        K = self.W_k(K).view(B, -1, self.num_heads, self.d_k).transpose(1, 2)
        V = self.W_v(V).view(B, -1, self.num_heads, self.d_k).transpose(1, 2)

        scores = torch.matmul(Q, K.transpose(-2, -1)) / math.sqrt(self.d_k)
        attn = torch.softmax(scores, dim=-1)
        ctx = torch.matmul(attn, V)

        ctx = ctx.transpose(1, 2).contiguous().view(B, -1, self.num_heads * self.d_k)
        return self.W_o(ctx)
```

## 핵심 포인트

| 장점 | 설명 |
|-----|------|
| 병렬 처리 | RNN과 달리 시퀀스 전체를 한 번에 처리 |
| 장거리 의존성 | 멀리 떨어진 단어도 직접 비교 |
| 해석 가능성 | 어텐션 가중치로 모델 판단 이유 파악 |

다음 포스트: **Transformer 아키텍처 전체 구조 분석**
