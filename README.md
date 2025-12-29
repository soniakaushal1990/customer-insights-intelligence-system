# Customer Insights Intelligence System

A backend-first project that aggregates customer events into behavioral segments and uses
**retrieval-augmented generation (RAG)** to produce grounded, human-readable insights for each segment.

This project explores how **traditional analytics / ML-style segmentation** can be combined with
**embeddings + semantic retrieval + LLM summarization** to support more explainable decision-making —
while keeping outputs tied to real customer data instead of unsupported assumptions.

---

## 🎯 Goals

- Turn raw metrics into **clear, grounded insights** for non-technical stakeholders  
- Use **semantic / vector search** to bring relevant historical context into segment explanations  
- Treat LLM output as an **explainability layer**, not the source of truth  
- Apply **basic evaluation checks** to monitor groundedness and correctness of LLM summaries

---

## 🧠 High-Level Architecture

1️⃣ **Data ingestion**  
&nbsp;&nbsp;&nbsp;&nbsp;Load sample `customers` and `events` data into MongoDB.

2️⃣ **Feature aggregation & segmentation**  
&nbsp;&nbsp;&nbsp;&nbsp;Compute basic features per customer (LTV, activity, recency, tenure).  
&nbsp;&nbsp;&nbsp;&nbsp;Assign rule-based segments such as:
- High-value active
- At-risk churn
- Low-engagement new

3️⃣ **Retrieval (RAG)**  
&nbsp;&nbsp;&nbsp;&nbsp;Embed a small corpus of customer-related notes (feedback, patterns, playbooks).  
&nbsp;&nbsp;&nbsp;&nbsp;Retrieve relevant context snippets using **vector / semantic search** for each segment.

4️⃣ **LLM-generated insight summaries**  
&nbsp;&nbsp;&nbsp;&nbsp;Feed **segment metrics + retrieved snippets** to an LLM  
&nbsp;&nbsp;&nbsp;&nbsp;Generate short, grounded summaries:
- Who the segment is  
- Why they behave this way  
- What action might help

5️⃣ **Evaluation & correctness checks**  
&nbsp;&nbsp;&nbsp;&nbsp;Basic evaluation ensures the summary:
- references segment metrics or retrieved snippets
- avoids claims not supported by data
- flags potential hallucinations

6️⃣ **API exposure**  
&nbsp;&nbsp;&nbsp;&nbsp;Minimal REST API to browse segments and their insights.

---

## 🛠️ Tech Stack

| Area | Technology |
|---|---|
| Backend | **TypeScript**, Node.js (Express or Fastify) |
| Data | **MongoDB** (Atlas or local), sample JSON data |
| AI / LLM | OpenAI API (or compatible), embeddings for retrieval |
| Patterns | RAG, semantic search, grounded summarization |
| Planned | Atlas Vector Search, evaluation scoring |

---

## 🔧 API Endpoints (planned)

| Method | Endpoint | Description |
|---|---|---|
| GET | `/segments` | List segments with metrics |
| GET | `/segments/:id` | Segment details + generated insight |
| POST | `/segments/:id/refresh-insight` | Regenerate the RAG-based insight summary |

---

## 🔍 Example Insight Prompt (early draft)

