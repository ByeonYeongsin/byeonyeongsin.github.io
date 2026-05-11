---
layout: post
title: "논문 리뷰: GPT-4 Technical Report 핵심 정리"
date: 2026-04-28
categories: [paper-review]
tags: [GPT-4, OpenAI, LLM, Multimodal, Paper Review]
excerpt: "OpenAI의 GPT-4 Technical Report를 분석하고 핵심 내용을 정리합니다."
---

## 📄 논문 정보

**제목**: GPT-4 Technical Report  
**저자**: OpenAI  
**발표**: 2023년 3월  
**링크**: [arxiv.org/abs/2303.08774](https://arxiv.org/abs/2303.08774)

> ⚠️ 주의: 이 논문은 구조, 학습 데이터, 파라미터 수 등 기술적 세부사항을 **공개하지 않습니다**.  
> 그럼에도 불구하고 평가 방법과 안전 연구에 대한 통찰이 많습니다.

---

## 🎯 핵심 기여

### 1. 멀티모달 능력

GPT-4는 텍스트와 이미지를 동시에 입력으로 받는 **최초의 대규모 멀티모달 모델** 중 하나입니다.

```
입력: 이미지 + 텍스트
출력: 텍스트

예시:
- 그래프 이미지 → "이 데이터가 의미하는 바는?"
- 코드 스크린샷 → "이 코드의 버그를 찾아줘"
- 음식 사진 → "이 요리의 레시피를 추측해줘"
```

### 2. 인간 수준 성능

다양한 전문 시험에서 인상적인 결과:

| 시험 | GPT-3.5 | GPT-4 | 인간 평균 |
|-----|---------|-------|---------|
| 사법시험 | 하위 10% | **상위 10%** | - |
| GRE Quantitative | 상위 25% | **상위 20%** | - |
| AMC 12 | 하위 6% | **하위 45%** | - |
| AP Chemistry | 56% | **71%** | - |

### 3. 향상된 정렬 (Alignment)

RLHF를 통한 안전성, 사실성, 유용성 개선

---

## 📊 평가 방법론

### Evals 프레임워크

OpenAI가 공개한 **Evals** 프레임워크를 통한 체계적인 평가:

```python
# Evals 예시 (공개 프레임워크)
class CustomEval(evals.Eval):
    def run(self, recorder):
        for sample in self.get_samples():
            result = self.completion_fn(
                prompt=sample["input"]
            )
            score = self.check_answer(
                result, 
                sample["expected"]
            )
            recorder.record_match(score)
```

### Few-Shot vs Zero-Shot

```
Zero-shot: 예시 없이 바로 질문
Few-shot: 2~5개 예시 제공 후 질문
Chain-of-thought: 단계적 사고 유도
```

GPT-4는 세 가지 모두에서 이전 모델 대비 큰 개선

---

## 🛡️ 안전 연구

### Red Teaming

논문에서 흥미로운 부분:

```
내부 Red Team → 잠재적 위험 발견
외부 전문가 → 다양한 관점에서 평가
반복적 개선 → 출시 전 6개월+ 안전 작업
```

### Constitutional AI 유사 접근법

```python
# 단순화된 개념
class SafeAI:
    def generate(self, prompt):
        response = self.model(prompt)
        
        # 안전 필터 적용
        if self.safety_check(response):
            return response
        else:
            return self.safe_fallback(prompt)
    
    def safety_check(self, text):
        # 유해 콘텐츠, 개인정보, 잘못된 정보 등 체크
        return not any([
            self.is_harmful(text),
            self.has_pii(text),
            self.is_factually_wrong(text)
        ])
```

### 주요 위험 요소들

1. **Hallucination**: 잘못된 정보를 사실처럼 제시
2. **Jailbreak**: 안전 장치 우회 시도
3. **Bias**: 특정 집단에 대한 편향
4. **Privacy**: 학습 데이터의 개인정보 노출

---

## 💡 주요 발견사항

### Predictable Scaling

```
더 많은 학습 = 더 나은 성능
이것이 예측 가능하게 관측됨
→ 스케일링 법칙(Scaling Laws) 유효성 확인
```

### 능력의 창발 (Emergent Abilities)

```
단순히 더 크게 만들었을 뿐인데
예상치 못한 능력이 생김:

- 다단계 수학 추론
- 코드 디버깅
- 복잡한 지시 따르기
- 언어 간 추론
```

---

## 🔍 비공개 정보들

OpenAI가 공개하지 않은 것들:

- ❌ 파라미터 수
- ❌ 정확한 학습 데이터
- ❌ 모델 아키텍처
- ❌ 학습 컴퓨팅 비용

**이유**: 경쟁사 보호 + 안전 우려

---

## ⭐ 개인 평가

### 강점
- 실용적인 평가 방법론 공개
- 안전 연구에 대한 투명성
- 다양한 벤치마크에서 검증

### 아쉬운 점
- 기술적 세부사항 미공개
- 재현 불가능한 연구
- "우리만 알고 있음" 방식

### 총평: ⭐⭐⭐⭐

AI 안전에 대한 진지한 접근법이 인상적이지만,  
과학적 재현성 측면에서는 아쉬움이 있습니다.

---

**다음 리뷰**: LLaMA 2 - Meta의 오픈소스 전략  
**관련 포스트**: [Attention Is All You Need 리뷰](/yeongsin.github.io/paper-review/2026/05/07/attention-all-you-need-review/)
