# ShikshaSetu (शिक्षासेतु): AI-Enabled Vernacular Socratic Homework Companion

An AI-powered, state-constrained multimodal learning companion designed for Indian middle and secondary school students (Classes 6–10). Grounded strictly in the **NCERT Science and Mathematics curriculum** and aligned with the **National Education Policy (NEP 2020)**, ShikshaSetu guides learners through step-by-step Socratic inquiry in conversational vernacular and Hinglish dialects without spoon-feeding direct answers.

---

## 📌 Table of Contents
- [Executive Overview](#-executive-overview)
- [The Core Problem vs. The Socratic Solution](#-the-core-problem-vs-the-socratic-solution)
- [System Architecture & Data Flow](#-system-architecture--data-flow)

---

## 📖 Executive Overview

Millions of school students in Tier-2, Tier-3, and rural India face a dual barrier in STEM learning: conceptual difficulty and English language friction. Existing commercial homework helpers (e.g., Doubtnut, Brainly, Google Lens) function as solution-copying mills, exacerbating rote learning. 

**ShikshaSetu** decouples problem ingestion, curriculum vector retrieval, and dialectical synthesis into an interactive Socratic dialogue. When a student uploads a photo of a textbook problem or physics diagram, the system retrieves relevant NCERT concepts and provides bite-sized hints, culturally authentic analogies (e.g., cricket pitch friction, pressure cooker thermodynamics), and guiding questions in their mother tongue.

---

## ⚖️ The Core Problem vs. The Socratic Solution

| Dimension | Legacy Solution Apps (Doubtnut / Solvers) | General LLMs (ChatGPT / Claude) | ShikshaSetu (Dedicated Socratic RAG) |
| :--- | :--- | :--- | :--- |
| **Pedagogical Posture** | Delivers instant copy-paste answers. | Solves problems in a single turn. | **Enforces multi-turn guided self-discovery**. |
| **Curriculum Scope** | Unstructured scraping of question banks. | Unbounded global context. | **Class 6–10 NCERT/CBSE scoped vectors**. |
| **Linguistic Nuance** | Monolingual English or recorded video lectures. | Formal, literal translation. | **Conversational Hinglish / Indian regional vernacular**. |
| **Academic Integrity** | Enables exam & homework cheating. | Easily manipulated via jailbreak prompts. | **Hard-coded zero-leakage safety evaluator node**. |

---

## 🏗️ System Architecture & Data Flow

ShikshaSetu operates as a **4-Tier State-Constrained Socratic Retrieval-Augmented Generation (RAG)** pipeline:
                   ┌────────────────────────────────────────────────┐
                   │           CLIENT INGESTION TIER                │
                   │  • Next.js PWA (Camera / Audio / LaTeX)        │
                   │  • WhatsApp Webhook Connector (Twilio/Meta)    │
                   └──────────────────────┬─────────────────────────┘
                                          │ Multipart / Base64 Payload
                                          ▼
                   ┌────────────────────────────────────────────────┐
                   │           FASTAPI BACKEND GATEWAY              │
                   │  • Session State Management (Turn Counters)    │
                   │  • Zero-PII In-Memory File Preprocessor        │
                   └──────────────────────┬─────────────────────────┘
                                          │
                                          ▼
                   ┌────────────────────────────────────────────────┐
                   │          LANGFLOW ORCHESTRATION TIER           │
                   │  1. Multimodal OCR (GPT-4o Vision API)         │
                   │  2. Grade & Chapter Classifier                 │
                   └───────┬───────────────────────────────┬────────┘
                           │ Extracted Query               │ Metadata Filters
                           ▼                               ▼
   ┌──────────────────────────────────────┐  ┌──────────────────────────────┐
   │     COGNITIVE REASONING TIER         │  │   KNOWLEDGE RETRIEVAL TIER   │
   │  • OpenAI GPT-4o-mini                │  │  • DataStax Astra Vector DB  │
   │  • Pedagogical Dialogue State Engine │◄─┤  • text-embedding-3-small    │
   │  • Vernacular Analogy Injector       │  │  • NCERT Class 6-10 Vectors  │
   └──────────────────┬───────────────────┘  └──────────────────────────────┘
                      │ Candidate Socratic Hint
                      ▼
   ┌────────────────────────────────────────────────────────────────────────┐
   │                    SAFETY & ANTI-LEAK GUARDRAIL                        │
   │  • Zero-Shot Evaluator Node (Checks for Answer Leakage / Formulas)     │
   └──────────────────┬─────────────────────────────────────────────────────┘
                      │ Approved Hint
                      ▼
   ┌────────────────────────────────────────────────────────────────────────┐
   │                     MULTIMODAL OUTPUT DELIVERY                         │
   │  • Bhashini Speech / Google Cloud Indian Accent TTS                    │
   │  • Formatted LaTeX & Markdown Token Stream to PWA / WhatsApp           │
   └────────────────────────────────────────────────────────────────────────┘
