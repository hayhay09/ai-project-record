# Baking App: Unstructured Content Parser & ETL Pipeline
### Tech Stack: JavaScript (Node.js), Google Gemini API, Cheerio (Scraping), Firebase Realtime Database, Firebase Auth, JSON, ETL Architecture

## Project Overview
This project records a full-stack, AI-assisted data pipeline created for a hobby web application dedicated to baking and recipe organisation. As an amateur baker, I wanted a tool that could ingest any messy, unstructured recipe webpage link from the internet, instantly clean the text, and map it into a standardised layout on a personal user dashboard and calendar.

This project was built using "Vibe Coding"—collaborating with advanced AI coding assistants to design the full-stack architecture. It highlights a modern ETL (Extract, Transform, Load) pipeline, serverless cloud functions, secure user authentication, and intelligent data mapping.

---

## How the Data Pipeline Flows
The system relies on an asynchronous serverless architecture to extract webpage markup, transform it using a Large Language Model (LLM), and load it securely into a cloud database:

```text
[User Inputs Recipe URL] -> [Firebase Auth Check] (Verifies Signed-In User Session)
                                       │
                                       ▼
                       [Netlify Serverless Cloud Function]
                                       │
            ┌──────────────────────────┴──────────────────────────┐
            ▼                                                     ▼
 [Extract: Cheerio Smarter Scraping]                  [Transform: Google Gemini API]
 (Fetches HTML & parses main containers)              (Normalises text into strict JSON schema)
            │                                                     │
            └──────────────────────────┬──────────────────────────┘
                                       ▼
                           [Load: Firebase Database]
                 (Syncs to User Profile, Dashboard, & Calendar)

```
## Detailed Pipeline Stages
Extraction (JavaScript & Cheerio): The user submits a raw URL through the application interface. A Netlify cloud function executes an optimized server-side routine using node-fetch and cheerio (a blazing-fast, lightweight alternative to BeautifulSoup/Puppeteer). Rather than spinning up a heavy browser instance, it fetches the HTML source directly and processes a prioritized list of CSS targets (e.g., [itemtype*="schema.org/Recipe"], .recipe-container, .recipe__main, .article-content) to isolate primary content and immediately discard noisy scripts, ads, and footers.

Transformation (Google Gemini API)
The remaining unstructured, whitespace-sanitised text payload is pushed to the gemini-1.5-flash-latest model. The integration logic enforces Structured Outputs via responseMimeType: "application/json". Using a strict target schema layout, the model isolates components into declarative JSON variables matching a string for recipeTitle, an array of objects for ingredients (mapping quantity, measurement, and name), and an array of strings for individual instructions.

Loading (Firebase Cloud Database): The normalized JSON payload is returned to the client application where it targets the Firebase Realtime Database API. The client routing dynamically parses the payload and appends it to the user's relational dashboard profile nodes, automatically updating their layout view and syncing it with interactive recipe calendar scheduling indices.

## Technical Security, Privacy, & Governance Analysis
Because this repository is public, no active software API keys, private database URLs, or real user data are included in this codebase. Security and responsible AI choices were implemented from day one:

1. Robust Access Control & Session Privacy
In open cloud databases, poor access control allows users to accidentally view, overwrite, or maliciously delete other people's saved data, violating core CRUD privacy rules. To resolve this, I implemented Firebase Authentication to manage user access. The cloud database relies on strict server-side rules that check the user's token before granting access. If a request does not match the active account holder's unique ID (auth.uid), the cloud database triggers an instant "Permission Denied" block, keeping personal baking dashboards completely private and secure.

2. Algorithmic Cleansing vs. Scraping Errors
Web scraping often pulls in random, messy strings of text like ads, newsletter pop-ups, or erratic styling. Trying to force this messy text directly into a mobile interface breaks the layout. The Google Gemini API is utilized purely as an intelligent data translator. By enforcing a deterministic, system-level responseSchema requirement, the pipeline locks down model inference parameters. Any errant text artifact or web junk that slips through the scraper is systematically filtered out by the schema validation layer before hitting storage, guaranteeing clean data readiness.

3. Serverless System Governance & Timeout Protection
Fetching large external websites and waiting for AI processing can cause serverless functions to hang or time out. This results in untrackable system crashes, database lag, or infinite loops that drive up API costs. I engineered explicit error-handling loops and state verification blocks within the function's execution thread. The application checks for missing parameter inputs and handles non-OK server statuses gracefully—terminating faulty processes early and relaying clean feedback arrays to the client layout rather than hanging resources or generating redundant API billing cycles.

4. Human-Centred Tech (Manaakitanga)
Technology should make real-world hobbies more enjoyable, not more tedious. By automating the extraction process, the app removes the boring chore of manually typing out long, ad-heavy recipes from blogs. It values the baker's personal time and mental energy—allowing them to focus entirely on the craft of baking, proving that AI-assisted full-stack design should always serve to enhance human hobbies.

> **With AI Assistance:** This documentation was compiled with AI assistance. The underlying architectural design, system logic, and governance frameworks represent my original work and were personally reviewed, verified, and refined.
