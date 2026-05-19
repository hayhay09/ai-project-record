# Agri-Tech Operations Bot: Ingestion & Data Standardisation
### Tech Stack: n8n Automation Engine, Telegram Bot API, Google Sheets Cloud API, Webhooks, Regex Parsing, JSON, OAuth 2.0

## Project Overview
This project documents the setup of a real-time, bi-directional edge integration built to automate field data logging directly from the paddock during the high-pressure calving season. 

During calving, relying on paper notebooks or waiting until the end of the day to type up records leads to lost notes, typos, and delayed information. This project fixes that by creating an instant data link that changes raw text messages sent from a phone into clean, uniform spreadsheet rows—saving time for workers and keeping records completely accurate.

---

## How the Data Ingestion Flows
The system uses a quick, event-driven link to map data securely from the field to a cloud spreadsheet:

```text
 [Staff Input in Paddock] ──► (Telegram Client via MTProto)
                                         │
                                         ▼
                            [Telegram Bot API Servers]
                                         │  (Encrypted HTTPS Post Request)
                                         ▼
                            [Obscured n8n Webhook URL]
                                         │
                   ┌─────────────────────┴─────────────────────┐
                   ▼                                           ▼
       [Security & Authorization]                 [Data Normalization Engine]
       (Verifies Whitelisted Chat ID)             (Regex Slicing & JSON Structuring)
                   │                                           │
                   └─────────────────────┬─────────────────────┘
                                         ▼
                            [Google Sheets Cloud API]
                            (OAuth 2.0 IAM Append-Only Entry)

