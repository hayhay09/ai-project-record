# HayCrypto Hub & AH Academy Ecosystem
### Tech Stack: n8n Workflow Automation, OpenAI API, Pinecone (Vector DB), CryptoPanic API, REST APIs, JavaScript, GitHub

## Project Overview
This project records the architecture of an automated, AI-driven operations and research engine built to manage digital asset literacy, community insights, and personalised sector intelligence.

Instead of deploying generic, out-of-the-box bots, I designed a tailored automation system via n8n. The core objective was twofold: first, to establish a culturally grounded RAG safety framework for community engagement, and second, to engineer a highly personalised data pipeline that filters market noise into high-signal, styled intelligence.

## Technical Setup & Core Workflows
The ecosystem is driven by two primary automated pipelines orchestrated through an n8n core engine.

### 1. The "AwhiAwhi" Support & Governance RAG Agent
* **The Logic:** To eliminate the high-stakes risk of model hallucinations and legal liability in financial and digital asset contexts, I built a custom Retrieval-Augmented Generation (RAG) pipeline named AwhiAwhi.
* **Data Domain Restriction:** Unlike standard public AI models that pull answers broadly from the open web, the AwhiAwhi data domain was explicitly restricted. The n8n automation engine was architected to sync and query a vector database containing *only* my own verified website content, digital safety guides, and published articles.
* **Compliance Guardrails:** Hard-coded system prompt boundaries were enforced to strictly limit the agent's scope to digital literacy and educational purposes. If a query crossed into financial speculation, the model was restricted by deterministic logic to refuse the prompt, completely mitigating the risk of automated financial advice.
* **The Flow:** When a user submits a query via the interface, an n8n webhook routes the string to a Pinecone Vector Database for a semantic search across my curated repository (which embeds baseline Māori Tikanga principles). The retrieved context is injected into the OpenAI API prompt template as strict grounding rules, forcing a culturally safe, accurate response within a legally protected operational scope.

**Data Flow Pipeline:** User Query Input, n8n Ingestion Webhook, Pinecone Vector Database Search, OpenAI API Context Injection, Safe Educational Response Output

### 2. Personalised News Aggregation & Style-Curation Engine
* **The Logic:** A scheduled data pipeline engineered to cut through market speculation, extract high-signal compliance and safety shifts, and format the output to match a specific structural layout and communication tone.
* **The Flow:** Scheduled n8n cron-nodes automatically query data streams from the CryptoPanic API and curated aggregators to pull the day's top sector updates. The raw text payload is pushed to an OpenAI LLM node where custom prompt logic executes three distinct steps:
  1. *Filter:* Strip out market manipulation, repetitive noise, and hyper-speculative clickbait.
  2. *Analyse:* Synthesise the core operational or regulatory impact of the news.
  3. *Style:* Re-write and format the data into a custom, highly specific aesthetic layout and tone.
* **The Output:** The n8n engine automatically compiles the final data and delivers a dual-format payload straight to my inbox via an automated email. This includes a beautifully formatted newsletter/blog layout for instant reading, alongside a clean Markdown copy block. This setup allows me to review the curated intelligence first, then seamlessly copy and paste the markdown straight into my personal website portfolio to publish verified, high-signal insights.

**Data Flow Pipeline:** CryptoPanic API & Streams, n8n Cron Trigger, OpenAI LLM Curation Node (Filter, Analyse, Style), Automated Email Delivery, Inbox Dual-Payload (Blog Layout for review, Markdown copy for website upload)

## Responsible AI & Governance Analysis
This architecture was developed with a "Privacy and Governance by Design" mindset, intentionally aligning with emerging international AI frameworks and indigenous data structures.

### 1. Mitigation of Algorithmic Harm & Misinformation (Kaitiakitanga)
Standard Large Language Models (LLMs) are notorious for "hallucinations"—generating highly confident but factually incorrect information. In a digital asset and crypto environment, a hallucinated response can result in immediate financial detriment. By deploying a strict RAG architecture, forcing the LLM to ground its reasoning only within a closed vector database of pre-verified, self-authored articles functions as a foundational guardrail. If a solution cannot be found in the verified dataset, the system safely defaults rather than guessing, upholding the principle of accuracy and consumer safety.

### 2. Algorithmic Boundary Enforcement vs. Unauthorized Advice
Automated agents interacting with users in financial or digital sectors can inadvertently cross legal boundaries by providing personalised financial advice, exposing the operator to regulatory risk. The system prompt functions as a hard deterministic barrier. By hardcoding negative constraints ("Do not under any circumstances provide financial speculation or price predictions; explicitly pivot to baseline digital literacy education"), the agent respects regulatory compliance and handles adversarial jailbreaking inputs gracefully.

### 3. Cultural Safety & Indigenous Data Grounding (Manaakitanga & Tikanga)
Global foundational models are predominantly trained on Western, English-centric internet data scrapes, resulting in a systemic bias that lacks localised cultural context or data sovereignty protections. The baseline index of the AwhiAwhi pipeline explicitly treats localised community resources as taonga (treasures requiring stewardship). By embedding Māori Tikanga values into the core prompt logic, the agent is directed to generate responses that maintain appropriate relational tones, respect community safety, and prevent the tokenisation or erasure of indigenous contexts.

### 4. Noise Filtration & Human-Aesthetic Agency
Unregulated automated data scrapers often aggregate and amplify hyper-speculative clickbait, which skews decision-making and increases user anxiety. The Personalised News Engine introduces an intentional curation and synthesis layer. By programming the LLM to act as a defensive editor—stripping out speculative market manipulation strings before formatting the final layout—the pipeline prioritises cognitive clarity. Furthermore, by keeping the final publishing step manual (requiring my personal review of the inbox markdown before uploading it to the live website), the architecture ensures a robust "human-in-the-loop" verification framework, leaving the user in complete control of the information environment.

> **With AI Assistance:** This documentation was compiled with AI assistance. The underlying architectural design, system logic, and governance frameworks represent my original work and were personally reviewed, verified, and refined.
