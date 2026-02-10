# Agent Experience Terminology Map

The AX/agent optimization space suffers from significant terminology fragmentation. This document maps how terms relate to each other.

## Core Terms

| Term | Full Name | Focus | Origin |
|------|-----------|-------|--------|
| **AX** | Agent Experience | Holistic design discipline for agent interactions | Matt Biilmann / Netlify, 2024-2025 |
| **ASO** | Agent Search Optimization | Making content discoverable by AI agents | Industry |
| **SAO** | Search Agent Optimization | Synonym for ASO | Industry |
| **AAIO** | Agentic AI Optimization | Making websites agent-ready | Industry |
| **AXO** | Agent Experience Optimization | Optimizing digital properties for AI agents | Industry |
| **GEO** | Generative Engine Optimization | Optimizing for citations in AI-generated responses | Princeton University, 2023 |
| **AEO** | Answer Engine Optimization | Optimizing for AI answer engines | Industry |
| **LLMO** | LLM Optimization | Optimizing for large language model citations | Industry |
| **LLM SEO** | LLM Search Engine Optimization | SEO adapted for LLM-driven search | Industry |

## Relationships

```
                    ┌─────────────────────────┐
                    │   Agent Experience (AX)  │  ← Broadest: design discipline
                    │   (Biilmann/Netlify)     │
                    └────────────┬────────────┘
                                 │
              ┌──────────────────┼──────────────────┐
              │                  │                   │
    ┌─────────▼────────┐  ┌─────▼──────┐  ┌────────▼────────┐
    │  ASO / SAO / AAIO │  │  Protocol  │  │  Content        │
    │  (Discovery &     │  │  Design    │  │  Standards      │
    │   Optimization)   │  │  (MCP,A2A) │  │  (llms.txt,     │
    └─────────┬────────┘  └────────────┘  │   SKILL.md)     │
              │                            └─────────────────┘
    ┌─────────▼────────┐
    │  GEO / AEO / LLMO │  ← Most specific: citation optimization
    │  / LLM SEO        │
    │  (Princeton)       │
    └──────────────────┘
```

## Usage Guide

- **AX** is the most developed as a **design discipline** -- use when discussing holistic system design for agents
- **GEO** has the strongest **academic foundation** -- use when discussing research or citing papers
- **ASO/SAO** are the most directly **analogous to traditional SEO** -- use when talking to SEO professionals
- **LLMO/LLM SEO** are most **accessible** to existing marketing teams -- use in marketing contexts
- In practice, GEO, AEO, LLMO, and LLM SEO are treated as **effectively synonymous**

## Related But Distinct

| Term | Meaning | Distinction |
|------|---------|-------------|
| **DX** (Developer Experience) | Making systems usable for developers | AX's predecessor in the UX -> DX -> AX arc |
| **SEO** (Search Engine Optimization) | Optimizing for traditional search engines | Being redefined as "Search Everywhere Optimization" |
| **MCP** (Model Context Protocol) | Protocol for agent-tool connections | Infrastructure, not optimization |
| **A2A** (Agent-to-Agent) | Protocol for inter-agent communication | Infrastructure, not optimization |
