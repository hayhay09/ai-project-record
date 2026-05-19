# Baking App: Unstructured Content Parser & ETL Pipeline
### Tech Stack: Python, OpenAI API, BeautifulSoup (BS4), Firebase Realtime Database, Firebase Auth, JSON, ETL Architecture

## Project Overview
This project records a full-stack, AI-assisted data pipeline created for a hobby web application dedicated to baking and recipe organisation. As an amateur baker, I wanted a tool that could ingest any messy, unstructured recipe webpage link from the internet, instantly clean the text, and map it into a standardised layout on a personal user dashboard and calendar.

This project was built using "Vibe Coding"—collaborating with advanced AI coding assistants to design the full-stack architecture. It highlights a modern ETL (Extract, Transform, Load) pipeline, serverless cloud functions, secure user authentication, and intelligent data mapping.

---

## How the Data Pipeline Flows
The system relies on a serverless Python pipeline to extract webpage data, transform it using an LLM, and load it securely into a cloud database:

```text
[User Inputs Recipe URL] ──► [Firebase Auth Check] (Verifies Signed-In User Session)
                                       │
                                       ▼
                       [Serverless Python Cloud Function]
                                       │
            ┌──────────────────────────┴──────────────────────────┐
            ▼                                                     ▼
 [Extract: BeautifulSoup (BS4)]                       [Transform: OpenAI API]
 (Scrapes raw HTML/Unstructured text)                 (Normalises messy text into strict JSON)
            │                                                     │
            └──────────────────────────┬──────────────────────────┘
                                       ▼
                         [Load: Firebase Database]
                         (Syncs to User Profile, Dashboard, & Calendar)

