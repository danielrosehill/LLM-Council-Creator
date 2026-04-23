---
name: list-council-templates
description: Show the available base templates for LLM Council projects with when-to-use guidance. Use when the user asks "what council templates are available", "which LLM council base should I use", or is deciding between Template / Grounded / Decide / Bespoke.
allowed-tools: Read
---

# List LLM Council base templates

Report the four base options Daniel maintains for new LLM Council projects, with guidance on when each fits best.

Present as a table followed by a one-paragraph recommendation if the user has already described a purpose:

| Base | Lens | Knowledge | Best for |
|---|---|---|---|
| **Template** | 6 personality-based prompts | LLM parametric only | General ideation, brainstorming, multi-angle commentary |
| **Grounded** | 6 personalities + retrieval | Pinecone + Tavily + LLM | Factual questions, research-backed deliberations, current events |
| **Decide** | Formal decision frameworks | LLM parametric | "Should I do X?" decisions with options and stakes |
| **Bespoke** | Custom roles | Configurable | Domain-specific councils (medical triage, architecture review, etc.) |

Full comparison in `../new-llm-council/references/templates.md`. Full Decide framework catalogue in `../new-llm-council/references/frameworks.md`.

When the user has stated a purpose, recommend:
- Decision with options → **Decide**
- Factual / research → **Grounded**
- Ideation / general → **Template**
- Specialized domain roles → **Bespoke**
