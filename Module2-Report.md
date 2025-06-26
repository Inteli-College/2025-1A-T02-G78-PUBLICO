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
## 4. Technology & architecture (colocar mais aqui)

Key choices  
- **Micro‑services** per connector (Docker‑compose for local dev).  
- **Qdrant** for fast similarity search across messages.  
- **Redis** queues decouple ingestion from processing.  

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
4. **Paid tier ** – subscription billing, advanced automations, calendar management.  
5. + Other features priorization coming from POC results.  

---  
## 7. Risks & mitigations (sugestão do gpt, ver se faz sentido)

| Risk | Mitigation |
|------|------------|
| Third‑party API policy changes | Maintain abstraction layer, diversify channels. |
| LLM cost spikes | Cache embeddings, fine‑tune smaller models where viable. |
| Data privacy (PII) | End‑to‑end encryption at rest & transit, GDPR‑aligned policies. |
