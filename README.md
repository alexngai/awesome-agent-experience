# Awesome Agent Experience (AX)

A curated collection of standards, protocols, and best practices for making technology systems accessible and usable by AI agents.

**Agent Experience (AX)** is to AI agents what User Experience (UX) is to humans and Developer Experience (DX) is to developers. As AI agents become first-class participants in digital ecosystems, the systems they interact with need to be designed with agents in mind.

> "We are going from the age of product-led growth to the age of agent-led growth." -- Sonya Huang, Sequoia Capital

---

## Contents

- [The AX Landscape](#the-ax-landscape)
- [Content Discovery Standards](#content-discovery-standards)
- [Agent Instruction Files](#agent-instruction-files)
- [Agent Communication Protocols](#agent-communication-protocols)
- [Discovery Mechanisms](#discovery-mechanisms)
- [Search & Visibility Optimization](#search--visibility-optimization)
- [Governance & Standards Bodies](#governance--standards-bodies)
- [Awesome Lists & Community Resources](#awesome-lists--community-resources)
- [Research & Further Reading](#research--further-reading)

---

## The AX Landscape

The Agent Experience ecosystem is organized around a fundamental question: **how do agents discover, understand, and interact with services?**

```
                    ┌─────────────────────────────┐
                    │   CONTENT & DISCOVERY        │
                    │   llms.txt, SKILL.md,        │
                    │   agents.json, NLWeb         │
                    └──────────────┬──────────────┘
                                   │
          ┌────────────────────────┼────────────────────────┐
          │                        │                        │
┌─────────▼─────────┐   ┌─────────▼─────────┐   ┌─────────▼─────────┐
│  Agent <-> Tools   │   │  Agent <-> Agent   │   │  Agent <-> Web    │
│  MCP (Anthropic)   │   │  A2A (Google)      │   │  NLWeb (Microsoft)│
└─────────┬─────────┘   └─────────┬─────────┘   └─────────┬─────────┘
          │                        │                        │
          └────────────────────────┼────────────────────────┘
                                   │
                    ┌──────────────▼──────────────┐
                    │   GOVERNANCE                 │
                    │   Agentic AI Foundation       │
                    │   (Linux Foundation)          │
                    │   W3C / IETF                 │
                    └─────────────────────────────┘
```

**Terminology note:** This space has many overlapping terms -- AX, ASO (Agent Search Optimization), GEO (Generative Engine Optimization), AEO (Answer Engine Optimization), LLMO. See [research/terminology.md](research/terminology.md) for a full mapping.

---

## Content Discovery Standards

Standards that help agents find and understand content on the web.

### llms.txt

A Markdown file at `/llms.txt` that serves as a curated index of a site's most valuable content for LLM consumption.

| | |
|---|---|
| **Created by** | Jeremy Howard (Answer.AI), September 2024 |
| **Spec** | [llmstxt.org](https://llmstxt.org/) |
| **GitHub** | [AnswerDotAI/llms-txt](https://github.com/AnswerDotAI/llms-txt) |
| **Adoption** | ~844,000 websites (BuiltWith, Oct 2025) |
| **Adopters** | Anthropic, Stripe, Cloudflare, Vercel, Cursor, Hugging Face |

**File variants:**

| File | Purpose |
|------|---------|
| `/llms.txt` | Lightweight index/table of contents with links |
| `/llms-full.txt` | Full text of all documentation in one file |
| `/llms-ctx.txt` | Expanded version with linked content inlined |
| Per-page `.md` files | Clean Markdown versions of individual pages |

**Key insight:** AI agents visit `llms-full.txt` over 2x as frequently as `llms.txt` (Mintlify data), suggesting agents prefer comprehensive content.

**Status:** Widely adopted but controversial -- no major AI provider has officially confirmed reading these files. Google has explicitly rejected the standard.

[Detailed research](research/llms-txt.md) | [Tools & generators](research/llms-txt.md#tools-generators-validators-and-related-projects)

---

### SKILL.md (Agent Skills Specification)

A Markdown file with YAML frontmatter that describes a capability an agent can learn and execute. Originated from OpenClaw/Moltbook and evolved into an open standard maintained by Anthropic.

| | |
|---|---|
| **Origin** | OpenClaw (Moltbook ecosystem), formalized by Anthropic |
| **Spec** | [agentskills.io/specification](https://agentskills.io/specification) |
| **Discovery RFC** | [Cloudflare agent-skills-discovery-rfc](https://github.com/cloudflare/agent-skills-discovery-rfc) |
| **Adopters** | Claude Code, OpenAI Codex, GitHub Copilot, Cursor, Manus |

**How it works:** Agents discover skills via `/.well-known/skills/index.json` or platform-specific directories. Skills use progressive disclosure -- metadata first (~100 tokens), full instructions on activation (<5,000 tokens), scripts/assets on execution (unlimited).

**Example SKILL.md:**
```yaml
---
name: deploy-to-production
description: Deploy the current project to production infrastructure
license: Apache-2.0
metadata:
  author: example-org
  version: "1.0"
---

# Deploy to Production

[Markdown instructions for the agent...]
```

[Detailed research](research/skill-md.md)

---

### AGENTS.md

A Markdown file placed in a repository root that gives coding agents project-specific instructions (build commands, architecture, conventions, security notes).

| | |
|---|---|
| **Created by** | OpenAI, now part of Agentic AI Foundation |
| **Spec** | [agents.md](https://agents.md/) |
| **GitHub** | [agentsmd/agents.md](https://github.com/agentsmd/agents.md) |
| **Adoption** | 60,000+ open-source repositories |
| **Supported by** | Codex, Cursor, Gemini CLI, Amp, Devin, Jules |

**Relationship to SKILL.md:** AGENTS.md defines identity and global rules ("who your agent is"), while SKILL.md defines task-specific capabilities ("what your agent can do"). They are complementary.

[Detailed research](research/agents-md.md)

---

### HEARTBEAT.md

A Markdown file in an agent's workspace that serves as a periodic task checklist. When the agent's runtime triggers a "heartbeat" (default: every 30 minutes), the agent reads this file and follows its instructions.

| | |
|---|---|
| **Created by** | OpenClaw project |
| **Scope** | OpenClaw ecosystem (not a broad industry standard) |
| **Docs** | [docs.openclaw.ai/gateway/heartbeat](https://docs.openclaw.ai/gateway/heartbeat) |

**How it works:** The agent reads HEARTBEAT.md on each heartbeat cycle. If nothing needs attention, it replies `HEARTBEAT_OK` (suppressed). If something does, it sends a message to the configured target (Telegram, Slack, etc.).

**Example:**
```markdown
# Heartbeat checklist
- Quick scan: anything urgent in inboxes?
- If it's daytime, do a lightweight check-in if nothing else is pending.
- If a task is blocked, write down what is missing and ask next time.
```

**Significance:** Demonstrates the pattern of agents maintaining ambient awareness through periodic check-ins rather than purely reactive behavior.

[Detailed research](research/heartbeat-md.md)

---

## Agent Communication Protocols

### MCP (Model Context Protocol)

The de facto standard for connecting AI agents to external tools and data sources. Often described as "USB-C for AI."

| | |
|---|---|
| **Created by** | Anthropic, November 2024 |
| **Governance** | Agentic AI Foundation (Linux Foundation), December 2025 |
| **Spec** | [modelcontextprotocol.io](https://modelcontextprotocol.io/specification/2025-11-25) |
| **GitHub** | [modelcontextprotocol](https://github.com/modelcontextprotocol/modelcontextprotocol) |
| **Adoption** | 13,000+ MCP servers on GitHub; supported by OpenAI, Google, Microsoft |

MCP servers expose **tools** (actions), **resources** (files/data), and **prompts** (templates). Clients connect via JSON-RPC over stdio or HTTP+SSE.

---

### A2A (Agent-to-Agent Protocol)

Peer-to-peer communication between independently built AI agents.

| | |
|---|---|
| **Created by** | Google Cloud, April 2025 |
| **Governance** | Linux Foundation, June 2025 |
| **Spec** | [a2a-protocol.org](https://a2a-protocol.org/latest/specification/) |
| **GitHub** | [a2aproject/A2A](https://github.com/a2aproject/A2A) |
| **Partners** | 150+ organizations (Atlassian, Salesforce, SAP, PayPal) |

**Agent Cards** at `/.well-known/agent.json` enable discovery. Uses HTTP, JSON-RPC 2.0, and SSE.

**Relationship with MCP:** "MCP for tools, A2A for agents." They are complementary.

---

### NLWeb (Natural Language Web)

Adds conversational endpoints to websites by leveraging existing Schema.org structured data.

| | |
|---|---|
| **Created by** | R.V. Guha (creator of Schema.org), Microsoft, 2025 |
| **Site** | [nlweb.ai](https://nlweb.ai/) |
| **GitHub** | [nlweb-ai/NLWeb](https://github.com/nlweb-ai/NLWeb) |

Every NLWeb instance exposes a `/ask` REST endpoint and an `/mcp` MCP server. This shifts the relationship from "AI reads the site" to "AI queries the site."

---

### Other Protocols

| Protocol | Creator | Purpose |
|----------|---------|---------|
| [Agent Protocol](https://agentprotocol.ai/) | AI Engineer Foundation | Framework-agnostic REST API for communicating with any agent |
| [ACP](https://github.com/ibm/acp) | IBM BeeAI | Lightweight HTTP-based agent messaging |
| [ANP](https://github.com/agent-network-protocol) | Community | "HTTP of the agentic web era" with DID-based identity |
| [AG-UI](https://github.com/ag-ui-protocol) | Community | Agent-to-user interaction protocol |

---

## Discovery Mechanisms

How agents find and identify services they can interact with.

### Well-Known URIs

| URI Path | Protocol | Purpose |
|----------|----------|---------|
| `/.well-known/agent.json` | A2A | Agent Card (identity, capabilities, auth) |
| `/.well-known/agents.json` | agents.json | API contracts for agent consumption |
| `/.well-known/skills/index.json` | SKILL.md | Agent skill discovery index |
| `/llms.txt` | llms.txt | Content index for LLMs |
| `/llms-full.txt` | llms.txt | Full content for LLMs |

### agents.json

Multiple competing proposals for declaring agent-accessible API contracts:

| Proposal | Approach | Link |
|----------|----------|------|
| Wildcard AI | Extends OpenAPI with flows and links | [wild-card-ai/agents-json](https://github.com/wild-card-ai/agents-json) |
| jmilinovich | Agent permissions and interaction rules | [jmilinovich/agents.json](https://github.com/jmilinovich/agents.json) |
| JSON Agents (PAM) | Portable Agent Manifest specification | [jsonagents.org](https://jsonagents.org/) |

### robots.txt Evolution

| Proposal | Purpose |
|----------|---------|
| [IETF robots.txt Update](https://www.ietf.org/archive/id/draft-jimenez-tbd-robotstxt-update-00.html) | Intent-based policies (training vs. indexing vs. inference) |
| [Really Simple Licensing (RSL)](https://rsl.ink/) | AI bot licensing terms in robots.txt (Medium, Reddit, Yahoo) |
| ai.txt | UK publisher proposal for AI bot permissions (policy, not technical) |

---

## Search & Visibility Optimization

Making content discoverable and citable by AI agents.

### GEO (Generative Engine Optimization)

The academically grounded term for optimizing content to appear in AI-generated responses.

| | |
|---|---|
| **Origin** | Princeton University (KDD 2024 paper) |
| **Paper** | [arXiv:2311.09735](https://arxiv.org/abs/2311.09735) |
| **Conference** | [geo-conference.com](https://www.geo-conference.com/) |

**Core strategies:**
- Structure content with direct answers in the first 40-60 words
- Maintain fact density (statistics every 150-200 words)
- Cite authoritative sources throughout
- Implement proper Schema.org markup
- Optimize for "chunked" content -- short, logically complete ideas

### AX Best Practices

From [agentexperience.ax](https://agentexperience.ax/) (Matt Biilmann / Netlify):

1. **Structured data over visual hierarchy** -- agents parse data, not layouts
2. **Clear APIs with logical task flows** -- agents need predictable interaction patterns
3. **Machine-readable documentation** -- Markdown, structured data, clean schemas
4. **Access parity** -- APIs exposed to agents should match browser/app capabilities
5. **Agents are delegates** -- poor AX results in poor UX for the humans agents represent

### Key Statistics

- AI-referred web sessions jumped **527%** between January and May 2025
- LLM referral traffic converts at **6x** the rate of traditional search (Webflow)
- Only **24%** of API designers consider AI agents (Postman survey)
- LLMs cite only **2-7 domains** per response vs Google's ~10 blue links

---

## Governance & Standards Bodies

| Organization | Role | Key Standards |
|-------------|------|---------------|
| [Agentic AI Foundation](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation) (Linux Foundation) | Neutral consortium (Anthropic, OpenAI, Block) | MCP, AGENTS.md, Goose |
| [W3C AI Agent Protocol CG](https://www.w3.org/community/agentprotocol/) | Web standards for agent discovery & collaboration | Agent Protocol spec |
| IETF | Internet protocol standards | robots.txt update, agent discovery drafts |
| [OWASP](https://genai.owasp.org/) | Security standards | Agent Name Service (ANS) |

### Active IETF Drafts

| Draft | Focus |
|-------|-------|
| [draft-rosenberg-ai-protocols](https://datatracker.ietf.org/doc/draft-rosenberg-ai-protocols/) | Framework and requirements for AI agent protocols |
| [draft-zyyhl-agent-networks-framework](https://datatracker.ietf.org/doc/draft-zyyhl-agent-networks-framework/) | AI agent networks with W3C DID identity |
| [draft-liu-agent-context-protocol](https://datatracker.ietf.org/doc/draft-liu-agent-context-protocol/) | Agent context sharing (Alibaba) |
| [draft-cui-ai-agent-discovery-invocation](https://www.ietf.org/archive/id/draft-cui-ai-agent-discovery-invocation-00.html) | HTTP-based agent discovery |

---

## Awesome Lists & Community Resources

### Agent Experience & Standards
- [agentexperience.ax](https://agentexperience.ax/) -- The AX resource hub (Netlify)
- [llms-txt-hub](https://github.com/thedaviddias/llms-txt-hub) -- Largest directory of llms.txt implementations
- [directory.llmstxt.cloud](https://directory.llmstxt.cloud/) -- Community directory of llms.txt adopters
- [skills.sh](https://skills.sh/) -- Agent Skills directory
- [awesome-openclaw-skills](https://github.com/VoltAgent/awesome-openclaw-skills) -- Curated OpenClaw skills

### Agent Frameworks & Tools
- [awesome-web-agents](https://github.com/steel-dev/awesome-web-agents) -- Web-browsing AI agent tools
- [awesome-autonomous-web](https://github.com/Agent-Tools/awesome-autonomous-web) -- AI agent web interaction
- [awesome_ai_agents](https://github.com/jim-schwoebel/awesome_ai_agents) -- 1,500+ agent resources
- [awesome-ai-agents](https://github.com/slavakurilyak/awesome-ai-agents) -- 300+ agentic AI resources
- [awesome-llm-agents](https://github.com/kaushikb11/awesome-llm-agents) -- LLM agent frameworks

---

## Research & Further Reading

Detailed research notes compiled during the creation of this repository:

| Topic | File |
|-------|------|
| llms.txt deep dive | [research/llms-txt.md](research/llms-txt.md) |
| SKILL.md & OpenClaw/Moltbook | [research/skill-md.md](research/skill-md.md) |
| HEARTBEAT.md | [research/heartbeat-md.md](research/heartbeat-md.md) |
| Agent Search Optimization & GEO | [research/agent-search-optimization.md](research/agent-search-optimization.md) |
| Agent protocols (MCP, A2A, etc.) | [research/agent-protocols.md](research/agent-protocols.md) |
| Terminology mapping | [research/terminology.md](research/terminology.md) |

### Key Academic Papers

- [GEO: Generative Engine Optimization](https://arxiv.org/abs/2311.09735) -- Princeton, KDD 2024
- [Generative Engine Optimization: How to Dominate AI Search](https://arxiv.org/abs/2509.08919) -- Chen et al., 2025
- [A Survey of AI Agent Protocols](https://arxiv.org/pdf/2504.16736) -- April 2025
- [A Survey of Agent Interoperability Protocols](https://arxiv.org/html/2505.02279v1) -- May 2025

### Key Blog Posts & Articles

- [Introducing AX: Why Agent Experience Matters](https://biilmann.blog/articles/introducing-ax/) -- Matt Biilmann
- [The /llms.txt file proposal](https://www.answer.ai/posts/2024-09-03-llmstxt.html) -- Jeremy Howard
- [Moltbook is the most interesting place on the internet](https://simonwillison.net/2026/Jan/30/moltbook/) -- Simon Willison
- [Beyond DX: Developers Must Now Learn Agent Experience](https://thenewstack.io/beyond-dx-developers-must-now-learn-agent-experience-ax/) -- The New Stack

---

## Contributing

This is a living document. If you know of standards, tools, or best practices that should be included, please open an issue or PR.

---

## License

CC0 1.0 Universal - See [LICENSE](LICENSE)
