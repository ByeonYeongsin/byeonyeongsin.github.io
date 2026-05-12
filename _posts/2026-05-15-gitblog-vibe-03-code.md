---
title: "[깃블로그 바이브코딩] 3. 기존 코드 수정"
date: 2026-05-15 09:00:00 +0900
categories: [Vibe Coding, AI Product Builder, 깃블로그 바이브코딩]
tags: [vibe-coding, jekyll, chirpy, github-pages, claude-code, cursor]
---

> 이 시리즈는 AI Product Builder 방식으로 깃블로그를 직접 만들어가는 과정을 기록합니다.

## 이번 편에서 다룰 것

PRD와 UX/UI 설계가 끝났습니다. 이번엔 **실제 코드 수정**입니다.

```
아이디어 → PRD → UX/UI → ✅ 코드 수정 → 배포
```

Chirpy 테마를 설치하고, 홈페이지를 CV 스타일로 바꾸고,  
카테고리 탭을 커스텀하고, GitHub Actions로 자동 배포하기까지  
실제로 발생한 **에러와 해결 과정**을 기록합니다.

---

## 전체 수정 흐름

```
1. Gemfile 설정 (Chirpy 테마 적용)
2. _config.yml 기본 설정
3. GitHub Actions 워크플로우 설정
4. index.html — CV형 홈페이지 작성
5. _tabs/ — 네비게이션 탭 커스텀
6. _posts/ — 포스트 front matter 구조 정리
7. 빌드 에러 3회 디버깅 및 수정
8. GitHub Pages 배포 확인
```

---

## 1. Gemfile 설정

### Claude에게 요청

```
Jekyll Chirpy 테마를 GitHub Pages에 배포하기 위한
최소한의 Gemfile을 작성해줘.
```

### 결과

```ruby
# Gemfile
source "https://rubygems.org"
gem "jekyll-theme-chirpy", "~> 7.3"
```

> ✅ **포인트**: `jekyll-github-pages` gem을 쓰면 테마 충돌이 납니다.  
> Chirpy는 자체 빌드 시스템이 있어서 `jekyll-theme-chirpy`만 지정하면 됩니다.

---

## 2. _config.yml 핵심 설정

```yaml
theme: jekyll-theme-chirpy
lang: ko-KR
timezone: Asia/Seoul
title: Yeongsin's AI Lab
tagline: AI Engineer · LLM · RAG · ML Systems
url: "https://byeonyeongsin.github.io"
baseurl: "/yeongsin.github.io"

github:
  username: ByeonYeongsin

social:
  name: 변영신
  email: yeongsin_byeon@kolon.com
  links:
    - https://github.com/ByeonYeongsin
```

> ⚠️ **주의**: `url`과 `baseurl`을 정확히 설정하지 않으면 CSS/JS가 깨집니다.  
> `username.github.io` 레포가 아니면 `baseurl`에 레포명을 넣어야 합니다.

---

## 3. GitHub Actions 워크플로우

### Claude에게 요청

```
Chirpy Jekyll 테마를 GitHub Pages에 배포하는
GitHub Actions 워크플로우를 작성해줘.
Ruby 3.x 환경, pages-deploy 방식으로.
```

```yaml
# .github/workflows/pages-deploy.yml
name: Build and Deploy

on:
  push:
    branches: [main]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - uses: ruby/setup-ruby@v1
        with:
          ruby-version: 3.3
          bundler-cache: true

      - name: Build site
        run: bundle exec jekyll build
        env:
          JEKYLL_ENV: production

      - uses: actions/upload-pages-artifact@v3
        with:
          path: _site

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - id: deployment
        uses: actions/deploy-pages@v4
```

---

## 4. 홈페이지 (index.html) 커스텀

UX 설계에서 잡은 와이어프레임을 코드로 구현합니다.

### Claude에게 요청

```
바로 코드를 수정하지 말고 먼저 구현 계획을 작성해줘.
Jekyll Chirpy 테마에서 홈페이지를 CV 스타일로 바꾸려면
어떤 파일을 수정해야 하는지, 수정 이유, 영향 범위를 정리해줘.
```

**Claude 답변:**

```
수정 대상: index.html (루트)
방법: layout: page 사용 + 인라인 HTML/CSS
이유: Chirpy 기본 홈(layout: home)은 포스트 목록만 표시하므로
      CV 형식으로 전환하려면 오버라이드 필요
영향: 홈 페이지만 변경. 다른 페이지/포스트에 영향 없음
리스크: Chirpy 업데이트 시 layout: page 스타일 변경 가능
```

### 주요 섹션 코드

**프로필 헤더**
```html
---
layout: page
title: ""
permalink: /
---
<div class="profile-header" style="
  background: linear-gradient(135deg, #1a1a2e, #16213e, #0f3460);
  border-radius: 12px;
  padding: 2.5rem;
  margin-bottom: 2rem;
  color: white;
">
  <h1>변영신 (Yeongsin Byeon)</h1>
  <p>AI Engineer · LLM · RAG · ML Systems</p>
  <div>
    <a href="https://github.com/ByeonYeongsin">GitHub</a>
  </div>
</div>
```

**기술 스택 태그**
```html
<div class="skill-tags">
  {% assign skills = "Python,PyTorch,LangChain,RAG,FastAPI,Docker,AWS" | split: "," %}
  {% for skill in skills %}
    <span class="badge">{{ skill }}</span>
  {% endfor %}
</div>
```

---

## 5. _tabs/ 커스텀

Chirpy의 사이드바 네비게이션은 `_tabs/` 폴더의 마크다운 파일로 제어합니다.

```bash
_tabs/
├── about.md       # order: 5
├── archives.md    # order: 3
├── categories.md  # order: 1 (Posts로 이름 변경)
├── projects.md    # order: 2 (신규 추가)
└── tags.md        # order: 4
```

### categories.md — 카테고리 카드 추가

```markdown
---
layout: page
icon: fas fa-pen-nib
order: 1
title: Posts
---

## 카테고리

<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 1rem;">
  <div class="category-card">
    <h3>🤖 AI Development</h3>
    <p>RAG, Fine-tuning, LLM 개발</p>
  </div>
  <!-- ... -->
</div>
```

---

## 6. 포스트 front matter 구조

### 카테고리 계층 설계

Chirpy는 배열 front matter로 계층을 표현합니다:

```yaml
# 1단계: categories: [Vibe Coding]
# 2단계: categories: [Vibe Coding, AI Product Builder]
# 3단계: categories: [Vibe Coding, AI Product Builder, 깃블로그 바이브코딩]
```

이 구조를 모든 포스트에 일관되게 적용했습니다.

---

## 7. 빌드 에러 3회 — 실제 디버깅 과정

### Error 1: `jekyll-redirect-from` not found

```
Bundler could not find compatible versions for gem "jekyll-redirect-from"
```

**원인**: `_config.yml`의 `plugins:` 섹션에 명시했지만 Gemfile에 없음  
**해결**: `_config.yml`에서 `plugins:` 섹션 전체 삭제 (Chirpy가 내부적으로 관리)

```yaml
# ❌ 제거
plugins:
  - jekyll-redirect-from
  - jekyll-paginate
```

---

### Error 2: `undefined method 'gsub' for Integer`

```
NoMethodError: undefined method `gsub' for 2026:Integer
```

**원인**: YAML에서 `tags: [ai-trends, 2026]`의 `2026`이 Integer로 파싱됨  
Chirpy의 `slugify` 필터가 String을 기대하는데 Integer가 들어옴

**해결**: 숫자 태그를 따옴표로 감싸기

```yaml
# ❌ 에러
tags: [ai-trends, 2026, llm]

# ✅ 수정
tags: [ai-trends, "2026", llm]
```

---

### Error 3: `@import "minima"` not found

```
Error: File to import not found or unreadable: minima.
```

**원인**: 이전에 minima 테마용으로 만든 `assets/css/style.scss`가 남아있음  
Chirpy에는 `minima` SCSS가 없어서 컴파일 실패

**해결**: 해당 파일 삭제

```bash
git rm assets/css/style.scss
git commit -m "remove minima style.scss"
git push
```

---

## 8. GitHub Pages 배포 설정

### GitHub Settings → Pages

```
Source: GitHub Actions (⚠️ "Deploy from a branch" 아님!)
```

`Deploy from a branch`를 선택하면 Chirpy 워크플로우와 충돌합니다.  
반드시 **GitHub Actions**로 선택해야 합니다.

### 최종 배포 URL

```
https://byeonyeongsin.github.io/yeongsin.github.io/
```

---

## 전체 작업 시간 & AI 기여도

| 작업 | 총 시간 | AI 기여도 |
|-----|---------|---------|
| Gemfile + _config.yml | 10분 | 90% |
| GitHub Actions 워크플로우 | 5분 | 95% |
| 홈페이지 HTML/CSS | 30분 | 70% |
| 탭 커스텀 | 20분 | 60% |
| 에러 디버깅 3회 | 40분 | 80% |
| **총합** | **~2시간** | **~79%** |

> AI가 코드를 생성하고, 사람이 검수하고 맥락을 잡는 방식으로 진행하면  
> 혼자 처음부터 만드는 것보다 **3-5배 빠르게** 결과물을 낼 수 있습니다.

---

## 마무리: AI Product Builder 방식으로 만든 결과

이 시리즈 3편에 걸쳐 다음을 완성했습니다:

```
✅ PRD 작성 (10분)
✅ IA / UX 플로우 설계 (15분)
✅ UI 와이어프레임 (10분)
✅ Jekyll Chirpy 블로그 구현 (~2시간)
✅ GitHub Pages 자동 배포
✅ 15개+ 샘플 포스트 생성
```

**핵심 교훈**: AI는 초안을 만들고, 사람은 방향을 잡는다.  
이 블로그 자체가 AI Product Builder 방식의 살아있는 증거입니다. 🚀

---

**이전 편**: [[깃블로그 바이브코딩] 2. UX 플로우 및 UI 디자인](/posts/gitblog-vibe-02-ux-ui)
