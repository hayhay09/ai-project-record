# HayCrypto Hub & AH Academy Ecosystem
### Tech Stack: n8n Workflow Automation, OpenAI API, Pinecone (Vector DB), CryptoPanic API, REST APIs, JavaScript, GitHub

## Project Overview
This project records the architecture of an automated, AI-driven operations and research engine built to manage digital asset literacy, community insights, and personalised sector intelligence.

Instead of deploying generic, out-of-the-box bots, I designed a tailored automation system via n8n. The core objective was twofold: first, to establish a culturally grounded RAG safety framework for community engagement, and second, to engineer a highly personalised data pipeline that filters market noise into high-signal, styled intelligence.

---

## Technical Setup & Core Workflows
The ecosystem is driven by two primary automated pipelines orchestrated through an n8n core engine:

### 1. The "AwhiAwhi" Support & Governance RAG Agent
* **The Logic:** To eliminate the high-stakes risk of model hallucinations and legal liability in financial and digital asset contexts, I built a custom Retrieval-Augmented Generation (RAG) pipeline named **AwhiAwhi**.
* **Data Domain Restriction:** Unlike standard public AI models that pull answers broadly from the open web, the AwhiAwhi data domain was explicitly restricted. The n8n automation engine was architected to sync and query a vector database containing *only* my own verified website content, digital safety guides, and published articles.
* **Compliance Guardrails:** Hard-coded system prompt boundaries were enforced to strictly limit the agent's scope to digital literacy and educational purposes. If a query crossed into financial speculation, the model was restricted by deterministic logic to refuse the prompt, completely mitigating the risk of automated financial advice.
* **The Flow:** When a user submits a query via the interface, an n8n webhook routes the string to a **Pinecone Vector Database** for a semantic search across my curated repository (which embeds baseline Māori Tikanga principles). The retrieved context is injected into the OpenAI API prompt template as strict grounding rules, forcing a culturally safe, accurate response within a legally protected operational scope.

```text
  [User Query Input] ──► [n8n Ingestion Webhook]
                                │
                                ▼
                  [Pinecone Vector Database Search] 
                  (Queries pre-verified local articles)
                                │
                                ▼
                    [OpenAI API Context Injection]
                    (Applies strict system prompt guardrails)
                                │
                                ▼
               [Safe, Educational Response Output]
