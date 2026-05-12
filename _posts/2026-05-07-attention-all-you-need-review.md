---
title: "논문 리뷰: Attention Is All You Need (Transformer 논문)"
date: 2026-05-07 09:00:00 +0900
categories: [Paper Review, NLP]
tags: [transformer, nlp, deep-learning, paper-review, attention]
---

## 📄 논문 정보

| 항목 | 내용 |
|-----|------|
| **제목** | Attention Is All You Need |
| **저자** | Vaswani et al. (Google Brain) |
| **발표** | 2017년 NeurIPS |
| **인용** | 100,000+회 |

## 🎯 핵심 기여

**RNN 없이 어텐션만으로도 좋은 성능을 낼 수 있다**는 것을 증명했습니다.

1. **Self-Attention**: 시퀀스 내 모든 위치 간의 관계 모델링
2. **병렬 처리**: RNN의 순차 처리 제약 극복
3. **Positional Encoding**: 순서 정보 유지

## 📊 성능

| 모델 | BLEU | 학습 시간 |
|-----|------|---------|
| **Transformer** | **28.4** | **3.5일** |
| 이전 SOTA | 27.3 | 12일+ |

## 🏗️ 아키텍처

```
Input → Embedding + Positional Encoding
      → [Multi-Head Self-Attention
      →  Add & Norm
      →  Feed Forward
      →  Add & Norm] × N
      → Output
```

### Residual Connection & Layer Norm

```python
output = LayerNorm(x + MultiHeadAttention(x))
output = LayerNorm(output + FeedForward(output))
```

## ⭐ 평가

**강점**
- 명확한 아이디어: 어텐션만으로 충분하다
- 충실한 실험: 다양한 태스크에서 검증
- 재현 가능: 코드와 설정이 잘 기술됨

**한계**
- 계산 복잡도 O(n²): 긴 시퀀스에서 비효율
- 절대적 위치 정보만 사용

## 🔍 이후 발전

```
2017  Transformer (이 논문)
2018  BERT - Bidirectional Encoder
2018  GPT - 디코더 기반 생성 모델
2020  Vision Transformer (ViT)
2022  ChatGPT (GPT-3.5 RLHF)
2024  GPT-4o, Claude 3, Gemini ...
```

> **개인 총평 ⭐⭐⭐⭐⭐**: 현대 AI 혁명의 시발점. 아이디어의 우아함이 인상적입니다.

다음 리뷰: **LLaMA 2 - Meta의 오픈소스 전략**
