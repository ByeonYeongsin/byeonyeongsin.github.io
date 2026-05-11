---
layout: page
title: Projects
permalink: /projects/
---

<style>
  .project-card {
    background: #f8f9fa;
    border-left: 4px solid #667eea;
    padding: 25px;
    margin-bottom: 25px;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  }
  
  .project-card h3 {
    color: #667eea;
    margin-top: 0;
  }
  
  .project-meta {
    color: #666;
    font-size: 0.9em;
    margin: 10px 0;
  }
  
  .project-description {
    line-height: 1.6;
    margin: 15px 0;
  }
  
  .tech-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin: 15px 0;
  }
  
  .tech-tag {
    background-color: #e8eaf6;
    color: #667eea;
    padding: 5px 12px;
    border-radius: 15px;
    font-size: 0.85em;
    font-weight: 500;
  }
  
  .project-links {
    margin-top: 15px;
  }
  
  .project-links a {
    display: inline-block;
    margin-right: 15px;
    color: #667eea;
    text-decoration: none;
    font-weight: bold;
  }
  
  .project-links a:hover {
    text-decoration: underline;
  }
</style>

# 🚀 Projects & Portfolio

여기서는 제가 진행한 AI/ML 프로젝트들을 소개합니다.

---

## 핵심 프로젝트

<div class="project-card">
  <h3>🤖 Advanced RAG System for Document Analysis</h3>
  <div class="project-meta">
    <strong>2026년 1월 - 현재</strong> | 개인 프로젝트
  </div>
  <div class="project-description">
    벡터 데이터베이스와 대규모 언어모델을 결합한 고급 문서 분석 시스템입니다. 
    여러 형식의 문서를 처리하고 복잡한 쿼리에 대한 정확한 답변을 제공합니다.
  </div>
  <div class="tech-tags">
    <span class="tech-tag">Python</span>
    <span class="tech-tag">LangChain</span>
    <span class="tech-tag">OpenAI API</span>
    <span class="tech-tag">Pinecone</span>
    <span class="tech-tag">FastAPI</span>
  </div>
  <div class="project-links">
    <a href="https://github.com/ByeonYeongsin/rag-system">GitHub →</a>
    <a href="/yeongsin.github.io/ai-development/2026/05/10/rag-system/">블로그 포스트 →</a>
  </div>
</div>

<div class="project-card">
  <h3>🎯 Fine-tuned LLM for Domain-Specific Tasks</h3>
  <div class="project-meta">
    <strong>2025년 10월 - 2025년 12월</strong> | 팀 프로젝트
  </div>
  <div class="project-description">
    특정 도메인 작업을 위해 오픈소스 LLM을 파인튜닝한 프로젝트입니다. 
    QLoRA를 활용한 효율적인 파인튜닝과 최적화된 추론 시스템을 구현했습니다.
  </div>
  <div class="tech-tags">
    <span class="tech-tag">PyTorch</span>
    <span class="tech-tag">HuggingFace</span>
    <span class="tech-tag">QLoRA</span>
    <span class="tech-tag">Llama 2</span>
    <span class="tech-tag">VRAM Optimization</span>
  </div>
  <div class="project-links">
    <a href="https://github.com/ByeonYeongsin/finetuned-llm">GitHub →</a>
    <a href="/yeongsin.github.io/ai-development/2025/12/01/llm-finetuning/">블로그 포스트 →</a>
  </div>
</div>

<div class="project-card">
  <h3>💬 Multi-Turn Conversation AI with Memory</h3>
  <div class="project-meta">
    <strong>2025년 8월 - 2025년 9월</strong> | 개인 프로젝트
  </div>
  <div class="project-description">
    대화 맥락을 이해하고 장기 메모리를 활용하는 AI 채봇입니다. 
    사용자의 선호도를 학습하고 개인화된 응답을 제공합니다.
  </div>
  <div class="tech-tags">
    <span class="tech-tag">Python</span>
    <span class="tech-tag">OpenAI GPT-4</span>
    <span class="tech-tag">SQLite</span>
    <span class="tech-tag">Discord API</span>
  </div>
  <div class="project-links">
    <a href="https://github.com/ByeonYeongsin/conversational-ai">GitHub →</a>
  </div>
</div>

<div class="project-card">
  <h3>📊 AI-Powered Data Analysis Dashboard</h3>
  <div class="project-meta">
    <strong>2025년 6월 - 2025년 7월</strong> | 팀 프로젝트
  </div>
  <div class="project-description">
    자연언어 쿼리로 데이터를 분석하는 스마트 대시보드입니다. 
    사용자가 복잡한 SQL 없이도 데이터 인사이트를 얻을 수 있습니다.
  </div>
  <div class="tech-tags">
    <span class="tech-tag">Python</span>
    <span class="tech-tag">Streamlit</span>
    <span class="tech-tag">Pandas</span>
    <span class="tech-tag">Claude API</span>
    <span class="tech-tag">PostgreSQL</span>
  </div>
  <div class="project-links">
    <a href="https://github.com/ByeonYeongsin/ai-data-dashboard">GitHub →</a>
  </div>
</div>

<div class="project-card">
  <h3>🔍 Semantic Search Engine</h3>
  <div class="project-meta">
    <strong>2025년 4월 - 2025년 5월</strong> | 개인 프로젝트
  </div>
  <div class="project-description">
    임베딩 모델을 활용한 의미 기반 검색 엔진입니다. 
    키워드 검색보다 더 정확하고 컨텍스트를 이해한 검색 결과를 제공합니다.
  </div>
  <div class="tech-tags">
    <span class="tech-tag">Python</span>
    <span class="tech-tag">Sentence Transformers</span>
    <span class="tech-tag">FAISS</span>
    <span class="tech-tag">FastAPI</span>
  </div>
  <div class="project-links">
    <a href="https://github.com/ByeonYeongsin/semantic-search">GitHub →</a>
  </div>
</div>

---

## 오픈소스 기여

- **LangChain**: RAG 기능 개선 (PR #1234)
- **HuggingFace Transformers**: 한국어 토크나이저 최적화
- **Llama Index**: Vector store 통합 기능

---

## 향후 프로젝트

- 🚀 멀티모달 AI 시스템 개발
- 🧠 AI 에이전트 프레임워크
- 📡 실시간 스트리밍 처리 시스템

더 많은 프로젝트는 [GitHub](https://github.com/ByeonYeongsin)에서 확인할 수 있습니다!
