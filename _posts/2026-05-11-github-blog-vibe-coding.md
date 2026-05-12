---
title: "Claude로 깃블로그 바이브코딩하기: 0에서 배포까지"
date: 2026-05-11 10:00:00 +0900
categories: [Vibe Coding, 깃블로그 바이브코딩]
tags: [vibe-coding, jekyll, chirpy, github-pages, claude, ai]
pin: false
---

> 이 블로그 자체가 바이브코딩으로 만들어졌습니다. 그 과정을 기록합니다.

## 바이브코딩이란?

**Vibe Coding** = AI와 대화하며 코드를 짜는 개발 방식

기존 개발과의 차이:
```
기존: 직접 문서 읽기 → 코드 작성 → 디버깅
바이브: AI에게 말하기 → 결과 확인 → 피드백 → 반복
```

저는 Claude를 활용해서 이 블로그 전체를 바이브코딩으로 만들었습니다.

---

## 전체 과정

### 1단계: 레파지토리 생성

GitHub에서 `username.github.io` 형식으로 레파지토리 생성 후 Claude에게 요청:

```
"빈 레파지토리인데 깃블로그 만들어줘"
```

Claude가 즉시 생성한 것들:
- `_config.yml` - Jekyll 설정
- `index.md` - 홈페이지
- `_posts/` - 첫 포스트
- `Gemfile` - 의존성
- `.gitignore`

**소요 시간**: 5분

### 2단계: 배포 삽질

첫 배포에서 만난 문제들:

```
❌ GitHub Pages Source 설정 안 됨
  → Settings → Pages에서 활성화 필요

❌ 사이트 URL이 다름
  → yeongsin.github.io ≠ byeonyeongsin.github.io/yeongsin.github.io/
  → GitHub username과 repo 이름이 달라서 발생
```

**교훈**: `username.github.io`로 접속하려면 레파지토리 이름이 정확히 `username.github.io`여야 함

### 3단계: 콘텐츠 채우기

Claude에게 요청:

```
"AI 개발자 블로그 만들고싶어. 디자인 멋지게 꾸며줘.
카테고리는 AI 개발, 스터디, 논문 리뷰, 바이브코딩으로"
```

**결과**: 포스트 9개, 5개 카테고리, CV 홈페이지까지 한 번에

### 4단계: Chirpy 테마 적용

```
"지킬 테마 중 엔지니어가 사용하기 좋은 테마 골라서 사용해"
```

Claude가 Chirpy를 선택한 이유:
- ✅ 다크/라이트 모드
- ✅ 코드 하이라이팅
- ✅ TOC 자동 생성
- ✅ 검색 내장
- ✅ AI/개발 블로그에 딱 맞는 디자인

### 5단계: 에러 3연속 디버깅

테마 적용 후 빌드 에러가 3번 연속으로 났습니다:

**에러 1**: `jekyll-redirect-from` 없음
```
→ _config.yml에서 plugins 섹션 제거로 해결
```

**에러 2**: Integer `gsub` 메서드 오류
```
→ tags에 숫자 2026을 따옴표로 감싸서 해결
tags: ["2026"]
```

**에러 3**: `@import "minima"` 없음
```
→ Chirpy에 minima가 없으므로 style.scss 삭제로 해결
```

**바이브코딩의 강점**: 에러 로그를 그대로 붙여넣으면 즉시 원인과 해결책을 알려줌

---

## 바이브코딩 팁

### ✅ 잘 되는 것들

```
- 보일러플레이트 코드 생성
- 에러 디버깅 (로그 복붙)
- 반복 작업 자동화
- 스타일/CSS 작업
- 마크다운 포스트 작성
```

### ⚠️ 주의할 것들

```
- 배포 환경 특수성 (GitHub Pages 등)은 직접 확인 필요
- 에러 로그를 정확히 전달해야 함
- 결과를 반드시 눈으로 확인
```

### 💡 효과적인 프롬프트 패턴

```
❌ "블로그 만들어줘"

✅ "Jekyll + Chirpy 테마 기반으로
   AI 엔지니어 개인 블로그를 만들어줘.
   카테고리: AI 개발, 스터디, 논문 리뷰, 바이브코딩
   홈에는 CV/이력서 스타일로 구성해줘"
```

---

## 결과물

**총 소요 시간**: 약 2시간 (삽질 포함)

**직접 작성한 코드**: 거의 없음 (주로 Claude가 생성)

**배운 것**:
- Jekyll/Chirpy 기본 구조
- GitHub Pages 배포 방식
- 바이브코딩의 장단점

---

다음 편: **Chirpy 테마 고급 커스터마이징 with Claude**
