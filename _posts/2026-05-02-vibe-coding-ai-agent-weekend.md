---
title: "주말에 AI 에이전트 만들다가 생긴 일 🤣"
date: 2026-05-02 09:00:00 +0900
categories: [Vibe Coding, 주말프로젝트]
tags: [ai-agent, langgraph, vibe-coding, 주말프로젝트, langchain]
---

## 발단

금요일 밤 11시. 퇴근 후 유튜브를 보다가 LangGraph로 AI 에이전트 만드는 영상을 봤습니다.

*"오, 이거 나도 할 수 있겠는데?"* 🤔

...결과적으로는 할 수 있었습니다. 하지만 **그 과정이 문제**였죠.

---

## 토요일 오전: 자신감 충만

```python
# 계획한 것 (예상 소요 시간: 2시간)
agent = create_agent(
    tools=[search, calculator, code_executor],
    memory=True
)
```

뭔가 되게 쉬워보였습니다...

## 토요일 오후: 첫 번째 벽

**에러 1**: 버전 충돌 → 해결에 45분 소요

```
ERROR: langchain requires langchain-core<0.2,>=0.1.16
but you have langchain-core 0.2.1
```

**에러 2**: API 키 깜빡함 → 30분 삽질 후 3분 해결

```python
# 이걸 까먹음...
import os
os.environ["OPENAI_API_KEY"] = "sk-..."
```

## 토요일 저녁: 무한 루프의 공포

에이전트가 멈추지 않았습니다 💸

```
[Agent] 검색 실행 중...
[Agent] 추가 검색 필요.
[Agent] 검색 실행 중...
[Agent] 추가 검색 필요.
(∞ 비용이 쌓이는 중...)
```

급히 추가한 안전장치:

```python
MAX_ITERATIONS = 10

def should_continue(state):
    if state["iterations"] > MAX_ITERATIONS:
        return "end"
    return "continue"
```

## 일요일 오전: 드디어 빛이!

```
나: "서울 날씨 알려줘"
에이전트: 오늘 서울은 맑고 22도입니다. 자외선 지수 높으니 선크림 바르세요! ☀️

나: (감동의 눈물)
```

## 최종 결과

| 항목 | 결과 |
|-----|------|
| 기본 검색 에이전트 | ✅ 완성 |
| 대화 메모리 | ✅ 완성 |
| 계산기 도구 | ✅ 완성 |
| 코드 실행 | ❌ 시간 부족 |
| 멀티 에이전트 | ❌ 다음에... |

## 배운 것들

```python
# 1. 항상 max_iterations 설정
graph.add_conditional_edges("agent", should_continue, {
    "continue": "tools",
    "end": END
})

# 2. 비용 모니터링 필수!
from langchain.callbacks import get_openai_callback
with get_openai_callback() as cb:
    result = agent.run(query)
    print(f"총 비용: ${cb.total_cost:.4f}")
```

**인간적으로 배운 것**:
- 주말 코딩은 계획보다 3배 오래 걸린다
- 중간에 밥을 먹어야 한다 (12시간 굶음 😅)
- 완성보다 학습이 더 중요할 때도 있다

---

> 혹시 비슷한 주말 코딩 경험 있으신가요?  
> 댓글로 여러분의 삽질 이야기를 공유해주세요! 😄
