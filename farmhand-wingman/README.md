# AWS Bedrock "Farm-Hand Wingman" Application
### Tech Stack: AWS Bedrock, Large Language Models (LLMs), Generative AI Text-to-Image (Multimodal), Sequential Prompt Engineering

## Project Overview
Developed as part of the competitive Udacity AWS AI Practitioner Scholarship Challenge, this application addresses a distinct socio-technical issue within the agricultural sector: mitigating the operational friction, communication barriers, and high-risk safety hazards on New Zealand dairy farms for non-agricultural partners moving into a farming environment.

The system acts as an AI-driven, contextual lifestyle co-pilot. Rather than executing simple single-turn prompts, this architecture utilises **Sequential Agentic Orchestration** across a multi-stage pipeline. The system processes live inputs (such as specific regional farming seasons, shifting daily worker tasks, and user energy levels) to synthesise safety-focused mission briefs, highly customised gear/apparel recommendations, fatigue-aware relationship strategies, and cross-modal visual assets.

---

## Architectural & Node Pipeline Flow

As documented in the repository's `architecture-flow.png`, the system routes variable inputs through a layered inference pipeline to maintain context across multiple specialized generative tasks:

```text
 [Input Parameters] ──► (Partner's Name, Current Season, Energy Level, Partner's Tasks)
                                  │
         ┌────────────────────────┴────────────────────────┐
         ▼                                                 ▼
[Node 1: Your Mission]                       [Node 2: Post-Milking Window]
(Generates 3 practical,                      (Generates 3 low-energy,
 safety-first regional tasks)                fatigue-aware evening activities)
         │                                                 │
         └────────────────────────┬────────────────────────┘
                                  ▼
                     [Node 3: The Farm Fit Outfit]
                     (Compiles apparel safety requirements,
                      incorporating user aesthetic preferences)
                                  │
                                  ▼
                     [Node 4: The Cow Widget]
                     (Cross-Modal Text-to-Image generation
                      rendering visual interface feedback)
