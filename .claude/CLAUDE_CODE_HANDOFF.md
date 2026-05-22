# Claude Code 핸드오프 문서

이 문서를 Claude Code에 복사/붙여넣기하면, 현재 Jekyll 블로그를 새로운 디자인 시스템으로 변환할 수 있습니다.

---

## 작업 요청

현재 Yeongsin's AI Lab 블로그를 새로운 디자인 시스템으로 완전히 변환해주세요.

### 변환 사항

1. **GitHub 저장소에서 코드 다운로드**
   - 저장소: https://github.com/ByeonYeongsin/yeongsin.github.io
   - 모든 파일 구조 그대로 유지

2. **새로운 CSS 시스템 적용**
   - 다음 CSS 파일을 `assets/` 폴더에 추가:
   
```css
/* FILE: assets/css/design-tokens.css */
@import url('https://fonts.googleapis.com/css2?family=Geist:wght@400;500;600;700&display=swap');

:root {
  /* ════════════════════════════════════════════════════════════════
     COLOR PALETTE — PRIMARY
     ════════════════════════════════════════════════════════════════ */

  /* Background */
  --color-bg-primary: #ffffff;
  --color-bg-secondary: #f9fafb;
  --color-bg-tertiary: #f0f0f0;

  /* Text / Foreground */
  --color-text-primary: #1a1a1a;
  --color-text-secondary: #666666;
  --color-text-tertiary: #999999;
  --color-text-inverse: #ffffff;

  /* Borders */
  --color-border-primary: #e5e5e5;
  --color-border-light: #f0f0f0;

  /* Accent */
  --color-accent: #0969da;
  --color-accent-hover: #0860ca;
  --color-accent-light: #f0f7ff;

  /* ════════════════════════════════════════════════════════════════
     TYPOGRAPHY — FONT FAMILY
     ════════════════════════════════════════════════════════════════ */

  --font-family-primary: 'Geist', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  --font-family-mono: 'Geist Mono', 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, monospace;

  /* ════════════════════════════════════════════════════════════════
     TYPOGRAPHY — SIZE SCALE (Base: 16px = 1rem)
     ════════════════════════════════════════════════════════════════ */

  --fs-display: 42px;
  --fs-h1: 32px;
  --fs-h2: 24px;
  --fs-h3: 20px;
  --fs-h4: 18px;
  --fs-base: 16px;
  --fs-body: 16px;
  --fs-small: 14px;
  --fs-xs: 12px;
  --fs-2xs: 11px;

  /* ════════════════════════════════════════════════════════════════
     TYPOGRAPHY — FONT WEIGHTS
     ════════════════════════════════════════════════════════════════ */

  --fw-regular: 400;
  --fw-medium: 500;
  --fw-semibold: 600;
  --fw-bold: 700;

  /* ════════════════════════════════════════════════════════════════
     TYPOGRAPHY — LINE HEIGHT
     ════════════════════════════════════════════════════════════════ */

  --lh-tight: 1.2;
  --lh-snug: 1.3;
  --lh-normal: 1.5;
  --lh-relaxed: 1.6;
  --lh-loose: 1.75;

  /* ════════════════════════════════════════════════════════════════
     SPACING SCALE
     ════════════════════════════════════════════════════════════════ */

  --space-0: 0;
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 20px;
  --space-6: 24px;
  --space-7: 28px;
  --space-8: 32px;
  --space-10: 40px;
  --space-12: 48px;
  --space-16: 64px;

  /* ════════════════════════════════════════════════════════════════
     BORDERS & CORNERS
     ════════════════════════════════════════════════════════════════ */

  --radius-xs: 3px;
  --radius-sm: 6px;
  --radius-md: 8px;
  --radius-lg: 12px;

  --border-width: 1px;

  /* ════════════════════════════════════════════════════════════════
     TRANSITIONS & ANIMATIONS
     ════════════════════════════════════════════════════════════════ */

  --transition-fast: all 0.15s ease;
  --transition-base: all 0.2s ease;
  --transition-slow: all 0.3s ease;

  /* ════════════════════════════════════════════════════════════════
     LAYOUT
     ════════════════════════════════════════════════════════════════ */

  --max-width-content: 1100px;
}

/* ════════════════════════════════════════════════════════════════
   RESET & BASE STYLES
   ════════════════════════════════════════════════════════════════ */

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  font-size: 16px;
  scroll-behavior: smooth;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  font-family: var(--font-family-primary);
  font-size: var(--fs-body);
  font-weight: var(--fw-regular);
  line-height: var(--lh-relaxed);
  color: var(--color-text-primary);
  background-color: var(--color-bg-primary);
}

/* ════════════════════════════════════════════════════════════════
   HEADING STYLES
   ════════════════════════════════════════════════════════════════ */

h1, .h1 {
  font-size: var(--fs-h1);
  font-weight: var(--fw-bold);
  line-height: var(--lh-snug);
  color: var(--color-text-primary);
  margin: 0;
}

h2, .h2 {
  font-size: var(--fs-h2);
  font-weight: var(--fw-bold);
  line-height: var(--lh-snug);
  color: var(--color-text-primary);
  margin: 0;
}

h3, .h3 {
  font-size: var(--fs-h3);
  font-weight: var(--fw-semibold);
  line-height: var(--lh-snug);
  color: var(--color-text-primary);
  margin: 0;
}

h4, h5, h6 {
  font-size: var(--fs-h4);
  font-weight: var(--fw-semibold);
  line-height: var(--lh-snug);
  color: var(--color-text-primary);
  margin: 0;
}

/* ════════════════════════════════════════════════════════════════
   TEXT UTILITIES
   ════════════════════════════════════════════════════════════════ */

.text-primary { color: var(--color-text-primary); }
.text-secondary { color: var(--color-text-secondary); }
.text-tertiary { color: var(--color-text-tertiary); }
.text-accent { color: var(--color-accent); }

.text-xs { font-size: var(--fs-xs); }
.text-sm { font-size: var(--fs-small); }
.text-base { font-size: var(--fs-base); }

.text-bold { font-weight: var(--fw-bold); }
.text-semibold { font-weight: var(--fw-semibold); }

/* ════════════════════════════════════════════════════════════════
   LINK STYLES
   ════════════════════════════════════════════════════════════════ */

a {
  color: var(--color-text-primary);
  text-decoration: none;
  transition: var(--transition-fast);
}

a:hover {
  color: var(--color-accent);
}

/* ════════════════════════════════════════════════════════════════
   CONTAINER & SPACING
   ════════════════════════════════════════════════════════════════ */

.container {
  max-width: var(--max-width-content);
  margin: 0 auto;
  padding: 0 var(--space-6);
}

.header {
  padding: 40px 24px;
  border-bottom: 1px solid var(--color-border-primary);
  background: var(--color-bg-primary);
  position: sticky;
  top: 0;
  z-index: 100;
}

.header-content {
  max-width: var(--max-width-content);
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header-brand {
  font-size: 20px;
  font-weight: var(--fw-bold);
  color: var(--color-text-primary);
}

.header-nav {
  display: flex;
  gap: 28px;
  list-style: none;
}

.header-nav a {
  color: var(--color-text-secondary);
  text-decoration: none;
  font-size: 14px;
  transition: var(--transition-base);
}

.header-nav a:hover {
  color: var(--color-accent);
}

/* ════════════════════════════════════════════════════════════════
   HERO SECTION
   ════════════════════════════════════════════════════════════════ */

.hero {
  max-width: 1100px;
  margin: 0 auto;
  padding: 60px 24px 40px;
  display: grid;
  grid-template-columns: 1fr 280px;
  gap: 40px;
}

.hero-text h1 {
  font-size: var(--fs-display);
  font-weight: var(--fw-bold);
  line-height: var(--lh-snug);
  margin-bottom: 16px;
}

.hero-text p {
  color: var(--color-text-secondary);
  font-size: 16px;
  line-height: var(--lh-relaxed);
  margin-bottom: 24px;
}

.hero-card {
  background: var(--color-bg-secondary);
  border: 1px solid var(--color-border-primary);
  border-radius: var(--radius-md);
  padding: 20px;
  height: fit-content;
}

.hero-card h3 {
  font-size: 13px;
  text-transform: uppercase;
  font-weight: var(--fw-bold);
  letter-spacing: 1px;
  color: var(--color-text-secondary);
  margin-bottom: 12px;
}

.hero-skills {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.hero-skill {
  font-size: 13px;
  color: var(--color-text-primary);
}

/* ════════════════════════════════════════════════════════════════
   POSTS SECTION
   ════════════════════════════════════════════════════════════════ */

.posts-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 32px;
  padding-bottom: 20px;
  border-bottom: 2px solid var(--color-accent);
}

.posts-header h2 {
  font-size: 24px;
  font-weight: var(--fw-bold);
  color: var(--color-text-primary);
}

.view-all {
  color: var(--color-accent);
  text-decoration: none;
  font-size: 14px;
  transition: var(--transition-base);
}

.view-all:hover {
  color: var(--color-accent-hover);
}

/* ════════════════════════════════════════════════════════════════
   FEATURED POSTS
   ════════════════════════════════════════════════════════════════ */

.posts-featured {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
  margin-bottom: 40px;
}

.featured-post {
  background: var(--color-bg-secondary);
  border: 1px solid var(--color-border-primary);
  border-radius: var(--radius-md);
  padding: 28px;
  display: flex;
  flex-direction: column;
  transition: var(--transition-base);
}

.featured-post:hover {
  border-color: var(--color-accent);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
}

.featured-post:first-child {
  grid-column: 1 / -1;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 32px;
  align-items: center;
}

.featured-post:first-child > * {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.featured-label {
  color: var(--color-accent);
  font-size: 12px;
  font-weight: var(--fw-bold);
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 8px;
}

.featured-title {
  font-size: 24px;
  font-weight: var(--fw-bold);
  margin-bottom: 12px;
  line-height: var(--lh-snug);
  color: var(--color-text-primary);
}

.featured-excerpt {
  color: var(--color-text-secondary);
  font-size: 14px;
  line-height: var(--lh-relaxed);
  margin-bottom: 16px;
}

.featured-date {
  color: var(--color-text-tertiary);
  font-size: 12px;
}

.featured-image {
  background: linear-gradient(135deg, var(--color-accent) 0%, var(--color-accent-hover) 100%);
  border-radius: var(--radius-md);
  min-height: 250px;
}

/* ════════════════════════════════════════════════════════════════
   POST LIST
   ════════════════════════════════════════════════════════════════ */

.posts-list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.post-item {
  background: white;
  border: 1px solid var(--color-border-primary);
  border-radius: var(--radius-sm);
  padding: 20px;
  transition: var(--transition-base);
}

.post-item:hover {
  border-color: var(--color-accent);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
}

.post-date {
  color: var(--color-text-tertiary);
  font-size: 12px;
  margin-bottom: 6px;
}

.post-title {
  font-size: 16px;
  font-weight: var(--fw-semibold);
  margin-bottom: 8px;
  color: var(--color-text-primary);
}

.post-title a {
  color: var(--color-text-primary);
  text-decoration: none;
  transition: var(--transition-base);
}

.post-title a:hover {
  color: var(--color-accent);
}

.post-tags {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
}

.tag {
  padding: 3px 8px;
  background: var(--color-bg-tertiary);
  color: var(--color-text-secondary);
  border-radius: var(--radius-xs);
  font-size: 11px;
  text-decoration: none;
  transition: var(--transition-base);
  cursor: pointer;
}

.tag:hover {
  background: var(--color-accent);
  color: white;
}

/* ════════════════════════════════════════════════════════════════
   RESPONSIVE
   ════════════════════════════════════════════════════════════════ */

@media (max-width: 900px) {
  .hero {
    grid-template-columns: 1fr;
  }

  .posts-featured {
    grid-template-columns: 1fr;
  }

  .featured-post:first-child {
    grid-template-columns: 1fr;
  }

  .featured-image {
    min-height: 200px;
  }

  .header-nav {
    gap: 16px;
  }

  .header-nav a {
    font-size: 13px;
  }
}

@media (max-width: 640px) {
  .header {
    padding: 24px 16px;
  }

  .header-content {
    flex-direction: column;
    gap: 16px;
  }

  .header-nav {
    flex-direction: column;
    gap: 8px;
  }

  .hero {
    padding: 40px 16px 24px;
  }

  .hero-text h1 {
    font-size: 32px;
  }

  .container {
    padding: 0 16px;
  }

  .posts-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 12px;
  }
}
```

3. **Jekyll 레이아웃 수정**
   - `_includes/head.html` 또는 `_layouts/default.html`에 다음 추가:
   
```html
<link rel="stylesheet" href="{{ '/assets/css/design-tokens.css' | relative_url }}">
```

4. **홈페이지 (index.md 또는 index.html) 구조 변경**
   - 헤더 네비게이션 추가
   - 히어로 섹션 추가
   - Featured 포스트 섹션 추가
   - 포스트 리스트 섹션 추가

5. **기존 스타일 제거**
   - 기존 테마의 CSS 비활성화 또는 덮어쓰기
   - Chirpy 테마의 기본 스타일 제거 (필요시)

---

## 참고 자료

### 디자인 시스템 설명
- **색상:** 파란색 액센트 (#0969da) + 뉴트럴 그레이
- **폰트:** Geist (Google Fonts에서 제공)
- **레이아웃:** 최대 1100px 너비, 반응형 (900px 브레이크포인트)
- **간격:** 4px 기반 시스템
- **상호작용:** 호버시 액센트색, 카드는 경계선 + 그림자

### 주요 클래스 및 변수
```
색상: --color-text-primary, --color-bg-secondary, --color-accent 등
타이포: --fs-h1, --fw-bold, --lh-relaxed 등
간격: --space-4, --space-6, --space-8 등
컴포넌트: .header, .hero, .featured-post, .post-item, .tag 등
```

### UI Kit 참고
더 자세한 레이아웃은 다음 파일들을 참고:
- Homepage: ui_kits/blog/index.html
- Post Detail: ui_kits/blog/post.html
- Archive: ui_kits/blog/archive.html
- About: ui_kits/blog/about.html

---

## 주의사항

1. **Git 저장소 클론** 후 작업 시작
2. **CSS 파일** 경로 확인 (assets/css/ 폴더 필요)
3. **Jekyll 빌드** 후 로컬에서 테스트
4. **이미지 플레이스홀더** (featured-image)는 그래디언트이므로 실제 이미지로 변경 가능
5. **모바일 반응성** 테스트 필수

---

**작업 완료 후:**
- 로컬 `bundle exec jekyll serve`로 테스트
- GitHub에 커밋 및 푸시
- GitHub Pages 배포 확인

