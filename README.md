# Aura

Aura is an AI-powered, clinic-vetted Q&A assistant for parents, caregivers, and professionals supporting children's mental health. Answers are grounded strictly in approved documents via Retrieval-Augmented Generation (RAG).

---

## Project Overview

Aura uses Flowise, OpenAI, Upstash Vector, and Supabase to provide an intelligent chatbot that retrieves and summarizes verified wellness and clinical information. The system ensures that all answers come exclusively from a controlled knowledge base.

---

## Repository Structure

```
Aura/
├─ README.md
├─ LICENSE
├─ .gitignore
├─ .env.example
├─ PRIVACY.md
├─ docs/
│  ├─ flowise-export.json
│  ├─ prompts/
│  │  ├─ system_prompt.md

```

---

## Quick Start

1. Clone the repository and navigate into it.
2. Create a `.env` file based on `.env.example`.
3. Install dependencies.
4. Run seed scripts to embed demo PDFs.
5. Optionally, launch the minimal web client for local testing.

---

## Architecture Overview

```
User (Bubble Chat UI) → Bubble API Connector → Flowise Agent
Flowise Agent → OpenAI Embeddings → Upstash Vector (for retrieval)
Flowise Agent → OpenAI Chat Model (for generation)
Flowise Agent → Supabase (for logs, metadata, and optional user management)
```

### Key Components

* **OpenAI:** Generates embeddings and model responses.
* **Upstash Vector:** Stores document embeddings for semantic search.
* **Supabase:** Handles backend data such as logs or user sessions.
* **Flowise:** Orchestrates the RAG pipeline.

---

## Knowledge Prompt

```
You are Aura, a knowledge-grounded assistant. Answer only using the provided knowledge base excerpts. If the answer is not present or insufficient, reply: "I don’t have enough information in my knowledge base to answer that." Keep responses clear, compassionate, and concise for caregivers. When helpful, cite the source title and section. Do not use external sources.
```

---

## Environment Variables

```
FLOWISE_API_URL="https://your-flowise.example.com/api/v1/prediction"
FLOWISE_API_KEY="changeme"
OPENAI_API_KEY="sk-..."
EMBEDDING_MODEL="text-embedding-3-small"
CHAT_MODEL="gpt-4o-mini"
UPSTASH_VECTOR_REST_URL="https://...upstash.io"
UPSTASH_VECTOR_REST_TOKEN="..."
SUPABASE_URL="https://xyzcompany.supabase.co"
SUPABASE_ANON_KEY="..."
```
---

## Chunking and Metadata

* Chunk size: 700–900 tokens
* Overlap: 100–150 tokens
* Metadata: `{ source_title, category, clinic, page_start, page_end }`

---

## License

TBD

## Test Queries

```
Q: How can I support my child’s bedtime anxiety?
A: Provide evidence-based steps [Source: Clinic Sleep Guide, p. 3]

Q: What is Spider-Man’s birthday?
A: I don’t have enough information in my knowledge base to answer that.
```
