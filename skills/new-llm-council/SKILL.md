---
name: new-llm-council
description: Scaffold a new LLM Council project repository. Use when the user wants to "create a new LLM council", "start an LLM council for X", "build a council project for [domain/decision/topic]", or references Karpathy's llm-council pattern as a starting point. Walks through purpose, visibility (public/private), base template choice (Template / Grounded / Decide / Bespoke), then constructs a customized repo.
argument-hint: [optional purpose, e.g. "career decisions"]
allowed-tools: Bash, Read, Write, Edit, Glob, Grep
---

# Create a new LLM Council project

Scaffold a fresh LLM Council repository tailored to a specific purpose, based on one of three public template repos or built bespoke.

## Background

LLM Council is a deliberation pattern (Karpathy — https://github.com/karpathy/llm-council) where multiple perspectives deliberate on a question, then a chairman synthesizes. Three public templates are available:

- **LLM-Council-Template** (`danielrosehill/LLM-Council-Template`) — baseline: six personality-based system prompts, single model, three stages (perspectives → peer review → chairman synthesis). Best for: general ideation, brainstorming, multi-angle commentary.
- **LLM-Council-Grounded** (`danielrosehill/LLM-Council-Grounded`) — Template + retrieval layer (Pinecone for domain knowledge, Tavily for real-time web). Best for: factual questions, research-backed deliberations.
- **LLM-Council-Decide** (`danielrosehill/LLM-Council-Decide`) — swaps personalities for **formal decision-making frameworks** (Pros/Cons, Weighted Matrix, Pre-Mortem, 10/10/10, Regret Minimization, etc.). Best for: "should I do X?" decisions.
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
4. **Repo name** — suggest a descriptive name (Train-Case recommended, e.g. `LLM-Council-Architecture`). Confirm or take user override.
5. **Target directory** — where to create the local working copy. Default to the current working directory; confirm or take override.
6. **GitHub account/org** — which account or organization to create the repo under (e.g. the user's personal GitHub username, or a workspace org). Required for the push step.
7. **Council members** — for Bespoke, ask for 4–6 member roles. For Template/Grounded, ask whether to keep the six default personalities or customize. For Decide, ask whether to hand-pick frameworks or leave auto-select (default).

If the user's initial invocation already included some of these, pre-fill and ask only for missing items.

### Step 2 — Create repo skeleton

**For Template / Grounded / Decide**: clone from GitHub as a starting point, then remove its git history:

```bash
TEMPLATE_REPO="danielrosehill/LLM-Council-<Base>"   # Template | Grounded | Decide
DEST="<target-dir>/<RepoName>"
git clone --depth 1 "https://github.com/$TEMPLATE_REPO.git" "$DEST"
rm -rf "$DEST/.git"
cd "$DEST" && git init -b main
```

**For Bespoke**: scaffold fresh using the structure in `references/bespoke-scaffold.md`.

### Step 3 — Customize for purpose

Edit these files to reflect the council's specific purpose:

- **README.md** — replace the top-level description, "Why" section, and any example prompts with ones relevant to the stated purpose. Keep the attribution link to `karpathy/llm-council`.
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

Then create the GitHub repo using `gh` under the account/org the user specified in Step 1:

```bash
# public
gh repo create <account>/<RepoName> --public --source=. --push --description "<one-line purpose>"
# private
gh repo create <account>/<RepoName> --private --source=. --push --description "<one-line purpose>"
```

If the user prefers not to push immediately, skip this step and report the local path only.

### Step 6 — Report

Summarize in 3–5 lines:
- Repo path (local + GitHub URL, if pushed)
- Base template used
- What was customized (members/frameworks/grounding)
- What the user should do next (e.g. `cd` into repo, add `OPENROUTER_API_KEY` to `.env`, run `./start.sh`)

## Guardrails

- **Do not reuse** an existing repo name. Check `ls <target-dir> | grep -i <name>` before creating.
- **Do not push secrets** — copied `.env` files should be `.env.example` only; verify `.gitignore` covers real `.env`.
- If the user's requested purpose is sensitive (personal finance, health, legal), default to **private** even if they didn't specify — and confirm before pushing.
- If `gh` is not authenticated for the target account, stop at Step 5 and tell the user to run `gh auth login` first.
