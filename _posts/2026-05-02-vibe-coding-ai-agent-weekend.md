---
layout: post
title: "주말에 AI 에이전트 만들다가 생긴 일 🤣"
date: 2026-05-02
categories: [vibing-coding]
tags: [AI Agent, LangGraph, Vibe Coding, 주말프로젝트]
excerpt: "주말 48시간 동안 AI 에이전트 만들기에 도전한 생생 후기입니다."
---

## 발단

금요일 밤 11시. 퇴근 후 유튜브를 보다가 LangGraph로 AI 에이전트 만드는 영상을 봤습니다.

"오, 이거 나도 할 수 있겠는데?" 🤔

...결과적으로는 할 수 있었습니다. 하지만 그 과정이 문제였죠.

---

## 토요일 오전: 자신감 충만

```python
# 계획한 것
agent = create_agent(
    tools=[search, calculator, code_executor],
    memory=True,
    personality="helpful"
)
# 예상 소요 시간: 2시간
```

뭔가 되게 쉬워보였습니다...

---

## 토요일 오후: 첫 번째 벽

**에러 1**: 버전 충돌

```
ERROR: langchain 0.1.0 requires langchain-core<0.2,>=0.1.16
but you have langchain-core 0.2.1
```

해결: 45분  
느낀 것: 왜 파이썬 패키지는 항상 싸우는 걸까

**에러 2**: API 키 설정 문제

```python
# 이걸 까먹음
import os
os.environ["OPENAI_API_KEY"] = "..."

# AuthenticationError: No API key provided
```

해결: 3분 (하지만 30분 동안 다른 데 삽질)

---

## 토요일 저녁: 진짜 문제 시작

에이전트가 무한 루프에 빠졌습니다.

```
[Agent] 검색 실행 중...
[Agent] 검색 완료. 추가 검색 필요.
[Agent] 검색 실행 중...
[Agent] 검색 완료. 추가 검색 필요.
[Agent] 검색 실행 중...
(∞)
```

비용이... 쌓이고 있었습니다 💸

```python
# 급히 추가한 안전장치
MAX_ITERATIONS = 10
current_iteration = 0

while True:
    current_iteration += 1
    if current_iteration > MAX_ITERATIONS:
        print("루프 감지! 탈출!")
        break
    # ...
```

---

## 일요일 오전: 빛이 보임

드디어 에이전트가 말이 되는 답변을 내놓기 시작했습니다!

```
나: "서울 날씨 알려줘"
에이전트: 검색 중...
에이전트: 오늘 서울 날씨는 맑고 기온은 22도입니다.
          자외선 지수가 높으니 선크림을 바르세요! ☀️

나: (눈물)
```

---

## 일요일 오후: 마무리

완성된 것:
- ✅ 기본 검색 에이전트
- ✅ 메모리 기능 (대화 맥락 유지)
- ✅ 도구 호출 (검색, 계산기)
- ❌ 코드 실행 (시간 부족)
- ❌ 멀티 에이전트 (다음에...)

---

## 배운 것들

### 기술적으로

```python
# 1. 항상 max_iterations 설정
graph = StateGraph(AgentState)
graph.add_node("agent", agent_node)
graph.add_conditional_edges(
    "agent",
    should_continue,
    {
        "continue": "tools",
        "end": END,
    }
)

# 2. 비용 모니터링 필수
from langchain.callbacks import get_openai_callback

with get_openai_callback() as cb:
    result = agent.run(query)
    print(f"총 비용: ${cb.total_cost:.4f}")

# 3. 로깅 추가하면 디버깅이 훨씬 쉬움
import logging
logging.basicConfig(level=logging.DEBUG)
```

### 인간적으로

- 주말 코딩은 계획보다 3배 오래 걸린다
- 에러 메시지를 잘 읽으면 답이 있다
- 중간에 밥을 먹어야 한다 (12시간 굶음)
- 완성보다 학습이 더 중요할 때도 있다

---

## 다음 목표

```
이번 주말: 멀티 에이전트 시스템
다다음 주말: 코드 실행 에이전트
그 다음: ...잠
```

---

혹시 비슷한 주말 코딩 경험 있으신가요? 😅  
댓글로 여러분의 "삽질" 이야기를 공유해주세요!
