---
layout: page
icon: fas fa-rocket
title: Projects
order: 2
---

<style>
.proj-card {
  border: 1px solid var(--border-color, #d0d7de);
  border-radius: 6px;
  padding: 20px 22px;
  margin-bottom: 16px;
  transition: border-color 0.15s;
}
.proj-card:hover {
  border-color: var(--label-color, #8b949e);
}
.proj-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 12px;
  margin-bottom: 8px;
}
.proj-title {
  font-size: 1rem;
  font-weight: 700;
  margin: 0;
  color: var(--heading-color, #1f2328);
}
.proj-status {
  font-size: 0.72rem;
  padding: 2px 9px;
  border-radius: 4px;
  white-space: nowrap;
  flex-shrink: 0;
  font-weight: 500;
  border: 1px solid;
}
.status-active {
  background: #f0fdf4;
  color: #166534;
  border-color: #bbf7d0;
}
.status-done {
  background: var(--card-bg, #f6f8fa);
  color: var(--label-color, #57606a);
  border-color: var(--border-color, #d0d7de);
}
.proj-desc {
  color: var(--label-color, #57606a);
  font-size: 0.87rem;
  line-height: 1.6;
  margin: 0 0 12px;
}
.proj-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
  margin-bottom: 12px;
}
.proj-tech span {
  font-size: 0.75rem;
  background: var(--card-bg, #f6f8fa);
  color: var(--label-color, #57606a);
  border: 1px solid var(--border-color, #d0d7de);
  padding: 2px 9px;
  border-radius: 4px;
}
.proj-links a {
  font-size: 0.83rem;
  color: var(--label-color, #57606a);
  text-decoration: none;
  margin-right: 14px;
}
.proj-links a:hover { text-decoration: underline; }

.sec-label {
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 0.09em;
  text-transform: uppercase;
  color: var(--label-color, #57606a);
  border-bottom: 1px solid var(--border-color, #d0d7de);
  padding-bottom: 6px;
  margin: 28px 0 14px;
}
.sec-label:first-of-type { margin-top: 0; }
</style>

<div class="sec-label">진행 중</div>

<div class="proj-card">
  <div class="proj-header">
    <div class="proj-title">Advanced RAG System for Document Analysis</div>
    <span class="proj-status status-active">진행 중</span>
  </div>
  <div class="proj-desc">
    벡터 데이터베이스와 LLM을 결합한 고급 문서 분석 시스템.<br>
    하이브리드 검색(BM25 + Vector), Reranking, 멀티홉 추론을 지원합니다.
  </div>
  <div class="proj-tech">
    <span>Python</span><span>LangChain</span><span>OpenAI API</span><span>Pinecone</span><span>FastAPI</span>
  </div>
  <div class="proj-links">
    <a href="https://github.com/ByeonYeongsin/rag-system">GitHub →</a>
    <a href="{{ '/posts/rag-system-guide/' | relative_url }}">포스트 →</a>
  </div>
</div>

<div class="proj-card">
  <div class="proj-header">
    <div class="proj-title">AI 엔지니어 깃블로그 (Vibe Coding)</div>
    <span class="proj-status status-active">진행 중</span>
  </div>
  <div class="proj-desc">
    Claude를 활용한 바이브코딩으로 Jekyll + Chirpy 기반 개인 기술 블로그 구축.<br>
    AI 도구만으로 블로그 기획부터 배포까지 전 과정을 경험합니다.
  </div>
  <div class="proj-tech">
    <span>Jekyll</span><span>Chirpy</span><span>GitHub Pages</span><span>Claude</span>
  </div>
  <div class="proj-links">
    <a href="https://github.com/ByeonYeongsin/yeongsin.github.io">GitHub →</a>
    <a href="{{ '/categories/vibe-coding/' | relative_url }}">Vibe Coding 포스트 →</a>
  </div>
</div>

<div class="sec-label">완료</div>

<div class="proj-card">
  <div class="proj-header">
    <div class="proj-title">LLM Fine-tuning Pipeline</div>
    <span class="proj-status status-done">완료</span>
  </div>
  <div class="proj-desc">
    QLoRA를 활용한 효율적인 도메인 특화 LLM 파인튜닝 파이프라인.<br>
    13B 모델을 8GB GPU에서 학습 가능하도록 최적화했습니다.
  </div>
  <div class="proj-tech">
    <span>PyTorch</span><span>HuggingFace</span><span>QLoRA</span><span>Llama 2</span><span>WandB</span>
  </div>
  <div class="proj-links">
    <a href="https://github.com/ByeonYeongsin">GitHub →</a>
  </div>
</div>

<div class="proj-card">
  <div class="proj-header">
    <div class="proj-title">Multi-Turn Conversation AI</div>
    <span class="proj-status status-done">완료</span>
  </div>
  <div class="proj-desc">
    장기 메모리와 개인화 기능을 갖춘 AI 챗봇.<br>
    사용자의 선호도와 이전 대화를 기억하여 개인화된 응답을 제공합니다.
  </div>
  <div class="proj-tech">
    <span>Python</span><span>GPT-4</span><span>LangGraph</span><span>SQLite</span>
  </div>
  <div class="proj-links">
    <a href="https://github.com/ByeonYeongsin">GitHub →</a>
  </div>
</div>

<div class="proj-card">
  <div class="proj-header">
    <div class="proj-title">Semantic Search Engine</div>
    <span class="proj-status status-done">완료</span>
  </div>
  <div class="proj-desc">
    임베딩 기반 의미론적 검색 엔진. 키워드 매칭 대신 문장의 의미를 이해해 검색합니다.
  </div>
  <div class="proj-tech">
    <span>Python</span><span>FAISS</span><span>Sentence Transformers</span><span>FastAPI</span>
  </div>
  <div class="proj-links">
    <a href="https://github.com/ByeonYeongsin">GitHub →</a>
  </div>
</div>

<div class="proj-card">
  <div class="proj-header">
    <div class="proj-title">AI-Powered Data Analysis Dashboard</div>
    <span class="proj-status status-done">완료</span>
  </div>
  <div class="proj-desc">
    자연어 쿼리로 데이터를 분석하는 스마트 대시보드. SQL 없이도 데이터 인사이트를 얻습니다.
  </div>
  <div class="proj-tech">
    <span>Streamlit</span><span>Pandas</span><span>Claude API</span><span>PostgreSQL</span>
  </div>
  <div class="proj-links">
    <a href="https://github.com/ByeonYeongsin">GitHub →</a>
  </div>
</div>
