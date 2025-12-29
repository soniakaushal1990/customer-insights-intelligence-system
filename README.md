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



## 📝 Status & Roadmap

This roadmap reflects how the project will grow from basic customer segmentation into a practical
retrieval-augmented insights system, with grounding and evaluation as core priorities.

### Phase 1 — Foundations
- [x] Create repository and README
- [ ] Add TypeScript / Node.js backend scaffolding
- [ ] Connect to MongoDB and load sample data

### Phase 2 — Segmentation & Metrics
- [ ] Define sample customer + event datasets
- [ ] Compute basic features (LTV, activity, recency, tenure)
- [ ] Implement rule-based segmentation (e.g., high-value, at-risk, low-engagement)
- [ ] Expose `GET /segments` to view metrics only

### Phase 3 — Retrieval & Embeddings (RAG)
- [ ] Create small notes corpus for retrieval context
- [ ] Generate embeddings for notes (OpenAI embeddings)
- [ ] Store embeddings in MongoDB / Atlas Vector Search
- [ ] Implement retrieval service to fetch relevant notes per segment

### Phase 4 — Insight Generation (LLM Layer)
- [ ] Design prompt template combining metrics + retrieved context
- [ ] Integrate LLM to generate grounded segment insights
- [ ] Store insights with metadata (context used, timestamp)
- [ ] Expose `GET /segments/:id` to return segment + insight

### Phase 5 — Evaluation & Groundedness
- [ ] Add basic evaluation checks (referencing metrics/context)
- [ ] Flag potential hallucinations or unsupported claims
- [ ] Log evaluation output for refinement

### Phase 6 — Developer Experience
- [ ] Add Docker setup for backend + MongoDB
- [ ] Add GitHub Actions workflow (install, lint, test, build)
- [ ] Write short “Design & Tradeoffs” note in README


