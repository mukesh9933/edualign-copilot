# edualign-copilot

# 📚 EduAlign Copilot: Automated Curriculum Compliance & Lesson Generation Engine

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Framework](https://img.shields.io/badge/RAG-LlamaIndex-FF4B4B.svg)](https://www.llamaindex.ai/)
[![Local LLM](https://img.shields.io/badge/Local%20LLM-Ollama%20%7C%20Llama%203.2-purple.svg)](https://ollama.ai/)
[![Interface](https://img.shields.io/badge/UI-Streamlit-orange.svg)](https://streamlit.io/)
[![Validation](https://img.shields.io/badge/Data%20Validation-Pydantic%20v2-green.svg)](https://docs.pydantic.dev/)

**EduAlign Copilot** is a privacy-first, on-premise Retrieval-Augmented Generation (RAG) system engineered to automate academic curriculum compliance auditing and dynamic remedial lesson plan generation. 

By employing **Asymmetric Vector Indexing**, **Cross-Encoder Semantic Re-ranking**, and **Skeptical Decision Heuristics**, EduAlign evaluates actual classroom lecture transcripts against institutional standards to detect hidden curriculum coverage gaps and formulate structured pedagogical interventions.

---

## 🌟 Key Features

* **🔒 100% On-Premise Execution:** Runs entirely locally via Ollama with zero external API calls or data exfiltration risks.
* **⚡ Asymmetric Dual-Vector Indexing:** Curricula and lecture transcripts are ingested into isolated embedding spaces via `nomic-embed-text`.
* **🎯 Cross-Encoder Semantic Re-Ranking:** Integrates `ms-marco-MiniLM-L-6-v2` to prioritize semantic relevance and cognitive depth over surface-level keyword matching.
* **🧠 Skeptical Compliance Auditor:** Employs constrained prompt orchestration to classify standards into `FULL`, `PARTIAL`, or `GAP` with exact source evidence.
* **📋 Schema-Enforced Remedial Planning:** Automatically generates validated JSON remedial lesson plans for flagged gaps using **Pydantic v2**.
* **📊 Comprehensive Report Exporter:** Outputs production-ready audit logs and actionable lesson plans in structured Markdown format.

---

## 🏗️ System Architecture

```text
               +-----------------------------+
               | Academic Standards (TXT/PDF)|
               +--------------+--------------+
                              |
                              v
               +-----------------------------+
               |  Teacher Lecture Transcript |
               +--------------+--------------+
                              |
                     [ Ingestion Layer ]
                              v
       +---------------------------------------------+
       |   LlamaIndex Vector Store & Embeddings      |
       |             (nomic-embed-text)              |
       +----------------------+----------------------+
                              | Top-K Candidate Chunks
                              v
       +---------------------------------------------+
       |     Cross-Encoder Semantic Re-Ranker        |
       |       (ms-marco-MiniLM-L-6-v2)              |
       +----------------------+----------------------+
                              | Top Re-Ranked Nodes
                              v
       +---------------------------------------------+
       |       Skeptical Compliance Auditor          |
       |               (Llama 3.2)                   |
       |  Verdicts: FULL | PARTIAL | GAP             |
       +----------------------+----------------------+
                              | If Verdict == PARTIAL / GAP
                              v
       +---------------------------------------------+
       |     Pydantic Structured Lesson Generator    |
       |       (Schema Validation & Fallback)        |
       +----------------------+----------------------+
                              |
                     [ Streamlit UI ]
                              |
                              v
             - Interactive Visual Audits
             - Expandable JSON Lesson Plans
             - Downloadable Markdown Report
