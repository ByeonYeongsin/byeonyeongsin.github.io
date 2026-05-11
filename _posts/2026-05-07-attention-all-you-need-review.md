---
layout: post
title: "논문 리뷰: Attention Is All You Need (Transformer 논문)"
date: 2026-05-07
categories: [paper-review]
tags: [Transformer, NLP, Deep Learning, Paper Review]
excerpt: "현대 AI의 기초를 마련한 'Attention Is All You Need' 논문을 상세히 분석합니다."
---

## 📄 논문 정보

**제목**: Attention Is All You Need  
**저자**: Vaswani et al. (Google Brain, Google Research)  
**발표**: 2017년 NeurIPS  
**인용**: 100,000+회 (가장 인용된 AI 논문 중 하나)

## 🎯 핵심 기여

이 논문은 **RNN 없이 어텐션만으로도 좋은 성능을 낼 수 있다**는 것을 증명했습니다.

### 혁신점

1. **Self-Attention 메커니즘**: 시퀀스 내 모든 위치 간의 관계 모델링
2. **병렬 처리**: RNN의 순차 처리 제약 극복
3. **Positional Encoding**: 순서 정보 유지

## 📊 성능

| 모델 | BLEU | 학습 시간 |
|-----|------|---------|
| Transformer | **28.4** | 3.5일 |
| 이전 SOTA | 27.3 | 12일+ |

## 🏗️ 아키텍처

### Encoder-Decoder 구조

```
입력 → Embedding + Positional Encoding 
      → Multi-Head Self-Attention
      → Feed Forward Network
      → (반복 × N layers)
      → 디코더도 동일 구조
      → 출력
```

## 💡 주요 개선사항

### 1. Multi-Head Attention (H=8)

```python
# 8개의 다른 representation space에서 동시에 어텐션
# 하나는 단어의 의미, 하나는 문법, ... 등으로 학습
```

### 2. Residual Connection & Layer Normalization

```python
output = LayerNorm(x + MultiHeadAttention(x))
output = LayerNorm(output + FeedForward(output))
```

이를 통해 매우 깊은 네트워크를 안정적으로 학습 가능

### 3. Position-Wise Feed-Forward Network

```python
FFN(x) = max(0, xW1 + b1)W2 + b2
# 두 개의 선형 변환 + ReLU
```

## 📈 실험 결과

- **Machine Translation**: 새로운 SOTA 달성
- **Parsing**: 구조적 감수성 입증
- **Generalization**: 큰 데이터에서 더 빠르게 수렴

## ⭐ 논문의 강점

✅ 명확한 아이디어: 어텐션만으로 충분하다  
✅ 충실한 실험: 다양한 테스크에서 검증  
✅ 재현 가능: 코드와 설정이 잘 기술됨  
✅ 영향력: 현대 AI 대혁명의 시작

## ⚠️ 제한사항

❌ 계산 복잡도: O(n²) (긴 시퀀스에서 비효율)  
❌ 절대적 위치 정보: 상대적 위치 정보도 필요  
❌ 메모리: 대규모 모델의 메모리 사용량  

## 🔍 이후 발전

이 논문 이후 많은 개선과 확장이 이루어졌습니다:

- **BERT** (2018): Bidirectional Transformer
- **GPT** (2018~): 디코더만 사용한 생성 모델
- **Vision Transformer** (2020): 이미지에 Transformer 적용
- **Efficient Transformers**: 계산 복잡도 개선

## 💭 개인적 생각

이 논문은 단순하지만 강력합니다. "모든 문제를 어텐션으로 해결할 수 있을까?"라는 질문이 오늘날의 LLM 혁명으로 이어졌습니다.

특히 인상적인 부분:
1. 아이디어의 우아함
2. 실험의 엄밀성
3. 실제 영향력

---

**다음 리뷰**: Vision Transformer (ViT) - 이미지에 Transformer를 어떻게 적용했을까?
