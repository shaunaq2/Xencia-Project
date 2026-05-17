# Xencia Technology Solutions — Internship Case Study

> **Note:** This repository contains no proprietary code. It documents the architecture, design decisions, and engineering work completed during my AI/ML internship at Xencia Technology Solutions (June 2025 – August 2025).

---

## Overview

At Xencia, I was embedded in the AI team building production-grade LLM-powered applications and retrieval infrastructure. The core challenge: enterprise clients needed to search and extract insights from massive internal document collections — fast and accurately — without hallucination or irrelevant results.

I owned the RAG pipeline end-to-end, from document ingestion and vector storage through query routing and response generation.

---

## What I Built

### RAG Pipeline (Retrieval-Augmented Generation)
Designed and implemented a full RAG pipeline to enable semantic search and question-answering over large internal document corpora:

- **Document ingestion** — chunked and embedded 10,000+ document chunks into vector stores
- **Dual vector store architecture** — used **ChromaDB** for persistent local retrieval and **FAISS** for high-speed in-memory similarity search, enabling query routing based on latency vs. accuracy tradeoffs
- **Azure OpenAI integration** — connected retrieval layer to Azure-hosted GPT models for grounded, citation-aware response generation
- **Query relevance** — tuned embedding strategies and chunk sizes to maximize retrieval precision, reducing off-topic results significantly

### LLM Application Framework (LangChain + LangGraph)
Built a modular LLM application layer using LangChain and LangGraph that allowed the team to rapidly prototype and deploy new AI features:

- Designed reusable chain components for document Q&A, summarization, and multi-step reasoning
- Used **LangGraph** to orchestrate stateful multi-step agent workflows, enabling complex pipelines that previous rule-based systems couldn't handle
- Reduced prototype-to-testable-feature iteration time by **30%**, directly accelerating the internal AI solution testing cycle

---

## Tech Stack

| Layer | Technologies |
|---|---|
| LLM & Embeddings | Azure OpenAI (GPT-4), text-embedding-ada-002 |
| Vector Stores | ChromaDB, FAISS |
| Orchestration | LangChain, LangGraph |
| Backend | Python, FastAPI |
| Infrastructure | Azure, Docker |

---

## Key Design Decisions

**Why both ChromaDB and FAISS?**
ChromaDB offered persistent storage and metadata filtering — useful for production queries that needed traceability. FAISS was used for batch similarity search jobs where raw throughput mattered more than persistence. Running both in parallel gave the flexibility to route queries appropriately.

**Why LangGraph over plain LangChain?**
Standard LangChain chains are stateless and linear. Several use cases required branching logic — for example, routing a query to a different retrieval strategy depending on document type. LangGraph's graph-based execution model handled this cleanly without hacky workarounds.

**Chunking strategy**
Naive fixed-size chunking degraded retrieval quality on long-form documents. Switched to sentence-boundary-aware chunking with overlapping windows, which meaningfully improved the relevance of top-k retrieved chunks.

---

## Impact

- Built RAG infrastructure processing **10,000+ document chunks** for semantic enterprise search
- Reduced internal AI prototype iteration time by **30%** through reusable LangChain/LangGraph components
- Delivered scalable LLM application architecture that became the foundation for subsequent client-facing AI features

---
