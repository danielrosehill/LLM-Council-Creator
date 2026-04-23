---
name: new-llm-council
description: Scaffold a new LLM Council project repository. Use when the user wants to "create a new LLM council", "start an LLM council for X", "build a council project for [domain/decision/topic]", or references Karpathy's llm-council pattern as a starting point. Walks through purpose, visibility (public/private), base template choice (Template / Grounded / Decide / Bespoke), then constructs a customized repo under ~/repos/github/my-repos/.
argument-hint: [optional purpose, e.g. "career decisions"]
allowed-tools: Bash, Read, Write, Edit, Glob, Grep
---

# Create a new LLM Council project

Scaffold a fresh LLM Council repository tailored to a specific purpose, based on one of Daniel's existing templates or built bespoke.

## Background

LLM Council is a deliberation pattern (Karpathy — https://github.com/karpathy/llm-council) where multiple perspectives deliberate on a question, then a chairman synthesizes. Daniel maintains several variants:

- **LLM-Council-Template** — baseline: six personality-based system prompts, single model, three stages (perspectives → peer review → chairman synthesis). Best for: general ideation, brainstorming, multi-angle commentary.
- **LLM-Council-Grounded** — Template + retrieval layer (Pinecone for domain knowledge, Tavily for real-time web). Best for: factual questions, research-backed deliberations.
- **LLM-Council-Decide** — swaps personalities for **formal decision-making frameworks** (Pros/Cons, Weighted Matrix, Pre-Mortem, 10/10/10, Regret Minimization, etc.). Best for: "should I do X?" decisions.
- **Bespoke** — a clean scaffold following the council pattern but with council members defined from scratch for a specific domain.

See `references/templates.md` for full comparison and `references/frameworks.md` for the Decide framework catalogue.

## Workflow

### Step 1 — Gather requirements

Ask the user (in one consolidated message) for:

1. **Purpose** — what is this council for? (one sentence; e.g. "evaluate Kubernetes architecture proposals", "help decide between job offers", "triage biomedical research questions")
2. **Visibility** — public or private GitHub repo?
3. **Base** — which of the four bases? Recommend based on purpose:
   - Decision-type question → **Decide**
   - Factual/research-backed → **Grounded**
   - General ideation → **Template**
   - None fit cleanly → **Bespoke**
4. **Repo name** — suggest a Train-Case name like `LLM-Council-<Domain>` (e.g. `LLM-Council-Architecture`). Confirm or take user override.
5. **Council members** — for Bespoke, ask for 4–6 member roles. For Template/Grounded, ask whether to keep the six default personalities or customize. For Decide, ask whether to hand-pick frameworks or leave auto-select (default).

If the user's initial invocation already included the purpose, pre-fill and ask only for missing items.

### Step 2 — Create repo skeleton

Create under `~/repos/github/my-repos/<RepoName>/`.

**For Template / Grounded / Decide**: copy from the existing local checkout as a starting point (do NOT clone from GitHub — use the local working copy):

```bash
SRC="$HOME/repos/github/my-repos/LLM-Council-<Base>"
DEST="$HOME/repos/github/my-repos/<RepoName>"
cp -r "$SRC" "$DEST"
rm -rf "$DEST/.git"
cd "$DEST" && git init -b main
```

**For Bespoke**: scaffold fresh using the structure in `references/bespoke-scaffold.md`.

### Step 3 — Customize for purpose

Edit these files to reflect the council's specific purpose:

- **README.md** — replace the top-level description, "Why" section, and any example prompts with ones relevant to the stated purpose. Keep the attribution link to karpathy/llm-council and the link back to the Awesome-LLM-Council-Projects index.
- **CLAUDE.md** (if present) — update the project summary so future Claude Code sessions understand the council's specific focus.
- **backend/config.py** or equivalent — update council member definitions if the user asked for custom personalities/roles/frameworks.
- **Typst templates** (if present, under `templates/` or `prompts/`) — update the report title and any purpose-specific headings.

For Decide with hand-picked frameworks: edit the default framework list in the config to the user's selection.

For Bespoke: write the council member system prompts based on the roles the user specified. Each member should have a distinct "lens" — avoid two members with overlapping thinking styles.

### Step 4 — Grounding sources (Grounded only)

If base is **Grounded**, ask whether the user wants to:
- Pre-configure a Pinecone index name (edit `.env.example` and config)
- Restrict Tavily to specific domains (edit the planning agent prompt)
- Skip both and leave defaults

### Step 5 — Initial commit and GitHub push

```bash
cd "$DEST"
git add -A
git commit -m "Initial scaffold: LLM Council for <purpose>"
```

Then create the GitHub repo using `gh`:

```bash
# public
gh repo create danielrosehill/<RepoName> --public --source=. --push --description "<one-line purpose>"
# private
gh repo create danielrosehill/<RepoName> --private --source=. --push --description "<one-line purpose>"
```

### Step 6 — Register in the index

Ask the user if they want to add the new repo to `~/repos/github/my-repos/Awesome-LLM-Council-Projects/README.md`. If yes, append a new entry in the appropriate category section following the existing format (stars badge, last-commit badge, one-line description, language, author link).

### Step 7 — Report

Summarize in 3–5 lines:
- Repo path (local + GitHub URL)
- Base template used
- What was customized (members/frameworks/grounding)
- What the user should do next (e.g. `cd` into repo, add `OPENROUTER_API_KEY` to `.env`, run `./start.sh`)

## Guardrails

- **Never clone from GitHub** for the base — always copy from the local working checkout so any uncommitted local improvements carry forward.
- **Do not reuse** an existing repo name. Check `ls ~/repos/github/my-repos/ | grep -i <name>` before creating.
- **Do not push secrets** — the copied `.env` files should be `.env.example` only; verify `.gitignore` covers real `.env`.
- **Train-Case naming** — enforce for both the local directory and the GitHub repo (Daniel's convention: `LLM-Council-<Domain>`, not `llm-council-domain`).
- If the user's requested purpose is sensitive (personal finance, health, legal), default to **private** even if they didn't specify.
