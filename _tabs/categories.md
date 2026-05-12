---
layout: page
icon: fas fa-pen-nib
title: POSTS
order: 1
---

<style>
/* ── 최상단 카테고리 카드 ── */
.cat-section {
  border: 1px solid var(--border-color, #d0d7de);
  border-radius: 6px;
  margin-bottom: 10px;
  overflow: hidden;
}

/* 최상단 폴더 헤더 행 */
.cat-l1 {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 12px 16px;
  background: var(--card-bg, #f6f8fa);
  font-size: 0.97rem;
  font-weight: 700;
  color: var(--heading-color, #1f2328);
  border-bottom: 1px solid var(--border-color, #d0d7de);
}
.cat-l1.empty { border-bottom: none; }
.cat-l1 a {
  color: inherit;
  text-decoration: none;
}
.cat-l1 a:hover { text-decoration: underline; }

/* 카드 내부 콘텐츠 영역 */
.cat-body {
  padding: 4px 0 6px;
}

/* ── 2단계 서브폴더 행 ── */
.cat-l2 {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 7px 16px 7px 40px;
  font-size: 0.88rem;
  font-weight: 600;
  color: var(--text-color, #24292f);
  border-top: 1px solid var(--border-color, #eaecef);
  margin-top: 4px;
}
.cat-l2:first-child { border-top: none; margin-top: 0; }
.cat-l2 a {
  color: inherit;
  text-decoration: none;
}
.cat-l2 a:hover { text-decoration: underline; }

/* 2단계 서브폴더 내부 */
.cat-l2-body { padding-bottom: 2px; }

/* ── 3단계 서브폴더 행 ── */
.cat-l3 {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 6px 16px 6px 64px;
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--text-color, #24292f);
  border-top: 1px solid var(--border-color, #f0f0f0);
  margin-top: 2px;
}
.cat-l3 a {
  color: inherit;
  text-decoration: none;
}
.cat-l3 a:hover { text-decoration: underline; }

/* ── 파일(포스트) 행 ── */
.file-row {
  display: flex;
  align-items: baseline;
  gap: 10px;
  padding: 5px 16px;
  font-size: 0.86rem;
  color: var(--text-color, #24292f);
}
.file-row:hover {
  background: var(--hover-bg, rgba(0,0,0,0.03));
}
.file-row .ftitle {
  flex: 1;
  min-width: 0;
}
.file-row .ftitle a {
  color: inherit;
  text-decoration: none;
}
.file-row .ftitle a:hover { text-decoration: underline; }
.file-row .fdate {
  font-size: 0.75rem;
  color: var(--label-color, #888);
  white-space: nowrap;
  flex-shrink: 0;
}

/* 들여쓰기 */
.fi1 { padding-left: 40px; }
.fi2 { padding-left: 64px; }
.fi3 { padding-left: 88px; }

/* ── 아이콘 ── */
.ico-f { color: #e5a430; margin-right: 2px; }
.ico-d { color: var(--label-color, #bbb); font-size: 0.82em; margin-right: 2px; }

/* ── 포스트 수 배지 ── */
.cnt {
  font-size: 0.72rem;
  font-weight: 400;
  color: var(--label-color, #888);
  background: var(--main-bg, #fff);
  border: 1px solid var(--border-color, #d8d8d8);
  border-radius: 10px;
  padding: 0px 7px;
  margin-left: 2px;
}
</style>

{% comment %} ── AI Development ───────────────────────────── {% endcomment %}
{% assign ai_dev = site.posts | where_exp: "p", "p.categories[0] == 'AI Development'" | sort: "date" | reverse %}
<div class="cat-section">
  <div class="cat-l1{% if ai_dev.size == 0 %} empty{% endif %}">
    <i class="fas fa-folder-open ico-f"></i>
    <a href="{{ '/categories/ai-development/' | relative_url }}">AI Development</a>
    <span class="cnt">{{ ai_dev.size }}</span>
  </div>
  {% if ai_dev.size > 0 %}
  <div class="cat-body">
    {% for post in ai_dev %}
    <div class="file-row fi1">
      <i class="far fa-file-alt ico-d"></i>
      <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
      <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
    </div>
    {% endfor %}
  </div>
  {% endif %}
</div>

{% comment %} ── AI Study ────────────────────────────────── {% endcomment %}
{% assign ai_study = site.posts | where_exp: "p", "p.categories[0] == 'AI Study'" | sort: "date" | reverse %}
<div class="cat-section">
  <div class="cat-l1{% if ai_study.size == 0 %} empty{% endif %}">
    <i class="fas fa-folder-open ico-f"></i>
    <a href="{{ '/categories/ai-study/' | relative_url }}">AI Study</a>
    <span class="cnt">{{ ai_study.size }}</span>
  </div>
  {% if ai_study.size > 0 %}
  <div class="cat-body">
    {% for post in ai_study %}
    <div class="file-row fi1">
      <i class="far fa-file-alt ico-d"></i>
      <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
      <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
    </div>
    {% endfor %}
  </div>
  {% endif %}
</div>

{% comment %} ── Paper Review ─────────────────────────────── {% endcomment %}
{% assign papers = site.posts | where_exp: "p", "p.categories[0] == 'Paper Review'" | sort: "date" | reverse %}
<div class="cat-section">
  <div class="cat-l1{% if papers.size == 0 %} empty{% endif %}">
    <i class="fas fa-folder-open ico-f"></i>
    <a href="{{ '/categories/paper-review/' | relative_url }}">Paper Review</a>
    <span class="cnt">{{ papers.size }}</span>
  </div>
  {% if papers.size > 0 %}
  <div class="cat-body">
    {% for post in papers %}
    <div class="file-row fi1">
      <i class="far fa-file-alt ico-d"></i>
      <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
      <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
    </div>
    {% endfor %}
  </div>
  {% endif %}
</div>

{% comment %} ── Development ──────────────────────────────── {% endcomment %}
{% assign dev = site.posts | where_exp: "p", "p.categories[0] == 'Development'" | sort: "date" | reverse %}
<div class="cat-section">
  <div class="cat-l1{% if dev.size == 0 %} empty{% endif %}">
    <i class="fas fa-folder-open ico-f"></i>
    <a href="{{ '/categories/development/' | relative_url }}">Development</a>
    <span class="cnt">{{ dev.size }}</span>
  </div>
  {% if dev.size > 0 %}
  <div class="cat-body">
    {% for post in dev %}
    <div class="file-row fi1">
      <i class="far fa-file-alt ico-d"></i>
      <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
      <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
    </div>
    {% endfor %}
  </div>
  {% endif %}
</div>

{% comment %} ── Vibe Coding (3단계 계층) ────────────────── {% endcomment %}
{% assign vibe_direct   = site.posts | where_exp: "p", "p.categories[0] == 'Vibe Coding' and p.categories[1] != 'AI Product Builder'" | sort: "date" | reverse %}
{% assign apb_direct    = site.posts | where_exp: "p", "p.categories.last == 'AI Product Builder'" | sort: "date" | reverse %}
{% assign gitblog       = site.posts | where_exp: "p", "p.categories.last == '깃블로그 바이브코딩'" | sort: "date" | reverse %}
{% assign vibe_total    = site.categories['Vibe Coding'] %}
{% assign apb_total     = site.categories['AI Product Builder'] %}
{% assign gitblog_total = site.categories['깃블로그 바이브코딩'] %}

<div class="cat-section">
  <div class="cat-l1">
    <i class="fas fa-folder-open ico-f"></i>
    <a href="{{ '/categories/vibe-coding/' | relative_url }}">Vibe Coding</a>
    <span class="cnt">{{ vibe_total.size }}</span>
  </div>
  <div class="cat-body">

    {% comment %} Vibe Coding 직속 포스트 {% endcomment %}
    {% for post in vibe_direct %}
    <div class="file-row fi1">
      <i class="far fa-file-alt ico-d"></i>
      <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
      <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
    </div>
    {% endfor %}

    {% comment %} AI Product Builder 서브폴더 {% endcomment %}
    <div class="cat-l2">
      <i class="fas fa-folder-open ico-f"></i>
      <a href="{{ '/categories/ai-product-builder/' | relative_url }}">AI Product Builder</a>
      <span class="cnt">{{ apb_total.size }}</span>
    </div>
    <div class="cat-l2-body">

      {% comment %} AI Product Builder 직속 포스트 {% endcomment %}
      {% for post in apb_direct %}
      <div class="file-row fi2">
        <i class="far fa-file-alt ico-d"></i>
        <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
        <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
      </div>
      {% endfor %}

      {% comment %} 깃블로그 바이브코딩 서브서브폴더 {% endcomment %}
      <div class="cat-l3">
        <i class="fas fa-folder ico-f"></i>
        <span>깃블로그 바이브코딩</span>
        <span class="cnt">{{ gitblog_total.size }}</span>
      </div>
      {% for post in gitblog %}
      <div class="file-row fi3">
        <i class="far fa-file-alt ico-d"></i>
        <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
        <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
      </div>
      {% endfor %}

    </div>
  </div>
</div>

{% comment %} ── Tools & Tips ─────────────────────────────── {% endcomment %}
{% assign tools = site.posts | where_exp: "p", "p.categories[0] == 'Tools & Tips'" | sort: "date" | reverse %}
<div class="cat-section">
  <div class="cat-l1{% if tools.size == 0 %} empty{% endif %}">
    <i class="fas fa-folder-open ico-f"></i>
    <a href="{{ '/categories/tools-tips/' | relative_url }}">Tools &amp; Tips</a>
    <span class="cnt">{{ tools.size }}</span>
  </div>
  {% if tools.size > 0 %}
  <div class="cat-body">
    {% for post in tools %}
    <div class="file-row fi1">
      <i class="far fa-file-alt ico-d"></i>
      <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
      <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
    </div>
    {% endfor %}
  </div>
  {% endif %}
</div>
