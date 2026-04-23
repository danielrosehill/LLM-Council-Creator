# Bespoke council scaffold

When none of the existing templates fit, build from scratch using this structure. Mirrors the Template/Grounded convention so Daniel's tooling (Typst PDF digest, Edge-TTS podcast) can be added later.

## Directory layout

```
<RepoName>/
├── README.md
├── CLAUDE.md
├── .env.example
├── .gitignore
├── pyproject.toml
├── main.py                          # CLI entry
├── start.sh                         # convenience runner
├── backend/
│   ├── __init__.py
│   ├── config.py                    # council member definitions
│   ├── council.py                   # Stage 1/2/3 orchestration
│   ├── chairman.py                  # synthesis logic
│   └── llm.py                       # OpenRouter client wrapper
├── prompts/
│   ├── stage1_perspective.md        # per-member prompt template
│   ├── stage2_peer_review.md
│   └── stage3_chairman.md
├── templates/
│   └── digest.typ                   # Typst PDF template
└── examples/
    └── example_query.md
```

## Council member definition (backend/config.py)

Each member needs a distinct lens. Minimum 4, recommended 5–6, hard max 8.

```python
COUNCIL_MEMBERS = [
    {
        "id": "member_key",
        "name": "Display Name",
        "system_prompt": """You are a <role>. Your job is to <specific lens>.
When evaluating a question, always:
- <behaviour 1>
- <behaviour 2>
Do NOT <anti-pattern>.""",
    },
    # ...
]
```

## Guidelines for writing member prompts

- **One verb per member.** If two members both "analyze", merge them or sharpen.
- **Name the anti-pattern.** Each member should know what they're *not* doing — stops drift toward generic LLM behaviour.
- **No chairman bleed-through.** Members should not hedge or synthesize; that's the Chairman's job.
- **Ground in the purpose.** A council for medical triage should have domain-aware members (Differential Diagnosis, Red Flags, Evidence-Based Medicine), not generic personalities.

## Pipeline (standard three-stage)

1. **Stage 1 — Individual perspectives.** Each member answers the query independently with their system prompt. Responses are collected.
2. **Stage 2 — Peer review.** Each member sees all Stage 1 responses *anonymized* and ranks them, with justification.
3. **Stage 3 — Chairman synthesis.** Chairman reads all perspectives + rankings and produces the final answer.

Grounding (optional): add a pre-Stage-1 retrieval step following the Grounded template's planning agent pattern.

## Output formats

Both are optional; add whichever the user wants:

- **Typst PDF digest** — rendered from `templates/digest.typ` using `typst compile`. Show Stage 1 side-by-side, Stage 2 rankings, Stage 3 synthesis.
- **Edge-TTS podcast** — chairman writes a first-person briefing script addressed to the user; `edge-tts` converts to MP3.
