---
layout: page
icon: fas fa-pen-nib
title: Posts
order: 1
---

<style>
.cat-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 14px; margin-bottom: 40px; }
.cat-card {
  display: flex; align-items: center; gap: 12px;
  padding: 16px 18px;
  border: 1px solid #e2e8f0; border-radius: 12px;
  text-decoration: none; color: inherit;
  transition: all 0.2s;
  background: #fafafa;
}
.cat-card:hover {
  border-color: #667eea;
  background: #eef2ff;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(102,126,234,0.15);
}
.cat-icon { font-size: 1.6rem; }
.cat-info h3 { margin: 0 0 2px; font-size: 0.95rem; font-weight: 600; }
.cat-info p { margin: 0; font-size: 0.78rem; color: #718096; }
.section-title {
  font-size: 1rem; font-weight: 700; letter-spacing: 0.06em;
  text-transform: uppercase; color: #667eea;
  border-bottom: 2px solid #667eea;
  padding-bottom: 6px; margin: 0 0 18px;
}
</style>

## 📂 카테고리

<div class="cat-grid">
  <a class="cat-card" href="/yeongsin.github.io/categories/ai-development/">
    <span class="cat-icon">🤖</span>
    <div class="cat-info">
      <h3>AI Development</h3>
      <p>RAG · Fine-tuning · Agent</p>
    </div>
  </a>
  <a class="cat-card" href="/yeongsin.github.io/categories/ai-study/">
    <span class="cat-icon">📖</span>
    <div class="cat-info">
      <h3>AI Study</h3>
      <p>개념 정리 · 튜토리얼</p>
    </div>
  </a>
  <a class="cat-card" href="/yeongsin.github.io/categories/paper-review/">
    <span class="cat-icon">📰</span>
    <div class="cat-info">
      <h3>Paper Review</h3>
      <p>최신 논문 분석</p>
    </div>
  </a>
  <a class="cat-card" href="/yeongsin.github.io/categories/development/">
    <span class="cat-icon">💻</span>
    <div class="cat-info">
      <h3>Development</h3>
      <p>백엔드 · API · 아키텍처</p>
    </div>
  </a>
  <a class="cat-card" href="/yeongsin.github.io/categories/vibe-coding/">
    <span class="cat-icon">🎨</span>
    <div class="cat-info">
      <h3>Vibe Coding</h3>
      <p>개발 일상 · 삽질기</p>
    </div>
  </a>
  <a class="cat-card" href="/yeongsin.github.io/categories/tools-tips/">
    <span class="cat-icon">🔧</span>
    <div class="cat-info">
      <h3>Tools & Tips</h3>
      <p>도구 · 생산성 팁</p>
    </div>
  </a>
</div>

## 📋 전체 포스트

{% assign sorted_posts = site.posts %}
{% for post in sorted_posts %}
<div style="display:flex; align-items:flex-start; gap:12px; padding:10px 0; border-bottom:1px solid #f0f0f0;">
  <span style="font-size:0.78rem; color:#aaa; white-space:nowrap; min-width:80px; padding-top:2px;">{{ post.date | date: "%Y.%m.%d" }}</span>
  {% if post.categories.first %}<span style="font-size:0.73rem; background:#667eea; color:white; padding:2px 9px; border-radius:10px; white-space:nowrap; flex-shrink:0;">{{ post.categories.first }}</span>{% endif %}
  <div style="font-size:0.9rem;"><a href="{{ post.url | relative_url }}" style="color:inherit; text-decoration:none;">{{ post.title }}</a></div>
</div>
{% endfor %}
