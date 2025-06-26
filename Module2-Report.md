# Public Report – Conversational AI assistant for entrepreneurs  
*(M2 Consolidation April – June 2025)*  

## 1. Executive summary  
Independent professionals and micro‑business owners routinely lose opportunities because their communication channels (WhatsApp, e‑mail, calendar, etc.) are scattered and noisy. Our team is building an AI‑powered assistant that connects to existing channels, classifies and summarizes messages, and automates first‑contact replies, giving entrepreneurs more focus and time to solve other priorities and not losing oportunities.

---  
## 2. Problem & opportunity  
- **Information overload and small teams**: solo founders juggle dozens of leads daily and miss timely follow‑ups.  
- **Fragmented channels**: e‑mail, WhatsApp, and calendars are siloed, making context retrieval slow.  
- **High switching cost**: full CRMs/ERPs are expensive and over‑engineered for early‑stage businesses.  
- **Market gap:** an intuitive assistant, with low barriers of interaction, that listens, organizes, and responds without the complexity of a CRM.

---  
## 3. Solution overview  
| Layer | Description | Status |
|-------|-------------|--------|
| **Connectors** | Gmail (live), WhatsApp (beta), Google Calendar (planned) | ✅/🟡 |
| **ETL & Storage** | Structured DB + **Qdrant** vector DB for semantic search | ✅ |
| **Intelligence** | LLM (Gemini API) + custom NLP classifier for lead categories | ✅ |
| **Interface** | WhatsApp chatbot + web dashboard (MVP front‑end) | 🟡 |
| **Automation** | Daily summaries, smart reply suggestions, cron‑driven digests | 🟡 |

---  
## 4. Technology & architecture

#### 1. Email service
- Scheduled job that monitors IMAP every 2 minutes
- Basic classification via NLP model with semantic search
- Dual storage: PostgreSQL (structured data) + Qdrant (semantic search)
- Incremental tracking via UIDs to avoid reprocessing

#### 2. WhatsApp integration
- Evolution API as middleware for WhatsApp Business
- Real-time webhook + Redis Streams for asynchronous processing
- Flow: WhatsApp → Evolution API → Webhook → Redis Streams → Qdrant
- Consumer groups for distributed processing and fault tolerance

#### 3. Vector search system (Qdrant)
- Vector database for semantic similarity search
- SentenceTransformers 'all-MiniLM-L6-v2' for embeddings (384 dimensions)
- Unifies search between emails and messages WhatsApp
- Consumer groups for parallel processing

### Backend and APIs
- **Python 3.11+** with **FastAPI** for REST APIs
- **SQLAlchemy** for ORM with PostgreSQL
- **SentenceTransformers** for generating NLP embeddings

### Node.js
- **Evolution API** (TypeScript) for WhatsApp Business integration

### Data infrastructure
- **PostgreSQL 15**: Structured data
- **Redis 6.2**: Cache and message broker (Streams)
- **Qdrant**: Vector database for semantic search

### Orchestration
- **Docker Compose** with network host mode
- `run.sh` script for coordinated service startup

## Data streams
### Email processing
```
IMAP → Basic Classification → PostgreSQL + Qdrant (embeddings)
```

### WhatsApp processing
```
Evolution API → Webhook → Redis Streams → Qdrant (embeddings)
```

### Semantic search
```
Query → Vectorization → Qdrant → Results by Similarity
```

## Implemented patterns

- **Event-Driven Architecture**: Redis Streams for asynchronous processing
- **Database Per Service**: PostgreSQL (email), Redis (WhatsApp), Qdrant (search)
- **Consumer Groups**: Distributed processing with exactly-once delivery
- **API-First**: FastAPI with automatic Swagger documentation

---  

## 5. Sprints highlights  

| Sprint | Key deliverables |
|--------|-----------------|
| **1 – Project plan** | Problem statement, value proposition, target persona, high‑level roadmap. |
| **2 – Architecture** | ETL blueprint, MVP feature set, initial Gmail connector. |
| **3 – Scope definition** | *Is/Is Not / Does/Does Not* framing; micro‑services for e‑mail and WhatsApp. |
| **4 – POC initial development** | Qdrant integration, WhatsApp webhook, vector enrichment pipeline. |
| **5 – POC development + prepare to test** | NLP lead‑classifier, Docker orchestration, landing page (Supabase + analytics). |


---  
## 6. Next steps  

1. **POC testing** – finish WhatsApp and Gmail connections + LLM, onboard early adopters.  
2. **Dashboard v1** – KPI widgets (lead funnel, response SLA).  
3. **Implementing other connectors** – expand TAM and multi‑channel view.  
4. **Paid tier** – subscription billing, advanced automations, calendar management.  
5. Plus: other features priorization coming from POC results.  
