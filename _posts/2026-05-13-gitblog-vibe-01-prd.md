---
title: "[깃블로그 바이브코딩] 1. 아이디어 기획/PRD 문서 생성"
date: 2026-05-13 09:00:00 +0900
categories: [Vibe Coding, AI Product Builder, 깃블로그 바이브코딩]
tags: [vibe-coding, prd, gitblog, jekyll, ai-product-builder, planning]
---

> 이 시리즈는 AI Product Builder 방식으로 깃블로그를 직접 만들어가는 과정을 기록합니다.  
> 아이디어 기획부터 PRD 작성, UX 설계, 코드 수정, 배포까지 전 과정을 AI와 함께 진행합니다.

## 이 시리즈에 대해

AI Product Builder란 포스트에서 설명한 것처럼, AI 시대의 제품 개발은 혼자서도 전 주기를 커버할 수 있습니다.  
이 시리즈는 그 실제 증거입니다. **깃블로그 하나를 AI Product Builder 방식으로 처음부터 만들어봅니다.**

```
아이디어 → PRD → UX/UI → 코드 수정 → 배포
```

오늘은 첫 번째 단계: **아이디어 기획과 PRD 문서 생성**입니다.

---

## 1단계: 아이디어 정리 (Product Discovery)

### 왜 깃블로그인가?

| 동기 | 내용 |
|-----|------|
| **기록 목적** | AI 개발 과정에서 배운 것을 정리하고 싶다 |
| **포트폴리오** | 이력서에 첨부할 수 있는 기술 블로그가 필요하다 |
| **실험 목적** | AI Product Builder 방식을 직접 검증해보고 싶다 |

### 핵심 사용자 (Persona)

```
나 자신 — AI 엔지니어
- 마크다운에 익숙하다
- 디자인은 잘 모른다
- 유지보수가 쉬웠으면 좋겠다
- 도메인 비용을 아끼고 싶다
```

### MVP 범위 정의

Claude에게 아래 프롬프트를 입력했습니다:

```
나는 AI 엔지니어 깃블로그를 만들고 싶다.
주요 독자는 나 자신과 다른 AI 개발자들이다.
카테고리: AI Development, AI Study, Paper Review, Vibe Coding, Development
기술 스택: GitHub Pages, Jekyll

이 블로그의 MVP 기능 목록과 성공 지표를 정리해줘.
```

**Claude 답변 요약:**

| MVP 기능 | 우선순위 |
|---------|---------|
| 카테고리별 포스트 분류 | 🔴 Must |
| 이력서/프로필 홈페이지 | 🔴 Must |
| 태그 기반 검색 | 🟡 Should |
| 다크모드 | 🟢 Nice |
| 프로젝트 페이지 | 🟡 Should |

---

## 2단계: PRD 작성

### Claude에게 PRD 생성 요청

```
다음 깃블로그 프로젝트의 PRD를 작성해줘.

프로젝트명: Yeongsin's AI Lab (GitHub Blog)
플랫폼: GitHub Pages + Jekyll (Chirpy 테마)
목적: AI 엔지니어 기술 블로그 + 포트폴리오

항목: Overview, Problem Statement, Goal, Non-Goal,
      Target User, User Scenario, Functional Requirements,
      Non-Functional Requirements, Success Metrics
```

### 생성된 PRD 요약

---

#### Overview

AI 엔지니어 변영신의 기술 블로그. GitHub Pages와 Jekyll Chirpy 테마를 활용하여 무료로 운영하는 개인 기술 블로그 겸 포트폴리오 사이트.

#### Problem Statement

- AI 개발 과정에서 배운 지식이 분산되어 있고 정리되지 않음
- 포트폴리오로 제출할 수 있는 기술 블로그가 없음
- 블로그 서비스(Tistory, Velog)는 커스터마이징 한계 존재

#### Goal

- GitHub Pages 기반 무료 운영 블로그 구축
- CV 스타일 홈페이지로 포트폴리오 역할
- 카테고리 계층 구조로 AI/개발 콘텐츠 체계적 관리

#### Non-Goal

- 댓글 시스템 (1차 MVP 제외)
- 광고 수익화
- 다국어 지원

#### Functional Requirements

```
FR-001: 홈페이지에 프로필, 기술스택, 경력, 프로젝트를 표시한다
FR-002: 카테고리 계층(3단계)으로 포스트를 분류한다
FR-003: 태그로 포스트를 검색할 수 있다
FR-004: 다크모드/라이트모드를 지원한다
FR-005: GitHub Actions로 자동 배포된다
FR-006: 모바일 반응형 UI를 제공한다
```

#### Success Metrics

| 지표 | 목표 |
|-----|------|
| GitHub Actions 빌드 성공률 | 100% |
| 모바일 Lighthouse 점수 | > 80 |
| 첫 3개월 포스트 수 | > 20개 |

---

## 3단계: 기술 결정 (Technical Design)

PRD를 바탕으로 기술 스택을 결정했습니다.

```
[Claude에게 기술 설계 요청]
위 PRD를 기반으로 GitHub Pages 블로그의 기술 설계를 해줘.
Jekyll 테마 추천, 파일 구조, 카테고리 설계 방식을 포함해줘.
```

**결정 사항:**

| 항목 | 선택 | 이유 |
|-----|------|------|
| Jekyll 테마 | **Chirpy** | 기술 블로그 특화, 다크모드, 카테고리/태그 지원 |
| 배포 방식 | **GitHub Actions** | 자동 빌드+배포, 안정적 |
| 홈 레이아웃 | **layout: page** | Chirpy 기본 홈 대신 CV형 커스텀 |
| 카테고리 구조 | **배열 front matter** | `[Vibe Coding, AI Product Builder, 깃블로그 바이브코딩]` |

---

## 배운 점

### AI Product Builder 방식의 강점

1. **아이디어 → PRD 전환이 10분 이내** — Claude에게 맥락만 주면 구조화된 문서를 즉시 생성
2. **요구사항 누락 방지** — Non-Goal, Edge Case까지 AI가 제안
3. **기술 결정도 근거 있게** — 테마 비교, 배포 방식 장단점을 AI가 정리

### 주의할 점

> ⚠️ AI가 생성한 PRD는 **시작점**입니다. 실제 프로젝트 맥락에 맞게 반드시 검수하고 수정하세요.

---

**다음 편**: [[깃블로그 바이브코딩] 2. UX 플로우 및 UI 디자인](/posts/gitblog-vibe-02-ux-ui)
