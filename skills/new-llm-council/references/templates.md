# Base template comparison

Quick reference for choosing among the four scaffold bases.

## LLM-Council-Template

**Source:** `https://github.com/danielrosehill/LLM-Council-Template`
**Stack:** Python (uv) backend + frontend, OpenRouter, Typst PDF, Edge-TTS podcast
**Council members:** 6 personality-based system prompts
  - Logical Thinker, Creative Problem Solver, Pessimist, Optimist, Connecting-The-Dots Specialist, Unconventional Solutions Ideator
**Pipeline:** Stage 1 individual perspectives → Stage 2 peer review + ranking → Stage 3 chairman synthesis
**Knowledge:** LLM parametric only

**Use when:** general-purpose ideation, multi-angle commentary, brainstorming — no external facts needed.

## LLM-Council-Grounded

**Source:** `https://github.com/danielrosehill/LLM-Council-Grounded`
**Adds to Template:**
  - Planning agent (decides whether to retrieve)
  - Pinecone integration (vector search over a knowledge base)
  - Tavily integration (real-time web/news)
  - Retrieved context is injected into every Stage 1 prompt

**Use when:** factual questions, domain-specific expertise, anything where hallucination risk matters or current events are in scope.

## LLM-Council-Decide

**Source:** `https://github.com/danielrosehill/LLM-Council-Decide`
**Council members:** formal decision-making frameworks (not personalities)
**Default panel:** `pros_cons, weighted_matrix, pre_mortem, wrap, ten_ten_ten`
**Selector:** optional `--auto-select` agent picks up to 5 frameworks matched to the decision
**Full catalogue:** see `frameworks.md` (15 frameworks: Pros/Cons, Weighted Matrix, Expected Value, 10/10/10, Regret Minimization, Type-1/Type-2 Doors, Pre-Mortem, Second-Order Thinking, OODA, Cynefin, Kepner-Tregoe, SWOT, Six Thinking Hats, Munger Latticework, WRAP)

**Use when:** the question is "should I do X?" — a decision with options and stakes, not an open-ended query.

## Bespoke

No upstream — scaffold from scratch using the structure in `bespoke-scaffold.md`.

**Use when:** domain has specialized roles that don't map to personalities or generic decision frameworks (e.g. a medical triage council with Differential Diagnosis / Red Flags / Evidence-Based Medicine / Patient Preference roles).
