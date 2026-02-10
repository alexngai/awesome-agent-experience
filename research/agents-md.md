# AGENTS.md

## Overview

AGENTS.md is a Markdown-based convention for giving AI coding agents project-specific instructions. It lives in the root of a repository and provides build/test commands, architecture overview, security notes, git workflows, and coding conventions.

| | |
|---|---|
| Created by | OpenAI (for Codex) |
| Governance | Agentic AI Foundation (Linux Foundation) |
| Official site | [agents.md](https://agents.md/) |
| GitHub | [agentsmd/agents.md](https://github.com/agentsmd/agents.md) |
| Adoption | 60,000+ open-source repositories |

## Supported Platforms

- OpenAI Codex
- Cursor
- Gemini CLI
- Amp
- Devin
- Jules
- And more (any tool that reads project root markdown)

## Purpose

AGENTS.md answers "who is this agent and how should it behave in this project?" It typically includes:

- **Build and test commands** -- how to run the project
- **Architecture overview** -- key directories, patterns
- **Coding conventions** -- style, naming, patterns to follow
- **Security notes** -- authentication, secrets handling
- **Git workflows** -- branching strategy, commit conventions

## Relationship to SKILL.md

| Aspect | AGENTS.md | SKILL.md |
|--------|-----------|----------|
| **Purpose** | Agent identity and global rules | Task-specific capabilities |
| **Loading** | Always loaded | On-demand, contextual |
| **Scope** | Broad, cross-task | Narrow, per-task |
| **Example** | "Our company voice is professional, escalate after 3 failures" | "How to process a refund step-by-step" |

They are complementary: AGENTS.md sets the stage, SKILL.md handles specific tasks.

## Relationship to Other Project Files

Many platforms have their own variant of project-level agent instructions:

| File | Platform |
|------|----------|
| `AGENTS.md` | Cross-platform (OpenAI standard) |
| `CLAUDE.md` | Claude Code (Anthropic) |
| `.cursorrules` | Cursor |
| `.github/copilot-instructions.md` | GitHub Copilot |

AGENTS.md is positioned as the **cross-platform standard** that all tools should support.

## Evaluation

Vercel's evaluation found that AGENTS.md with compressed documentation achieved **100% pass rates**, while skills maxed out at 79%. However, commentators attributed this gap to insufficient training data for skill-activation behavior rather than a fundamental advantage.

## Sources

- [AGENTS.md Official Site](https://agents.md/)
- [AGENTS.md Emerges as Open Standard - InfoQ](https://www.infoq.com/news/2025/08/agents-md/)
- [Vercel - AGENTS.md outperforms skills](https://vercel.com/blog/agents-md-outperforms-skills-in-our-agent-evals)
- [Skills.md vs Agents.md comparison](https://www.eesel.ai/blog/skills-md-vs-agents-md)
- [OpenAI Codex: AGENTS.md docs](https://developers.openai.com/codex/guides/agents-md/)
