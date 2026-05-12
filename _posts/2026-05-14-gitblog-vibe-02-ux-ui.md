---
title: "[깃블로그 바이브코딩] 2. UX 플로우 및 UI 디자인"
date: 2026-05-14 09:00:00 +0900
categories: [Vibe Coding, AI Product Builder, 깃블로그 바이브코딩]
tags: [vibe-coding, ux, ui, gitblog, jekyll, figma, design]
---

> 이 시리즈는 AI Product Builder 방식으로 깃블로그를 직접 만들어가는 과정을 기록합니다.

## 이번 편에서 다룰 것

지난 편에서 PRD를 완성했습니다. 이번엔 **UX 플로우와 UI 디자인**입니다.

```
아이디어 → PRD → ✅ UX/UI → 코드 수정 → 배포
```

깃블로그처럼 정적 사이트도 UX 설계 단계가 있어야 합니다.  
"그냥 테마 받아서 쓰면 되지 않나?"라고 생각할 수 있지만,  
**어떤 레이아웃, 어떤 네비게이션, 어떤 콘텐츠 계층**을 가질지 결정해야 합니다.

---

## 1단계: IA (Information Architecture) 설계

### Claude에게 IA 설계 요청

```
다음 PRD를 기반으로 깃블로그의 Information Architecture를 설계해줘.

목표: AI 엔지니어 기술 블로그 + 포트폴리오
주요 콘텐츠: 기술 포스트, 프로젝트, 이력서
네비게이션: 좌측 사이드바 (Chirpy 테마)

IA를 계층 구조로 표현하고, 각 페이지의 목적을 설명해줘.
```

### 생성된 IA

```
yeongsin.github.io/
│
├── 🏠 Home (/)
│   ├── 프로필 헤더 (이름, 직함, 소셜 링크)
│   ├── 기술 스택 태그
│   ├── 경력 타임라인
│   ├── 주요 프로젝트 카드
│   └── 최근 포스트 목록
│
├── 📝 Posts (/categories/)
│   ├── AI Development
│   ├── AI Study
│   ├── Paper Review
│   ├── Development
│   ├── Vibe Coding
│   │   ├── AI Product Builder
│   │   │   └── 깃블로그 바이브코딩
│   │   └── Debugging
│   └── Tools & Tips
│
├── 🚀 Projects (/projects/)
│   ├── 진행중 프로젝트 카드
│   └── 완료 프로젝트 카드
│
├── 📁 Archives (/archives/)
├── 🏷️ Tags (/tags/)
└── 👤 About (/about/)
```

---

## 2단계: User Flow 설계

### 주요 사용자 시나리오

**시나리오 1: 포스트 탐색자**

```
방문 → 홈에서 최근 포스트 확인
    → Posts 탭 클릭
    → 카테고리 카드에서 관심 분야 선택
    → 포스트 목록 확인
    → 포스트 읽기
    → 태그 클릭으로 관련 포스트 이동
```

**시나리오 2: 채용 담당자**

```
방문 → 홈에서 프로필/경력 확인
    → Projects 탭으로 이동
    → 프로젝트 상세 확인
    → About 페이지에서 연락처 확인
```

**시나리오 3: AI 개발자 동료**

```
검색 엔진 → 특정 기술 포스트 직접 진입
         → 관련 태그 클릭
         → 비슷한 포스트 탐색
         → 홈으로 이동, 다른 콘텐츠 확인
```

---

## 3단계: 화면별 와이어프레임 설계

Claude에게 각 화면의 와이어프레임을 텍스트로 요청했습니다.

```
깃블로그 홈 페이지의 와이어프레임을 ASCII art나
마크다운 형식으로 그려줘. Chirpy 테마의 사이드바 레이아웃 기준으로.
```

### 홈 페이지 와이어프레임

```
┌─────────────────────────────────────────────────┐
│  SIDEBAR          │  MAIN CONTENT               │
│                   │                             │
│  [Avatar]         │  ┌─────────────────────┐   │
│  Yeongsin         │  │  🎓 PROFILE HEADER  │   │
│  AI Engineer      │  │  이름 / 직함 / 링크  │   │
│                   │  └─────────────────────┘   │
│  ─────────────    │                             │
│  🏠 Home          │  ┌─────────────────────┐   │
│  📝 Posts         │  │  💡 TECH STACK      │   │
│  🚀 Projects      │  │  [Python][LLM][RAG] │   │
│  📁 Archives      │  └─────────────────────┘   │
│  🏷️ Tags          │                             │
│  👤 About         │  ┌─────────────────────┐   │
│                   │  │  📋 EXPERIENCE      │   │
│                   │  │  타임라인 형식       │   │
│                   │  └─────────────────────┘   │
│                   │                             │
│                   │  ┌─────────────────────┐   │
│                   │  │  🚀 PROJECTS        │   │
│                   │  │  [카드] [카드] [카드]│   │
│                   │  └─────────────────────┘   │
└─────────────────────────────────────────────────┘
```

### Posts 페이지 와이어프레임

```
┌─────────────────────────────────────────────────┐
│  SIDEBAR          │  POSTS                      │
│  (동일)           │                             │
│                   │  카테고리 카드 그리드:        │
│                   │  ┌──────┐  ┌──────┐        │
│                   │  │ AI   │  │ AI   │        │
│                   │  │ Dev  │  │Study │        │
│                   │  └──────┘  └──────┘        │
│                   │  ┌──────┐  ┌──────┐        │
│                   │  │Paper │  │Vibe  │        │
│                   │  │Review│  │Coding│        │
│                   │  └──────┘  └──────┘        │
│                   │                             │
│                   │  전체 포스트 목록:            │
│                   │  • [날짜] 포스트 제목        │
│                   │  • [날짜] 포스트 제목        │
└─────────────────────────────────────────────────┘
```

---

## 4단계: UI 디자인 결정

### 디자인 시스템 선택

Chirpy 테마의 기본 디자인 시스템을 그대로 활용합니다.

| 항목 | 결정 | 이유 |
|-----|------|------|
| 컬러 테마 | Chirpy 기본 (Blue accent) | 기술 블로그에 적합 |
| 다크모드 | 활성화 | 개발자 선호도 높음 |
| 폰트 | 시스템 폰트 | 로딩 속도 최적화 |
| 홈 레이아웃 | 커스텀 HTML + 인라인 CSS | Chirpy 레이아웃 오버라이드 |

### 홈 커스텀 UI 포인트

```
그라데이션 헤더 배경: #1a1a2e → #16213e → #0f3460
기술 스택 태그: 색상 구분 (Python=파랑, LLM=주황, ...)
경력 타임라인: 세로 라인 + 원형 마커
프로젝트 카드: CSS Grid, hover 효과
```

---

## 5단계: AI 도구 활용 UI 프롬프트

실제 코드로 가기 전, v0.dev나 Claude에게 UI 프롬프트를 작성합니다.

```
[v0.dev / Claude 프롬프트]
Create an AI engineer personal blog homepage with:
- Dark gradient header (#1a1a2e to #0f3460)
- Profile section with avatar, name, title, social links
- Tech stack badges: Python, LLM, RAG, PyTorch, FastAPI, Docker
- Experience timeline (vertical line style)
- Project cards grid (3 columns)
- Recent posts list
Style: modern, dark theme, developer-friendly
Framework: Plain HTML/CSS (Jekyll compatible, no JS framework)
```

### Claude가 제안한 주요 CSS 패턴

```css
/* 그라데이션 헤더 */
.profile-header {
  background: linear-gradient(135deg, #1a1a2e, #16213e, #0f3460);
  border-radius: 12px;
  padding: 2rem;
}

/* 기술 스택 태그 */
.skill-tag {
  display: inline-block;
  padding: 4px 12px;
  border-radius: 20px;
  background: rgba(255,255,255,0.1);
  margin: 4px;
  font-size: 0.85rem;
}

/* 프로젝트 카드 */
.project-card {
  border-radius: 12px;
  padding: 1.5rem;
  transition: transform 0.2s, box-shadow 0.2s;
}
.project-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.15);
}
```

---

## 배운 점

### UX 설계를 먼저 하면 좋은 이유

1. **코드 수정 방향이 명확해진다** — "어디에 무엇을 만들지" 정해놓고 코딩
2. **불필요한 수정 감소** — 설계 없이 코딩하면 계속 뒤집게 됨
3. **AI에게 정확한 지시 가능** — 와이어프레임이 있으면 프롬프트 품질 올라감

### Jekyll + Chirpy에서의 UI 커스텀 전략

```
✅ 가능: index.html에서 layout: page로 홈 완전 커스텀
✅ 가능: _tabs/ 파일로 네비게이션 커스텀
✅ 가능: 인라인 CSS로 스타일 추가
⚠️ 주의: Chirpy 내부 레이아웃(post.html 등)은 건드리지 않기
```

---

**이전 편**: [[깃블로그 바이브코딩] 1. 아이디어 기획/PRD 문서 생성](/posts/gitblog-vibe-01-prd)  
**다음 편**: [[깃블로그 바이브코딩] 3. 기존 코드 수정](/posts/gitblog-vibe-03-code)
