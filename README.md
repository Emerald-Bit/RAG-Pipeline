# UK Parliamentary Retrieval-Augmented Generation API 
## The Accountability Tracker

**The Problem**

In an age where political transparency is increasingly shaping public discourse, staying informed about parliamentary proceedings is more critical than ever. However, tracking political accountability within the UK is notoriously difficult. This is largely due to the sheer volume of dense, scattered parliamentary data that is produced on a weekly basis. For constituents and journalists alike, there is a pressing need for a fast, reliable method to cut through the noise and analyse exactly what Members of Parliament are doing and saying.

**The Solution**

To address this hurdle, I have developed an automated, scalable Retrieval-Augmented Generation (RAG) API. This system is designed to ingest weekly UK Parliament data and provide highly accurate, hallucination-free answers. Furthermore, these responses are backed by verifiable source links, ensuring that the information remains objective and entirely reliable.

**Core Tech Stack**

- **AI/Data:** LangChain, OpenAI (gpt-4o-mini, text-embedding-3-small), Pinecone.
- **Backend:** Python, FastAPI, SQLite (Memory).
- **Orchestration & Infra:** Apache Airflow, Docker, Azure Container Registry/Apps.
- **Observability & Eval:** Prometheus, Grafana, Evidently AI.

**Key Features & Engineering Justifications**

- **Automated Data Pipeline:** An Airflow DAG routinely scrapes the UK Parliament API, vectorises Written Ministerial Statements, Written Questions, and EDMs, and pushes them to Pinecone, ensuring the AI's knowledge base is never stale.
- **Optimised Chunking Strategy:** Implemented sentence-aware text splitting (400–600 tokens). This prevents semantic meaning from being violently cut in half between chunks, maximising retrieval accuracy while keeping memory demands low.
- **Robust Evaluation:** Utilised Evidently AI's "LLM-as-a-judge" framework to evaluate the retriever's semantic similarity and ensure high-quality contextual matches before pushing to production.
- **Production-Grade API:** Built with FastAPI, secured via SlowAPI rate-limiting (preventing token-drain attacks), ans strict Pydantic payload validation.
- **Full Observability:** Instrumented with custom LangChain callbacks feeding into Prometheus and Grafana to track LLM latency, Vector DB search times, and exact token consumption in real-time.
