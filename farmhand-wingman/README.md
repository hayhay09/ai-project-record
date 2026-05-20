# AWS Bedrock "Farm-Hand Wingman" Application
### Tech Stack: AWS Bedrock, Large Language Models (LLMs), Generative AI Text-to-Image (Multimodal), Sequential Prompt Engineering

## Project Overview
Developed as part of the competitive Udacity AWS AI Practitioner Scholarship Challenge, this application addresses a distinct socio-technical issue within the agricultural sector: mitigating the operational friction, communication barriers, and high-risk safety hazards on New Zealand dairy farms for non-agricultural partners moving into a farming environment.

The system acts as an AI-driven, contextual lifestyle co-pilot. Rather than executing simple single-turn prompts, this architecture utilises **Sequential Agentic Orchestration** across a multi-stage pipeline. The system processes live inputs (such as specific regional farming seasons, shifting daily worker tasks, and user energy levels) to synthesise safety-focused mission briefs, highly customised gear/apparel recommendations, fatigue-aware relationship strategies, and cross-modal visual assets.

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

```

## Core Execution Stages
* **Stage 1: Operational Translation (Your Mission):** Takes raw, technical daily farm schedules (Partner's tasks) and translates them into plain-language, low-barrier tasks tailored to the user's current baseline capacity. This ensures high-risk awareness and baseline operational orientation without overwhelming a non-technical user.
* **Stage 2: Fatigue Mitigation Management (The Post-Milking Window):** Processes seasonal dairy workloads (e.g., severe 6 AM / 3 PM split shifts) to generate zero-exertion, relationship-stabilising strategies tailored explicitly to address high-level operational fatigue.
* **Stage 3: Context-Aware Safety Apparel Mapping (The Farm Fit Outfit):** Dynamically consumes the outputs from Stage 1 (The Mission) and Stage 2 (The Season/Tasks) to mandate specific, head-to-toe safety gear requirements (e.g., thermal regulation, mud insulation, wet weather gear) mapped directly to user color preferences (Pink).
* **Stage 4: Cross-Modal Interface Feedback (Your Cow Widget...):** Passes the generated output from the apparel nodes into an image generation model to dynamically render a whimsical, encouraging user-interface token reflecting the active dataset.

**Data Flow Pipeline:** Input Parameters (Partner Name, Current Season, Energy Level, Partner Tasks), Node 1 (Your Mission) & Node 2 (The Post-Milking Window), Node 3 (The Farm Fit Outfit), Node 4 (Your Cow Widget Text-to-Image Generation)

## System Node Connections
As documented in the repository's core node architecture map, the system dynamically weights and maps user variables directly down through sequential processing blocks:
---

## Technical Merits & Prompt Engineering Insights
The core engineering substance of this project rests heavily on advanced prompt topology and structural constraints within cloud infrastructure:

* **Separation of Slang and Sentiment:** The prompt instructions enforce strict lexical guardrails, consciously filtering out generic masculine slang variables (mate, legend) while intentionally enforcing local New Zealand primary-sector terminology (break lines, drafting, red bands). This establishes localised, culturally accurate domain matching.
* **Deterministic Layout Control:** The inference models are bound to exact formatting rules (enforced line spacing, explicit bullet constraints, and strictly defined output counts) ensuring that the resulting data structures remain reliably scannable and highly readable for users under stress or experiencing fatigue.
* **Contextual Variable Cascading:** Stage 3 demonstrates advanced conditional generation, requiring the LLM to successfully reconcile an aesthetic color restriction ("Pink") with rugged industrial safety standards (e.g., long-sleeve protective overrides, gumboot requirements) based entirely on the task parameters pushed from the preceding nodes.

---

## Responsible AI & Governance Analysis
Operating an AI system that interfaces with heavy-industrial environments introduces distinct safety, behavioural, and operational risks. This analysis outlines how core principles were engineered directly into the pipeline.

### 1. Safety-First Context Guardrails & Physical Risk Mitigation
Generative AI models are prone to generic, idealised text generation. If an AI co-pilot blindly suggests a task without assessing the physical parameters of the environment, it risks sending a user into an active hazard zone. The orchestration architecture uses strict Contextual Variable Cascading to force physical reality onto the LLM. By routing live variables directly into Node 1 and Node 3, the model is architecturally blocked from generating out-of-context or unsafe suggestions. If the active task involves heavy paddock work, the downstream fashion node overrides generic advice and strictly mandates protective personal equipment (PPE) like steel-capped gumboots.

### 2. Lexical Integrity & Cultural Fairness
Foundational Western models often over-index on generic, aggressive, or overly hyper-masculine colloquial slang when prompted with a rural persona. This can alienate diverse users. The prompt topology implements strict linguistic boundaries. By explicitly programming negative constraints ("completely avoid masculine slang like 'mate' or 'legend'") alongside positive target parameters ("keep the vibe supportive, cutesy, and girlfriend-to-girlfriend"), the model achieves gender-inclusive alignment, making a high-risk industry welcoming to non-traditional operators.

### 3. Human Agency, Cognitive Load, & Ergonomics
Users experiencing acute exhaustion or stress (such as the fatigue associated with intense 6 AM / 3 PM split dairy milking schedules) experience a significant drop in cognitive processing capacity. Lengthy, erratic, or unstructured walls of text increase cognitive load and invite operational error. To protect human agency and mental bandwidth, the pipeline utilises Deterministic Layout Control. The prompts enforce a fixed, scannable data structure: exactly three actionable tasks, mandated empty line breaks, and a total ban on clunky syntax blocks, demonstrating ergonomic responsibility in layout design.

### 4. Transparency & Explainability via Cloud Orchestration
Monolithic, single-turn prompts operate inside an un-trackable "black box," making errors nearly impossible to diagnose. By leveraging AWS Bedrock's foundational modularity, the application splits different functional domains into independent, sequential inference steps. Because Node 1 (Physical Mission), Node 2 (Relationship Exhaustion), and Node 4 (Visual Rendering) are completely isolated, human operators can explicitly trace data transformations step-by-step, maintaining clean algorithmic accountability.

---

## Repository Documentation Review
> **With AI Assistance:** This documentation was compiled with AI assistance. The underlying architectural design, system logic, and governance frameworks represent my original work and were personally reviewed, verified, and refined.
>

