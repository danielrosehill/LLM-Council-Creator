# LLM-Council-Creator

A Claude Code plugin for scaffolding new [LLM Council](https://github.com/karpathy/llm-council) projects.

Provides two skills:

- **`new-llm-council`** — walks through purpose → visibility → base choice → customization → git init → optional GitHub push. Produces a ready-to-run council repo in the target directory of the user's choice.
- **`list-council-templates`** — quick reference of the four available bases with when-to-use guidance.

## Bases

| Base | Source | Use for |
|---|---|---|
| Template | [LLM-Council-Template](https://github.com/danielrosehill/LLM-Council-Template) | General ideation |
| Grounded | [LLM-Council-Grounded](https://github.com/danielrosehill/LLM-Council-Grounded) | Research-backed deliberation (Pinecone + Tavily) |
| Decide | [LLM-Council-Decide](https://github.com/danielrosehill/LLM-Council-Decide) | Decisions via formal frameworks |
| Bespoke | — | Custom domain-specific council |

## Install

From the `danielrosehill` marketplace:

```bash
claude plugin marketplace add danielrosehill/Claude-Code-Plugins
claude plugin install LLM-Council-Creator@danielrosehill
```

Or locally from a checkout:

```bash
claude plugin install /path/to/LLM-Council-Creator
```

## Usage

```
/LLM-Council-Creator:new-llm-council evaluate Kubernetes architecture proposals
```

The skill will ask for:

- Visibility (public/private)
- Base (Template / Grounded / Decide / Bespoke)
- Repo name
- Target directory (defaults to current working directory)
- GitHub account or organisation to push under
- Council member customisations (roles, frameworks, grounding sources)

Prerequisites: `git`, and `gh` (GitHub CLI) authenticated for the target account if pushing.

## Attribution

Council pattern originated in Andrej Karpathy's [llm-council](https://github.com/karpathy/llm-council). The three public template repos used as bases are maintained at `danielrosehill/LLM-Council-Template`, `…-Grounded`, and `…-Decide`.

## Licence

MIT.
