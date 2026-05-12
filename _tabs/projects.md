---
layout: page
icon: fas fa-rocket
title: Projects
order: 2
---

<style>
.proj-card {
  border: 1px solid #e2e8f0; border-radius: 12px;
  padding: 22px 24px; margin-bottom: 20px;
  transition: all 0.2s;
}
.proj-card:hover {
  border-color: #667eea;
  box-shadow: 0 6px 20px rgba(102,126,234,0.12);
  transform: translateY(-2px);
}
.proj-header { display: flex; align-items: flex-start; justify-content: space-between; gap: 12px; margin-bottom: 10px; }
.proj-title { font-size: 1.1rem; font-weight: 700; margin: 0; }
.proj-status {
  font-size: 0.75rem; padding: 3px 10px; border-radius: 12px;
  white-space: nowrap; flex-shrink: 0;
}
.status-active { background: #dcfce7; color: #166534; }
.status-done { background: #e0e7ff; color: #3730a3; }
.proj-desc { color: #4a5568; font-size: 0.9rem; line-height: 1.6; margin: 0 0 12px; }
.proj-tech { display: flex; flex-wrap: wrap; gap: 6px; margin-bottom: 12px; }
.proj-tech span {
  font-size: 0.78rem; background: #eef2ff; color: #4f46e5;
  padding: 3px 10px; border-radius: 12px; border: 1px solid #c7d2fe;
}
.proj-links a {
  font-size: 0.85rem; color: #667eea; text-decoration: none;
  margin-right: 16px; font-weight: 600;
}
.proj-links a:hover { text-decoration: underline; }
.section-label {
  font-size: 0.85rem; font-weight: 700; letter-spacing: 0.08em;
  text-transform: uppercase; color: #667eea;
  margin: 32px 0 16px; border-left: 4px solid #667eea; padding-left: 10px;
}
</style>

<div class="section-label">🔥 진행 중</div>

<div class="proj-card">
  <div class="proj-header">
    <div class="proj-title">🤖 Advanced RAG System for Document Analysis</div>
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
    <a href="/yeongsin.github.io/posts/rag-system-guide/">포스트 →</a>
  </div>
</div>

<div class="proj-card">
  <div class="proj-header">
    <div class="proj-title">🏗️ AI 엔지니어 깃블로그 (Vibe Coding)</div>
    <span class="proj-status status-active">진행 중</span>
  </div>
  <div class="proj-desc">
    Claude를 활용한 바이브코딩으로 Jekyll + Chirpy 기반 개인 기술 블로그 구축.<br>
    AI 도구만으로 블로그 기획부터 배포까지 전 과정을 경험합니다.
  </div>
  <div class="proj-tech">
    <span>Jekyll</span><span>Chirpy</span><span>GitHub Pages</span><span>Claude</span><span>Vibe Coding</span>
  </div>
  <div class="proj-links">
    <a href="https://github.com/ByeonYeongsin/yeongsin.github.io">GitHub →</a>
    <a href="/yeongsin.github.io/categories/vibe-coding/">Vibe Coding 포스트 →</a>
  </div>
</div>

<div class="section-label">✅ 완료</div>

<div class="proj-card">
  <div class="proj-header">
    <div class="proj-title">🎯 LLM Fine-tuning Pipeline</div>
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
    <div class="proj-title">💬 Multi-Turn Conversation AI</div>
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
    <div class="proj-title">🔍 Semantic Search Engine</div>
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
    <div class="proj-title">📊 AI-Powered Data Analysis Dashboard</div>
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
