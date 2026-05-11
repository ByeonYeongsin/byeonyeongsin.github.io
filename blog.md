---
layout: page
title: Blog
permalink: /blog/
---

<style>
  .category-nav {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    margin-bottom: 30px;
    justify-content: center;
  }
  
  .category-btn {
    padding: 8px 16px;
    border-radius: 20px;
    text-decoration: none;
    font-weight: 500;
    border: 2px solid #667eea;
    color: #667eea;
    transition: all 0.3s;
  }
  
  .category-btn:hover,
  .category-btn.active {
    background-color: #667eea;
    color: white;
  }
  
  .post-list {
    max-width: 800px;
    margin: 0 auto;
  }
  
  .post-item {
    padding: 20px;
    margin-bottom: 20px;
    border-left: 4px solid #667eea;
    background-color: #f9f9f9;
    border-radius: 5px;
  }
  
  .post-item h3 {
    margin: 0 0 10px 0;
  }
  
  .post-item h3 a {
    color: #667eea;
    text-decoration: none;
  }
  
  .post-item h3 a:hover {
    text-decoration: underline;
  }
  
  .post-meta {
    color: #666;
    font-size: 0.9em;
    margin-bottom: 10px;
  }
  
  .post-category {
    display: inline-block;
    background-color: #667eea;
    color: white;
    padding: 3px 10px;
    border-radius: 15px;
    font-size: 0.8em;
    margin-right: 5px;
  }
  
  .post-excerpt {
    color: #555;
    line-height: 1.6;
    margin: 10px 0;
  }
  
  .read-more {
    color: #667eea;
    font-weight: bold;
    text-decoration: none;
  }
  
  .read-more:hover {
    text-decoration: underline;
  }
</style>

# 📚 Blog

AI 개발, 기술 학습, 프로젝트 경험을 나누는 블로그입니다.

<div class="category-nav">
  <a href="/yeongsin.github.io/blog/" class="category-btn active">모두</a>
  <a href="#ai-development" class="category-btn">AI Development</a>
  <a href="#ai-study" class="category-btn">AI Study</a>
  <a href="#paper-review" class="category-btn">Paper Review</a>
  <a href="#vibing-coding" class="category-btn">Vibing Coding</a>
  <a href="#tools-and-tips" class="category-btn">Tools & Tips</a>
</div>

<div class="post-list">
  {% for post in site.posts %}
    <div class="post-item">
      <h3>
        <a href="{{ post.url }}">{{ post.title }}</a>
      </h3>
      <div class="post-meta">
        {% if post.categories %}
          {% for category in post.categories %}
            <span class="post-category">{{ category }}</span>
          {% endfor %}
        {% endif %}
        <span>{{ post.date | date: "%Y년 %m월 %d일" }}</span>
      </div>
      {% if post.excerpt %}
        <div class="post-excerpt">
          {{ post.excerpt | strip_html | truncatewords: 60 }}
        </div>
      {% endif %}
      <a href="{{ post.url }}" class="read-more">더 읽기 →</a>
    </div>
  {% endfor %}
</div>

---

## 📊 포스트 통계

- 🤖 **AI Development**: 실제 프로젝트 개발 경험
- 📖 **AI Study**: 학습 자료와 튜토리얼  
- 📰 **Paper Review**: 최신 논문 분석
- 🎨 **Vibing Coding**: 개발자 일상과 팁
- 🔧 **Tools & Tips**: 유용한 도구와 방법론

---

**구독하기**: RSS 피드를 통해 최신 포스트를 받아보세요!
