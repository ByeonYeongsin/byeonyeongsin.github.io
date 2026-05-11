---
layout: home
---

<style>
  .profile-section {
    text-align: center;
    padding: 40px 20px;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    border-radius: 10px;
    margin-bottom: 40px;
  }
  
  .profile-section h1 {
    font-size: 3em;
    margin: 20px 0;
    font-weight: bold;
  }
  
  .profile-section .subtitle {
    font-size: 1.3em;
    margin: 10px 0;
    opacity: 0.9;
  }
  
  .profile-section .bio {
    font-size: 1.1em;
    margin: 20px 0;
    max-width: 600px;
    margin-left: auto;
    margin-right: auto;
    line-height: 1.6;
  }
  
  .social-links {
    margin-top: 20px;
  }
  
  .social-links a {
    display: inline-block;
    margin: 0 15px;
    color: white;
    text-decoration: none;
    font-weight: bold;
  }
  
  .social-links a:hover {
    text-decoration: underline;
  }
  
  .skills-section {
    margin: 40px 0;
  }
  
  .skills-section h2 {
    font-size: 2em;
    margin-bottom: 20px;
    color: #333;
  }
  
  .skill-category {
    margin-bottom: 25px;
  }
  
  .skill-category h3 {
    font-size: 1.3em;
    color: #667eea;
    margin-bottom: 10px;
  }
  
  .skills-list {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }
  
  .skill-tag {
    background-color: #f0f0f0;
    padding: 8px 15px;
    border-radius: 20px;
    color: #333;
    font-weight: 500;
    border: 1px solid #ddd;
  }
  
  .recent-posts {
    margin: 40px 0;
  }
  
  .recent-posts h2 {
    font-size: 2em;
    margin-bottom: 20px;
    color: #333;
  }
  
  .post-preview {
    padding: 20px;
    margin-bottom: 20px;
    border-left: 4px solid #667eea;
    background-color: #f9f9f9;
    border-radius: 5px;
  }
  
  .post-preview h3 {
    margin: 0 0 10px 0;
  }
  
  .post-preview h3 a {
    color: #667eea;
    text-decoration: none;
  }
  
  .post-preview h3 a:hover {
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
</style>

<div class="profile-section">
  <h1>👋 Yeongsin Byeon</h1>
  <p class="subtitle">AI Engineer & ML Researcher</p>
  <p class="bio">
    LLMs, RAG systems, and AI applications에 열정을 가진 개발자입니다.
    <br>최신 AI 기술을 탐구하고 실제 프로젝트에 적용하는 것을 좋아합니다.
  </p>
  <div class="social-links">
    <a href="https://github.com/ByeonYeongsin">GitHub</a>
    <a href="mailto:yeongsin_byeon@kolon.com">Email</a>
  </div>
</div>

<section class="skills-section">
  <h2>🛠️ Tech Stack</h2>
  
  <div class="skill-category">
    <h3>Programming Languages</h3>
    <div class="skills-list">
      <span class="skill-tag">Python</span>
      <span class="skill-tag">JavaScript</span>
      <span class="skill-tag">SQL</span>
    </div>
  </div>
  
  <div class="skill-category">
    <h3>AI/ML Frameworks</h3>
    <div class="skills-list">
      <span class="skill-tag">PyTorch</span>
      <span class="skill-tag">TensorFlow</span>
      <span class="skill-tag">HuggingFace</span>
      <span class="skill-tag">LangChain</span>
      <span class="skill-tag">OpenAI API</span>
    </div>
  </div>
  
  <div class="skill-category">
    <h3>Specializations</h3>
    <div class="skills-list">
      <span class="skill-tag">LLM Fine-tuning</span>
      <span class="skill-tag">RAG Systems</span>
      <span class="skill-tag">Prompt Engineering</span>
      <span class="skill-tag">Vector Databases</span>
      <span class="skill-tag">NLP</span>
    </div>
  </div>
  
  <div class="skill-category">
    <h3>Tools & Platforms</h3>
    <div class="skills-list">
      <span class="skill-tag">Git</span>
      <span class="skill-tag">Docker</span>
      <span class="skill-tag">AWS</span>
      <span class="skill-tag">Jupyter</span>
      <span class="skill-tag">VS Code</span>
    </div>
  </div>
</section>

<section class="recent-posts">
  <h2>📝 Latest Posts</h2>
  {% for post in site.posts limit:6 %}
    <div class="post-preview">
      <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
      <div class="post-meta">
        {% if post.categories %}
          {% for category in post.categories %}
            <span class="post-category">{{ category }}</span>
          {% endfor %}
        {% endif %}
        <span>{{ post.date | date: "%Y년 %m월 %d일" }}</span>
      </div>
      <p>{{ post.excerpt | strip_html | truncatewords: 50 }}</p>
      <a href="{{ post.url }}" style="color: #667eea; font-weight: bold;">더 읽기 →</a>
    </div>
  {% endfor %}
  <div style="text-align: center; margin-top: 30px;">
    <a href="/yeongsin.github.io/blog/" style="background-color: #667eea; color: white; padding: 10px 30px; border-radius: 5px; text-decoration: none; font-weight: bold;">모든 포스트 보기</a>
  </div>
</section>
