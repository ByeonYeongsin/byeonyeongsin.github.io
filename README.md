# 깃블로그

Jekyll을 기반으로 만든 개인 블로그입니다.

## 로컬에서 실행하기

### 설치 (처음 한 번만)
```bash
bundle install
```

### 로컬 서버 실행
```bash
bundle exec jekyll serve
```

`http://localhost:4000`에서 확인할 수 있습니다.

## 포스트 작성하기

`_posts` 폴더에 새로운 마크다운 파일을 만들면 됩니다.

**파일 이름 형식:** `YYYY-MM-DD-제목.md`

**파일 내용 예시:**
```markdown
---
layout: post
title: "포스트 제목"
date: 2026-05-11
categories: blog
---

여기에 본문을 작성합니다.
```

## GitHub Pages 배포

커밋을 push하면 자동으로 `https://yeongsin.github.io`에 배포됩니다.

## 커스터마이징

- `_config.yml`: 블로그 설정 (제목, 설명 등)
- `index.md`: 홈페이지
- `_posts/`: 블로그 포스트들
