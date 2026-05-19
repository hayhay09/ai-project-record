# Agri-Tech Operations Bot: Ingestion & Data Standardisation
### Tech Stack: n8n Automation Engine, Telegram Bot API, Google Sheets Cloud API, Webhooks, Regex Parsing, JavaScript, JSON, OAuth 2.0

## Project Overview
This project documents the architecture of a real-time, event-driven edge integration built to automate calving log management directly from the paddock during high-pressure seasonal cycles. 

Instead of relying on generic farm management software with high cognitive barriers, this custom system creates an instant, conversational data loop via Telegram. The core objective was to streamline personal field logging for a cohort of 75 calves during a single calving season. The engine establishes a rapid data link that translates unstructured text entries into a clean, standard spreadsheet database - tracking calf ID tags, breeds, dates of birth, and evolving behavioural traits or personalities as they manifest in the field.

---

## How the Data Ingestion Flows
The application uses an asynchronous, webhook-driven architecture to securely route variable message strings from the field straight to a cloud spreadsheet repository.

```text
  [Personal Input in Paddock] -> (Telegram Client via MTProto)
                                         │
                                         ▼
                            [Telegram Bot API Servers]
                                         │  (Encrypted HTTPS POST Request)
                                         ▼
                            [Obscured n8n Webhook URL]
                                         │
                ┌────────────────────────┴────────────────────────┐
                ▼                                                 ▼
     [Security & Authorization]                       [Traffic Control Engine]
    (Verifies Whitelisted Chat ID)                   (Splits Query vs. Update Paths)
                │                                                 │
                └────────────────────────┬────────────────────────┘
                                         ▼
                            [Data Normalization Block]
                             (Regex Slicing & Age JS Calculation)
                                         │
                                         ▼
                            [Google Sheets Cloud API]
                            (OAuth 2.0 IAM Append/Update Node)
```

##  Core Execution Stages
Stage 1: Inbound Message Ingestion: The workflow triggers instantly on every text message pushed to the Telegram Bot API interface. The edge payload leverages platform-native MTProto encryption to pass tracking variables securely over cellular data lines.

Stage 2: Traffic Control Routing: An internal logical branching node parses the incoming JSON payload to determine the operator's intent. If the message matches an active context string or reply markup (e.g., updating a specific calf profile), the node routes the string to the database update path. If it contains a raw number query, it switches to a lookup path.

Stage 3: Data Extraction & Normalisation: When processing calf updates or lookups, a RegEx parsing statement isolates and extracts target numeric indices (e.g., matching a text string like "Who is 5" down to a clean integer "5"). Concurrently, a custom JavaScript execution block reads the birth timestamp values to calculate real-time baseline age metrics.

Stage 4: Automated Database Synchronization: The curated variables are mapped to an authenticated Google Sheets API configuration. Operating under strict schema constraints, the engine dynamically updates or appends a targeted line item matching columns for Tag Number, Name, Breed, Date of Birth, and Personality.

Data Flow Pipeline: Telegram Trigger Inbound Webhook, Check if Reply Logic Router, RegEx Number Extraction Node, Google Sheets OAuth 2.0 Append/Update Execution

##  Technical Merits & Architecture Insights
The architectural value of this deployment rests on robust message lifecycle handling and programmatic validation rules within the integration layer:

Bidirectional Interaction State Machine: By incorporating "Force Reply" markup headers within the chat orchestration node, the bot establishes an explicit dialogue state. If a targeted calf is found to have a missing "Personality" cell, the system automatically tags the user with a forced-input prompt, ensuring subsequent text entry is seamlessly processed as an update string rather than a clean query.

Deterministic Relational Mapping: Rather than pushing messy conversational blocks into a cell, the workflow forces loose text payloads into strict object schemas. Incoming data strings are tokenised programmatically into independent column keys (calf_id, breed_type, maternal_id), ensuring data sanitisation directly at the edge.

## Responsible AI & Governance Analysis
Operating personal edge applications interacting with core production datasets requires specific digital stewardship and data governance principles built directly into the workflow engine.

1. Data Protection & Cloud Security (Kaitiakitanga)
Manual livestock logging presents serious vulnerabilities to physical damage, lost field notes, and transcription lag, creating data debt. This system enforces data protection principles through technical isolation. Paddock communication routes through a distinct HTTPS web request to an obscured, authenticated webhook endpoint unique to the private n8n server, guaranteeing that historical performance tracking datasets remain clean and safe from interception.

2. Access Control & Strict Boundary Enforcement
Because open automation channels are exposed to public networks, leaving bot endpoints unmonitored invites structural data corruption or injection vulnerabilities. The n8n automation flow acts as an active digital firewall. The ingress logic explicitly reads the incoming message.chat.id and message.from.id parameters, validating the request against a hardcoded personal profile whitelist. If any unauthorized user attempts to converse with the bot, the workflow triggers an instantaneous termination sequence before executing any downstream database code.

3. Least Privilege Data Governance
To prevent broader storage system exposure, the cloud infrastructure applies strict identity and access management (IAM) partitioning. Rather than operating with universal administrative storage keys, the central integration token is bound tightly via OAuth 2.0 authorization codes. The n8n Google Sheets application node is explicitly scoped with restricted write-and-update privileges pointing to a single spreadsheet asset ID (11_uwORS4WRoPNhnLh6Nj6yqGMW1BlipxLtRP7g_m2p4), keeping surrounding document roots safe from unexpected modifications.

4. Cognitive Ergonomics & Human-Centred Design (Manaakitanga)
Traditional enterprise farm management tools are heavy, multi-layered, and difficult to manipulate on a mobile device while performing high-exertion field duties. This system implements an accessible, low-barrier alternative by utilizing a text-based, native instant messaging framework. Moving data collection tasks to an existing, familiar client UI removes technical friction and protects precious attention spans, ensuring that automation systems adapt to serve human workflows rather than forcing humans to adapt to technology.

## Repository Documentation Review
> **With AI Assistance:** This documentation was compiled with AI assistance. The underlying architectural design, system logic, and governance frameworks represent my original work and were personally reviewed, verified, and refined.
