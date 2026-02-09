# Agent Communication Protocols

## Protocol Landscape Overview

The emerging consensus is that these protocols are **complementary, not competing**:

```
MCP (Agent <-> Tools)  +  A2A (Agent <-> Agent)  +  NLWeb (Agent <-> Web)
         │                        │                        │
         └────────────────────────┼────────────────────────┘
                                  │
                    Agentic AI Foundation (Linux Foundation)
                    + AGENTS.md (OpenAI) + Goose (Block)
```

---

## MCP (Model Context Protocol)

**The de facto standard** for connecting AI agents to external tools and data sources. Often described as "USB-C for AI."

| | |
|---|---|
| Created by | Anthropic, November 2024 |
| Governance | Agentic AI Foundation (Linux Foundation), December 2025 |
| Spec | [modelcontextprotocol.io](https://modelcontextprotocol.io/specification/2025-11-25) |
| GitHub | [modelcontextprotocol](https://github.com/modelcontextprotocol/modelcontextprotocol) |

### Architecture

MCP servers expose three primitives:
- **Tools** -- actions the agent can invoke
- **Resources** -- files and data the agent can read
- **Prompts** -- templates for common interactions

Clients connect via JSON-RPC over **stdio** (local) or **HTTP+SSE** (remote).

### Adoption Timeline

- **Nov 2024:** Anthropic launches MCP
- **Mar 2025:** OpenAI adopts MCP (Agents SDK, Responses API, ChatGPT desktop)
- **Apr 2025:** Google DeepMind confirms Gemini support
- **May 2025:** Microsoft joins steering committee; integration in Windows 11
- **Nov 2025:** Major spec update (async ops, statelessness, server identity, official registry)
- **Dec 2025:** Donated to Agentic AI Foundation under Linux Foundation
- **By end 2025:** 13,000+ MCP servers on GitHub

### MCP Apps Extension (SEP-1865)

November 2025: Anthropic and OpenAI partnered to release standardized interactive UI capabilities for MCP.

### Key Prediction

Gartner's 2025 Software Engineering Survey: by 2026, **75% of API gateway vendors** and **50% of iPaaS vendors** will have MCP features.

---

## A2A (Agent-to-Agent Protocol)

Peer-to-peer communication between opaque, independently built AI agents.

| | |
|---|---|
| Created by | Google Cloud, April 2025 |
| Governance | Linux Foundation, June 2025 |
| Spec | [a2a-protocol.org](https://a2a-protocol.org/latest/specification/) |
| GitHub | [a2aproject/A2A](https://github.com/a2aproject/A2A) |
| Partners | 150+ organizations |

### Agent Card

The cornerstone of A2A discovery. Every agent publishes a JSON document at `/.well-known/agent.json`:
- Name, endpoint, skills
- Authentication flows
- Capabilities and constraints

### Core Design

- HTTP, JSON-RPC 2.0, Server-Sent Events
- Enterprise-ready with built-in auth, security, tracing
- Async-first for long-running tasks and human-in-the-loop workflows
- Version 0.3 (July 2025) added gRPC support and signed security cards

### Task Lifecycle

Tasks transition through states: submitted -> working -> input-required -> completed.

Communication uses:
- **Messages** -- between agents
- **Artifacts** -- immutable results
- **Parts** -- self-contained data blocks

### Relationship with MCP

"MCP for tools, A2A for agents." Applications typically need both.

---

## NLWeb (Natural Language Web)

Adds conversational endpoints to websites by leveraging existing Schema.org structured data.

| | |
|---|---|
| Created by | R.V. Guha (creator of Schema.org, RSS, RDF), Microsoft, 2025 |
| Site | [nlweb.ai](https://nlweb.ai/) |
| GitHub | [nlweb-ai/NLWeb](https://github.com/nlweb-ai/NLWeb) |

### Key Innovation

Every NLWeb instance is also an MCP server. Defines:
- REST API (`/ask` endpoint) accepting natural language queries
- MCP server (`/mcp` endpoint)
- Responses in Schema.org JSON format

Fundamentally shifts from "AI reads the site" to "AI queries the site."

---

## Agent Protocol

A tech-agnostic REST API specification (OpenAPI 3.0) for communicating with any AI agent.

| | |
|---|---|
| Maintained by | AGI, Inc. (originally AI Engineer Foundation) |
| Spec | [agentprotocol.ai](https://agentprotocol.ai/specification/) |
| GitHub | [AI-Engineer-Foundation/agent-protocol](https://github.com/AI-Engineer-Foundation/agent-protocol) |
| W3C CG | [w3.org/community/agentprotocol](https://www.w3.org/community/agentprotocol/) |

### Core Endpoints

- `POST /ap/v1/agent/tasks` -- Create a new task
- `POST /ap/v1/agent/tasks/{task_id}/steps` -- Execute one step

### Core Concepts

- **Tasks** -- goals/objectives
- **Steps** -- units of work
- **Artifacts** -- files/data produced

Primary value: framework-agnostic benchmarking and standardized integration.

---

## ACP (Agent Communication Protocol)

| | |
|---|---|
| Created by | IBM BeeAI, early 2025 |
| Governance | Linux Foundation |

Lightweight HTTP-based messaging protocol for agent-to-agent communication. Simpler than A2A, focused on direct messaging.

---

## ANP (Agent Network Protocol)

| | |
|---|---|
| Created by | Community (open source) |

Positioned as "HTTP of the agentic web era." Uses HTTP + JSON-LD with W3C DID-based decentralized identity and end-to-end encryption. Includes a meta-protocol layer for agents to negotiate communication terms.

---

## AG-UI (Agent-User Interaction Protocol)

Community-developed protocol for standardizing how agents interact with users (as opposed to other agents or tools).

---

## agents.json

Multiple competing proposals:

| Proposal | Approach | Link |
|----------|----------|------|
| **Wildcard AI** | Extends OpenAPI with flows and links for agent consumption | [wild-card-ai/agents-json](https://github.com/wild-card-ai/agents-json) |
| **jmilinovich** | Agent permissions and interaction rules (robots.txt for agents) | [jmilinovich/agents.json](https://github.com/jmilinovich/agents.json) |
| **JSON Agents (PAM)** | Portable Agent Manifest for capabilities, tools, security | [jsonagents.org](https://jsonagents.org/) |
| **OpenBB** | Custom agents expose capabilities to OpenBB platform | [docs.openbb.co](https://docs.openbb.co/workspace/developers/json-specs/agents-json-reference) |

---

## Discovery Mechanisms

### Well-Known URIs (RFC 8615)

| URI Path | Protocol | Purpose |
|----------|----------|---------|
| `/.well-known/agent.json` | A2A | Agent Card |
| `/.well-known/agents.json` | agents.json | API contracts |
| `/.well-known/skills/index.json` | SKILL.md | Skill discovery |
| `/.well-known/ai-plugin.json` | OpenAI (deprecated) | ChatGPT plugin manifest |

### Other Discovery

- DNS-based discovery
- Centralized registries/marketplaces
- Private catalogs
- ACP manifest files
- OWASP Agent Name Service (ANS) -- leverages PKI and JSON schemas

---

## robots.txt Evolution

| Proposal | Purpose | Status |
|----------|---------|--------|
| [IETF robots.txt Update](https://www.ietf.org/archive/id/draft-jimenez-tbd-robotstxt-update-00.html) | Intent-based policies, API discovery, cryptographic verification | Draft |
| [Really Simple Licensing (RSL)](https://rsl.ink/) | AI bot licensing terms in robots.txt | Active (Medium, Reddit, Yahoo) |
| ai.txt | UK publisher proposal for AI bot permissions | Policy proposal |

---

## Standards Bodies

### Agentic AI Foundation (AAIF)

Launched December 2025 under the Linux Foundation. Founded by Anthropic, OpenAI, and Block. Consolidates MCP, AGENTS.md, and Goose into a neutral consortium.

### Active IETF Drafts

| Draft | Focus |
|-------|-------|
| [draft-rosenberg-ai-protocols](https://datatracker.ietf.org/doc/draft-rosenberg-ai-protocols/) | Framework and requirements for AI agent protocols |
| [draft-zyyhl-agent-networks-framework](https://datatracker.ietf.org/doc/draft-zyyhl-agent-networks-framework/) | AI agent networks with W3C DID identity |
| [draft-liu-agent-context-protocol](https://datatracker.ietf.org/doc/draft-liu-agent-context-protocol/) | Agent context sharing (Alibaba) |
| [draft-cui-ai-agent-discovery-invocation](https://www.ietf.org/archive/id/draft-cui-ai-agent-discovery-invocation-00.html) | HTTP-based agent discovery |
| [draft-hw-ai-agent-6g](https://datatracker.ietf.org/doc/draft-hw-ai-agent-6g/) | Agent protocols for 6G networks |

### W3C Activities

- **AI Agent Protocol Community Group** -- developing open protocols for agent discovery, identification, and collaboration
- **TPAC 2025** -- sessions on agent security, payment protocols, generative UI
- **March 2025 Workshop** -- "How would AI Agents change the Web platform?"

### OWASP

- **Agent Name Service (ANS)** -- PKI and JSON schemas for secure agent discovery
- Supports A2A, MCP, and ACP protocols

## Academic Surveys

- [A Survey of AI Agent Protocols](https://arxiv.org/pdf/2504.16736) -- April 2025
- [A Survey of Agent Interoperability Protocols](https://arxiv.org/html/2505.02279v1) -- May 2025

## Sources

- [AI Agent Protocols 2026: Complete Guide](https://www.ruh.ai/blogs/ai-agent-protocols-2026-complete-guide)
- [Top AI Agent Protocols in 2026](https://getstream.io/blog/ai-agent-protocols/)
- [What Are AI Agent Protocols?](https://www.ibm.com/think/topics/ai-agent-protocols)
- [IETF Agentic AI Standards Blog](https://www.ietf.org/blog/agentic-ai-standards/)
- [W3C AI at TPAC 2025](https://www.w3.org/blog/2025/ai-at-tpac-2025/)
