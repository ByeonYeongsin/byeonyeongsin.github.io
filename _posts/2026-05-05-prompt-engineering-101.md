---
layout: post
title: "Prompt Engineering 101: LLM과 대화하는 법"
date: 2026-05-05
categories: [ai-study]
tags: [Prompt Engineering, LLM, ChatGPT, Claude]
excerpt: "효과적인 프롬프트 작성법을 배우고, 같은 모델도 다르게 사용하는 법을 알아봅시다."
---

## 프롬프트 엔지니어링이란?

**간단히**: LLM으로부터 원하는 출력을 얻기 위한 입력 작성 기법

**실제로**: 마법사가 정령에게 주문을 거는 것과 비슷합니다.

## 📋 기본 원칙

### 1. 명확함 (Clarity)

```
❌ 나쁜 프롬프트
"AI에 대해 얘기해줄래?"

✅ 좋은 프롬프트
"AI의 정의, 주요 응용 분야, 현재의 한계를 
3개 문단으로 설명해주세요. 한국어로."
```

### 2. 컨텍스트 제공 (Context)

```
❌ "파이썬이 뭐야?"

✅ "AI 초보자를 위해 
파이썬이 AI/ML 개발에 왜 중요한지, 
다른 언어와의 차이점, 학습 리소스를 설명해줘."
```

### 3. 역할 지정 (Role Assignment)

```python
system_message = """
당신은 경험 10년의 AI 엔지니어입니다.
기술적이지만 이해하기 쉬운 설명을 제공합니다.
한국어로 답변해주세요.
"""
```

## 🎯 고급 기법

### 1. Few-Shot Prompting (예시를 통한 학습)

```
질문: "다음 문장을 분류하세요 (긍정/부정)"

예시:
- "이 영화 정말 좋았어!" → 긍정
- "끔찍한 서비스네요" → 부정
- "그냥 그래요" → 중립

분류할 문장: "제품이 기대보다 나아요"
답변:
```

**효과**: 정확도 30~50% 향상

### 2. Chain-of-Thought (단계적 사고)

```
❌ "이 문제의 답은?"

✅ "이 문제를 단계별로 풀어주세요:
1. 먼저 문제를 이해하기
2. 필요한 정보 정리하기
3. 논리적으로 풀이하기
4. 최종 답 제시하기"
```

**효과**: 복잡한 문제 정확도 대폭 향상

### 3. System Prompt 설정

```python
from openai import OpenAI

client = OpenAI()

response = client.chat.completions.create(
    model="gpt-4",
    messages=[
        {
            "role": "system",
            "content": "당신은 친절한 AI 튜터입니다. 쉬운 언어로 설명해주세요."
        },
        {
            "role": "user",
            "content": "양자 컴퓨팅이 뭔가요?"
        }
    ]
)
```

### 4. Temperature 조절

```python
# 창의적인 답변 필요 (이야기, 시 등)
response = client.chat.completions.create(
    temperature=0.9,  # 높을수록 창의적
    ...
)

# 정확한 답변 필요 (수학, 코드 등)
response = client.chat.completions.create(
    temperature=0.1,  # 낮을수록 일관성 있음
    ...
)
```

## 💡 실용적인 예시

### 1. 코드 리뷰 프롬프트

```
"""
다음 파이썬 코드를 검토해주세요:
1. 성능 문제 찾기
2. 보안 문제 지적
3. 개선 제안
4. 예시 코드 제시

[코드]
```

### 2. 논문 요약 프롬프트

```
"""
이 논문을 읽고:
- 핵심 기여도 (3줄)
- 방법론 (5줄)
- 결과 (3줄)
- 한계 (2줄)

로 요약해주세요.

[논문 텍스트]
"""
```

### 3. 아이디어 브레인스토밍

```
"""
AI를 이용한 교육 앱 아이디어를 
다음 요구사항 하에서 10개 생성해주세요:
- 타겟: 중학생
- 비용: 낮음
- 개발 시간: 3개월 이내

각 아이디어에 대해:
1. 개념
2. 핵심 기능
3. 기술 스택
4. 수익화 모델

을 설명해주세요.
"""
```

## ⚠️ 주의사항

### ❌ 흔한 실수들

1. **너무 일반적인 질문**
   - 좋은 결과를 기대할 수 없음

2. **너무 길고 복잡한 프롬프트**
   - 오히려 모델이 혼동함

3. **구체적인 포맷 미지정**
   - JSON, 마크다운 등 명시하기

### ✅ Best Practice

```python
template = """
## 작업
{task_description}

## 제약사항
{constraints}

## 입력
{input}

## 출력 포맷
{output_format}

## 예시
{examples}
"""
```

## 🧪 실험해보기

```python
# 같은 질문, 다른 프롬프트
prompts = [
    "프롬프트 엔지니어링이란?",
    "AI 초보자도 이해할 수 있도록 프롬프트 엔지니어링을 설명해주세요",
    "프롬프트 엔지니어링에 대해 기술적으로 상세히 설명하되, 예시 3개도 포함해주세요"
]

for prompt in prompts:
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    print(f"Q: {prompt[:30]}...")
    print(f"답변 길이: {len(response.choices[0].message.content)} 자")
    print("---")
```

## 📈 측정과 개선

```python
def evaluate_prompt(prompt, test_cases):
    scores = []
    for question, expected_type in test_cases:
        response = get_response(prompt, question)
        score = evaluate_response(response, expected_type)
        scores.append(score)
    
    return sum(scores) / len(scores)

# 여러 프롬프트 비교
best_prompt = max(
    prompt_candidates,
    key=lambda p: evaluate_prompt(p, test_cases)
)
```

---

**핵심**: 프롬프트는 시스템이 아니라 **대화**입니다. 
계속 조정하고 개선하세요!

**다음 글**: "프롬프트 인젝션 공격과 방어법"
