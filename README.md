# LLM-Council-Creator

A Claude Code plugin for scaffolding new [LLM Council](https://github.com/karpathy/llm-council) projects.

Provides two skills:

- **`new-llm-council`** — walks through purpose → visibility → base choice → customization → git init → GitHub push. Produces a ready-to-run council repo under `~/repos/github/my-repos/`.
- **`list-council-templates`** — quick reference of the four available bases with when-to-use guidance.

## Bases

| Base | Source | Use for |
|---|---|---|
| Template | [LLM-Council-Template](https://github.com/danielrosehill/LLM-Council-Template) | General ideation |
| Grounded | [LLM-Council-Grounded](https://github.com/danielrosehill/LLM-Council-Grounded) | Research-backed deliberation (Pinecone + Tavily) |
| Decide | [LLM-Council-Decide](https://github.com/danielrosehill/LLM-Council-Decide) | Decisions via formal frameworks |
| Bespoke | — | Custom domain-specific council |

Index of related projects: [Awesome-LLM-Council-Projects](https://github.com/danielrosehill/Awesome-LLM-Council-Projects).

## Install

Private plugin — install from Daniel's private Claude Code marketplace, or add locally:

```bash
claude plugin install ~/repos/github/my-repos/LLM-Council-Creator
```

## Usage

```
/LLM-Council-Creator:new-llm-council evaluate Kubernetes architecture proposals
```

Then answer the clarifying questions (visibility, base, custom members).
