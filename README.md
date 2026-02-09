# Awesome Agent Experience (AX)

A curated collection of standards, protocols, best practices, projects, and resources for making technology systems accessible and usable by AI agents.

**Agent Experience (AX)** is to AI agents what User Experience (UX) is to humans and Developer Experience (DX) is to developers. As AI agents become first-class participants in digital ecosystems, the systems they interact with need to be designed with agents in mind.

> "We are going from the age of product-led growth to the age of agent-led growth." -- Sonya Huang, Sequoia Capital

---

## Contents

- [The AX Landscape](#the-ax-landscape)
- [Best Practices & Frameworks](#best-practices--frameworks)
- [Standards & Specifications](#standards--specifications)
- [Projects & Tools](#projects--tools)
- [Informational Resources](#informational-resources)
- [Case Studies & Applications](#case-studies--applications)
- [Research Notes](#research-notes)

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

### Terminology

This space has many overlapping terms. See [research/terminology.md](research/terminology.md) for a full mapping.

| Term | Meaning |
|------|---------|
| **AX** | Agent Experience -- holistic design discipline (coined by Matt Biilmann, 2025) |
| **GEO** | Generative Engine Optimization -- academic term from Princeton (KDD 2024) |
| **ASO** | Agent Search Optimization -- SEO analog for agents |
| **AEO / LLMO** | Answer Engine Optimization / LLM Optimization -- marketing-oriented terms |

---

## Best Practices & Frameworks

### The Four Pillars of AX

*From Matt Biilmann's ["One Year of AX"](https://biilmann.blog/articles/one-year-of-ax/) (Jan 2026):*

1. **Access** -- Can the agent reach your product? Remove friction. Enable anonymous flows. Don't gatekeep.
2. **Context** -- Does the LLM have the right information? Context engineering > prompt engineering. Use MCP, Skills, markdown docs, CLI feedback loops.
3. **Tools** -- Are you building agent-first tooling? MCP servers, agent-specific CLI commands, intuitive APIs.
4. **Orchestration** -- Can you trigger agent runs and provide sandboxes? Serverless agent execution as core platform functionality.

### The Five AX Principles

*From the [agentexperience.ax](https://agentexperience.ax/concepts/principles-of-ax/) community:*

1. **Human Centricity** -- Agents serve human needs as a medium, alongside browsers and apps
2. **Agent Accessibility** -- Remove barriers; "requiring a human to be involved in order to achieve a goal is an anti-pattern"
3. **Contextual Alignment** -- Provide robust, consistent context; don't assume agents have sufficient internal knowledge
4. **Agent Interactivity Patterns** -- Standardized communication, branding, and sensitive-flow handling
5. **Differentiate Agent Interaction** -- Track agent actions separately in metrics, logs, and audit trails

### Three AX Production Patterns

*From Biilmann's ["AX in Practice"](https://biilmann.blog/articles/ax-in-practice/) (Jul 2025):*

1. **Agent-First Onboarding** -- "Deploy anonymously, then claim." Agents deploy before humans sign up; users claim ownership through signed links afterward. Used by Netlify, Clerk, Prisma, Neon.
2. **Agent-Human Interactions Within Products** -- Bidirectional linking. Linear lets users @ mention agents (Devin, Codegen) from tickets. Contrast with Salesforce's closed "Agentforce" model.
3. **Context Engineering for LLMs** -- llms.txt, .cursorrules, AGENTS.md, MCP. Documentation must be precise about unique APIs, versions, and post-training-cutoff changes.

### Six DX-to-AX Dimensions

*From Zeno Rocha / [Resend](https://resend.com/blog/agent-experience):*

| Dimension | DX Approach | AX Approach |
|---|---|---|
| Onboarding | "Wow" moments with clear steps | Millisecond activation; agents won't wait for manual reviews |
| Documentation | Concise, scannable by humans | LLM-readable formats (llms.txt) for context windows |
| SDKs | Language-native libraries | Agents write their own SDKs; REST APIs and OpenAPI specs matter more |
| Audit Logs | Security, compliance, debugging | Differentiate human vs. agent actions with precision |
| API Keys | Humans create via password managers | Agents must create, delete, and rotate keys autonomously |
| RBAC | Simple admin/viewer roles | Granular task-specific permissions; high-risk actions need human confirmation |

### AX Implementation Checklist

*From [agentexperience.ax](https://agentexperience.ax/concepts/applying-ax-practices/):*

1. **Identify Human Engagement Areas** -- Where do users want agents to act?
2. **Assess Agent Readiness** -- Are APIs documented and machine-readable?
3. **Optimize Documentation for AI** -- OpenAPI specs, structured metadata, regular updates
4. **Simplify Access Controls** -- Token-based auth, role-based access for agents, clear attribution
5. **Use Agents to Test Your Product** -- Use the same tools your users' agents use

### GEO Content Strategies

*From [Princeton's GEO paper](https://arxiv.org/abs/2311.09735) (KDD 2024):*

- Structure content with direct answers in the first 40-60 words
- Maintain fact density (statistics every 150-200 words)
- Cite authoritative sources throughout
- Implement proper Schema.org markup
- Optimize for "chunked" content -- short, logically complete ideas

[More frameworks and perspectives](research/ax-perspectives.md)

---

## Standards & Specifications

### Content Discovery

| Standard | Purpose | Spec | Creator |
|----------|---------|------|---------|
| **[llms.txt](https://llmstxt.org/)** | Curated content index for LLMs | [llmstxt.org](https://llmstxt.org/) | Jeremy Howard / Answer.AI (2024) |
| **[SKILL.md](https://agentskills.io/specification)** | Agent capability descriptions | [agentskills.io](https://agentskills.io/specification) | OpenClaw / Anthropic |
| **[AGENTS.md](https://agents.md/)** | Project-level agent instructions | [agents.md](https://agents.md/) | OpenAI / Agentic AI Foundation |
| **HEARTBEAT.md** | Periodic agent task checklists | [docs.openclaw.ai](https://docs.openclaw.ai/gateway/heartbeat) | OpenClaw |

### Communication Protocols

| Protocol | Purpose | Spec | Creator |
|----------|---------|------|---------|
| **[MCP](https://modelcontextprotocol.io/)** | Agent-to-tool connections ("USB-C for AI") | [modelcontextprotocol.io](https://modelcontextprotocol.io/specification/2025-11-25) | Anthropic (2024) |
| **[A2A](https://a2a-protocol.org/)** | Agent-to-agent communication | [a2a-protocol.org](https://a2a-protocol.org/latest/specification/) | Google (2025) |
| **[NLWeb](https://nlweb.ai/)** | Conversational endpoints for websites | [nlweb.ai](https://nlweb.ai/) | Microsoft / R.V. Guha (2025) |
| **[Agent Protocol](https://agentprotocol.ai/)** | Framework-agnostic agent REST API | [agentprotocol.ai](https://agentprotocol.ai/specification/) | AI Engineer Foundation |
| **[ACP](https://github.com/ibm/acp)** | Lightweight agent messaging | GitHub | IBM BeeAI |
| **[ANP](https://github.com/agent-network-protocol)** | Decentralized agent networking | GitHub | Community |

### Discovery Mechanisms

| URI Path | Protocol | Purpose |
|----------|----------|---------|
| `/.well-known/agent.json` | A2A | Agent Card (identity, capabilities, auth) |
| `/.well-known/agents.json` | agents.json | API contracts for agent consumption |
| `/.well-known/skills/index.json` | SKILL.md | Agent skill discovery index |
| `/llms.txt` | llms.txt | Content index for LLMs |
| `/llms-full.txt` | llms.txt | Full content for LLMs |

### API Description Proposals

| Proposal | Approach | Link |
|----------|----------|------|
| Wildcard AI agents.json | Extends OpenAPI with flows and links | [wild-card-ai/agents-json](https://github.com/wild-card-ai/agents-json) |
| jmilinovich agents.json | Agent permissions and interaction rules | [jmilinovich/agents.json](https://github.com/jmilinovich/agents.json) |
| JSON Agents (PAM) | Portable Agent Manifest specification | [jsonagents.org](https://jsonagents.org/) |

### Access Control Evolution

| Proposal | Purpose |
|----------|---------|
| [IETF robots.txt Update](https://www.ietf.org/archive/id/draft-jimenez-tbd-robotstxt-update-00.html) | Intent-based policies (training vs. indexing vs. inference) |
| [Really Simple Licensing (RSL)](https://rsl.ink/) | AI bot licensing terms in robots.txt (Medium, Reddit, Yahoo) |
| ai.txt | UK publisher proposal for AI bot permissions |

### Governance

| Organization | Role | Key Standards |
|-------------|------|---------------|
| [Agentic AI Foundation](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation) (Linux Foundation) | Neutral consortium (Anthropic, OpenAI, Block) | MCP, AGENTS.md, Goose |
| [W3C AI Agent Protocol CG](https://www.w3.org/community/agentprotocol/) | Web standards for agent discovery & collaboration | Agent Protocol spec |
| IETF | Internet protocol standards | robots.txt update, agent discovery drafts |
| [OWASP](https://genai.owasp.org/) | Security standards | Agent Name Service (ANS) |

Detailed specs: [research/agent-protocols.md](research/agent-protocols.md) | [research/llms-txt.md](research/llms-txt.md) | [research/skill-md.md](research/skill-md.md)

---

## Projects & Tools

### Agent-Readable Content

Tools that help websites serve content to AI agents.

| Project | Description | Link |
|---------|-------------|------|
| **Firecrawl** | Web data API; turns websites into LLM-ready markdown (~30k stars) | [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) |
| **Crawl4AI** | Open-source LLM-friendly web crawler (~50k stars) | [unclecode/crawl4ai](https://github.com/unclecode/crawl4ai) |
| **llms-txt (spec)** | The original llms.txt specification | [AnswerDotAI/llms-txt](https://github.com/AnswerDotAI/llms-txt) |
| **llms-txt-hub** | Largest directory of llms.txt implementations (~684 stars) | [thedaviddias/llms-txt-hub](https://github.com/thedaviddias/llms-txt-hub) |
| **llmstxt-generator** | Generates llms.txt files by crawling a website | [firecrawl/llmstxt-generator](https://github.com/firecrawl/llmstxt-generator) |
| **aircode llms-txt-gen** | AI-powered llms.txt generator with MCP integration | [aircodelabs/llms-txt-generator](https://github.com/aircodelabs/llms-txt-generator) |

### Agent Discovery & Registration

How agents find and register with each other.

| Project | Description | Link |
|---------|-------------|------|
| **A2A Protocol** | Google's agent-to-agent protocol (Linux Foundation) | [a2aproject/A2A](https://github.com/a2aproject/A2A) |
| **Agent Network Protocol** | Decentralized agent networking with W3C DID identity | [agent-network-protocol/ANP](https://github.com/agent-network-protocol/AgentNetworkProtocol) |
| **Agent Cards** | Verifiable identity and capabilities for autonomous agents | [commandlayer/agent-cards](https://github.com/commandlayer/agent-cards) |
| **AGNTCY** | Open-source infrastructure for inter-agent collaboration | [agntcy](https://github.com/agntcy) |
| **OpenAgents** | AI agent network infrastructure with MCP and AsyncAPI | [openagents-org/openagents](https://github.com/openagents-org/openagents) |

### Agent-Friendly APIs

Making APIs accessible to agents.

| Project | Description | Link |
|---------|-------------|------|
| **NLWeb** | Natural language endpoints for websites (Microsoft) | [microsoft/NLWeb](https://github.com/microsoft/NLWeb) |
| **agents.json (Wildcard)** | OpenAPI extension for agent consumption | [wild-card-ai/agents-json](https://github.com/wild-card-ai/agents-json) |
| **agents.json (jmilinovich)** | robots.txt-like agent interaction rules | [jmilinovich/agents.json](https://github.com/jmilinovich/agents.json) |
| **wpnlweb** | WordPress plugin implementing NLWeb protocol | [gigabit-eth/wpnlweb](https://github.com/gigabit-eth/wpnlweb) |

### Agent Web Interaction

Browser automation and web agents.

| Project | Description | Link |
|---------|-------------|------|
| **browser-use** | Make websites accessible for AI agents (~78k stars) | [browser-use/browser-use](https://github.com/browser-use/browser-use) |
| **Stagehand** | SDK for AI browser automation with fail-safes | [browserbase/stagehand](https://github.com/browserbase/stagehand) |
| **agent-browser** | Browser automation CLI for AI agents (Vercel) | [vercel-labs/agent-browser](https://github.com/vercel-labs/agent-browser) |
| **Notte** | Full-stack framework for web agents | [nottelabs/notte](https://github.com/nottelabs/notte) |
| **Steel Browser** | Open-source browser API for AI agents | [steel-dev/steel-browser](https://github.com/steel-dev/steel-browser) |
| **Web Agent Protocol** | Standardized framework for recording/replaying browser interactions | [OTA-Tech-AI/web-agent-protocol](https://github.com/OTA-Tech-AI/web-agent-protocol) |

### MCP Ecosystem

Model Context Protocol servers and tools.

| Project | Description | Link |
|---------|-------------|------|
| **MCP Servers (official)** | Reference server implementations by Anthropic | [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) |
| **GitHub MCP Server** | GitHub's official MCP server (Go) | [github/github-mcp-server](https://github.com/github/github-mcp-server) |
| **awesome-mcp-servers** | Curated list of MCP servers (punkpeye) | [punkpeye/awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) |
| **awesome-mcp-servers** | Curated list of MCP servers (wong2) | [wong2/awesome-mcp-servers](https://github.com/wong2/awesome-mcp-servers) |
| **crawl4ai-mcp-server** | Web scraping as MCP tools | [sadiuysal/crawl4ai-mcp-server](https://github.com/sadiuysal/crawl4ai-mcp-server) |

### Skills & Instructions

Agent skill and instruction file standards.

| Project | Description | Link |
|---------|-------------|------|
| **AGENTS.md** | Open format for guiding coding agents (60k+ repos) | [agentsmd/agents.md](https://github.com/agentsmd/agents.md) |
| **ClawHub** | Public skill registry for OpenClaw | [openclaw/clawhub](https://github.com/openclaw/clawhub) |
| **awesome-openclaw-skills** | Curated collection of OpenClaw skills | [VoltAgent/awesome-openclaw-skills](https://github.com/VoltAgent/awesome-openclaw-skills) |
| **agent-trace** | Standard format for tracing AI-generated code (Cursor) | [cursor/agent-trace](https://github.com/cursor/agent-trace) |

### Agent SEO / GEO Tools

Optimizing content for AI discovery.

| Project | Description | Link |
|---------|-------------|------|
| **GEO** | Research framework for Generative Engine Optimization (Princeton) | [GEO-optim/GEO](https://github.com/GEO-optim/GEO) |
| **GetCito** | Open-source AI search optimization tool | [ai-search-guru/getcito](https://github.com/ai-search-guru/getcito-worlds-first-open-source-aio-aeo-or-geo-tool) |
| **Gego** | Open-source GEO tracker across multiple LLMs | [AI2HU/gego](https://github.com/AI2HU/gego) |
| **awesome-GEO** | Curated GEO resources and tools | [amplifying-ai/awesome-generative-engine-optimization](https://github.com/amplifying-ai/awesome-generative-engine-optimization) |
| **GEO tools list** | Extensive list of commercial and free GEO tools | [izak-fisher/generative-engine-optimization-tools](https://github.com/izak-fisher/generative-engine-optimization-tools) |

### Benchmarking & Testing

Evaluating agent capabilities and agent-friendliness.

| Project | Description | Link |
|---------|-------------|------|
| **AI Agent Benchmark Compendium** | Directory of 50+ agent benchmarks | [philschmid/ai-agent-benchmark-compendium](https://github.com/philschmid/ai-agent-benchmark-compendium) |
| **TheAgentCompany** | 175-task benchmark in a simulated software company | [TheAgentCompany/TheAgentCompany](https://github.com/TheAgentCompany/TheAgentCompany) |
| **best-of-mcp-servers** | Ranked list of MCP servers, updated weekly | [tolkonepiu/best-of-mcp-servers](https://github.com/tolkonepiu/best-of-mcp-servers) |

---

## Informational Resources

### Foundational Reading

| Resource | Author | Description |
|----------|--------|-------------|
| [Introducing AX: Why Agent Experience Matters](https://biilmann.blog/articles/introducing-ax/) | Matt Biilmann | The original AX manifesto (Jan 2025) |
| [One Year of AX](https://biilmann.blog/articles/one-year-of-ax/) | Matt Biilmann | Four Pillars framework; AX retrospective (Jan 2026) |
| [AX in Practice](https://biilmann.blog/articles/ax-in-practice/) | Matt Biilmann | Real-world patterns from Netlify and industry (Jul 2025) |
| [Principles of AX](https://agentexperience.ax/concepts/principles-of-ax/) | agentexperience.ax | Community-defined AX principles |
| [Applying AX Practices](https://agentexperience.ax/concepts/applying-ax-practices/) | agentexperience.ax | Five-step implementation checklist |

### Company Perspectives

| Resource | Author | Key Insight |
|----------|--------|-------------|
| [What is AX and How to Improve It](https://resend.com/blog/agent-experience) | Zeno Rocha / Resend | Six DX-to-AX dimensions (onboarding, docs, SDKs, audit, keys, RBAC) |
| [Agent Experience Is the Only Experience That Matters](https://www.daytona.io/dotfiles/agent-experience-is-the-only-experience-that-matters) | Ivan Burazin / Daytona | "DX is table stakes. AX is the next paradigm." |
| [The Age of Agent Experience](https://stytch.com/blog/the-age-of-agent-experience/) | Julianna Lamb / Stytch | Auth and identity for agent-mediated interactions |
| [MCP: A Key Unlock for AX](https://www.netlify.com/blog/mcp-a-key-unlock-for-delivering-a-good-ax/) | Sean Roberts / Netlify | Five community AX principles + MCP's role |
| [The Agent Web and Its Interface](https://www.netlify.com/blog/continuing-the-ax-conversation-the-agent-web-and-its-interface/) | Dana Lawson / Netlify | Content negotiation, NL APIs, rethinking auth |
| [Agent-Facing Analytics](https://clickhouse.com/blog/agent-facing-analytics) | Ryadh Dahimene / ClickHouse | Designing analytics for agent consumption |
| [Great AX starts with great collaboration](https://liveblocks.io/blog/great-agent-experience-great-collaboration) | Steven Fabre / Liveblocks | Collaborative agent workflows |
| [Making content AI-Ready](https://www.sanity.io/blog/improving-the-agent-experience-for-sanity-learn) | Knut Melvaer / Sanity | Plain text content for agent readability |
| [Designing APIs for AI](https://abhiaiyer.medium.com/designing-apis-for-ai-the-need-for-new-standards-700a606e9a10) | Abhi Aiyer | New API design standards for agents |
| [AI Go-To-Market](https://docs.buildwithlayer.com/ai_gtm) | Jonah Katz / Layer | Agents as a new path to adoption |

### VC & Analyst Perspectives

| Source | Key Insight |
|--------|-------------|
| **a16z** "Big Ideas 2026" | "We're no longer designing for humans, but for agents." Proposed dual-mode interfaces. |
| **Sequoia Capital** | "MCP may become as foundational as TCP/IP." Agent economy requires persistent identity and communication protocols. |
| **Bessemer Venture Partners** | Named AX as "Law #1" in AI Developer Laws. Created AI Agent Autonomy Scale. |
| **Forrester** | Five critical AX skills: knowledge curation, change management, critical thinking, interaction skills, agent oversight. |
| **McKinsey** | Up to $1T in US retail, $3-5T globally by 2030. "If your catalog is not machine-readable, agents will not find you." |
| **BCG** | AI traffic to retail up 4,700% YoY. "Those who wait risk becoming invisible." |

### Thought Leaders

| Resource | Author | Key Insight |
|----------|--------|-------------|
| [Simplicity and Agentic Experience](https://johnmaeda.medium.com/simplicity-and-agentic-experience-ax-0087553b73d8) | John Maeda | Simplicity principles applied to AX |
| [Beyond DX: Developers Must Now Learn AX](https://thenewstack.io/beyond-dx-developers-must-now-learn-agent-experience-ax/) | Richard MacManus / The New Stack | Industry analysis of emerging AX patterns |
| [Mastering Agentic Experience](https://shiftmag.dev/matt-biilmann-on-mastering-agentic-experience-6237/) | ShiftMag | Biilmann at Shift Conference: 5x signups, 7x conversions |
| [Moltbook is the most interesting place](https://simonwillison.net/2026/Jan/30/moltbook/) | Simon Willison | Analysis of the first agent social network |
| [The /llms.txt file proposal](https://www.answer.ai/posts/2024-09-03-llmstxt.html) | Jeremy Howard | Original llms.txt proposal |
| [Every Website Needs to be Redesigned for AX](https://www.daeila.com/blog/post-6/) | Nathan Daeila | The case for wholesale redesign |
| [Service Design for AI: Why HX Matters](https://blog.ronbronson.com/service-design-for-ai-why-human-experience-hx-matters) | Ron Bronson | Counterpoint: keeping humans in the loop |

### Academic Papers

| Paper | Authors | Venue |
|-------|---------|-------|
| [GEO: Generative Engine Optimization](https://arxiv.org/abs/2311.09735) | Aggarwal et al. | KDD 2024 |
| [How to Dominate AI Search](https://arxiv.org/abs/2509.08919) | Chen et al. | 2025 |
| [A Survey of AI Agent Protocols](https://arxiv.org/pdf/2504.16736) | Multiple | April 2025 |
| [A Survey of Agent Interoperability Protocols](https://arxiv.org/html/2505.02279v1) | Multiple | May 2025 |

### Conferences

| Event | Focus |
|-------|-------|
| [GEO Conference](https://www.geo-conference.com/) | Generative Engine Optimization (Austin, SF, DC) |
| [Netlify Agent Week](https://www.netlify.com/blog/agent-week-2025/) | Annual agent infrastructure event |

---

## Case Studies & Applications

### Agentic Commerce

| Company | What They Did | Impact |
|---------|---------------|--------|
| **Stripe** | Co-developed Agentic Commerce Protocol (ACP) with OpenAI; created Shared Payment Tokens (SPTs); hosted MCP server; all docs as markdown | New payment primitive for agent-mediated transactions |
| **Shopify** | Co-developed Universal Commerce Protocol (UCP) with Google; "every store agent-ready by default" | AI traffic surged **7x**, orders **11x**; thin product data stores invisible to agents |
| **Walmart** | "Super Agent" architecture with three personas sharing a single MCP data plane | Cut out-of-stock events by **30%** in pilot stores |
| **Michael Kors** | Shopping Muse semantic styling agent translating aesthetic language to products | **15-20% conversion rate improvement** over keyword search |

### Platform AX

| Company | What They Did | Impact |
|---------|---------------|--------|
| **Netlify** | Shifted North Star from DX to AX; anonymous deploy flows; MCP server; context files | **10M developers**; 5x daily signups; 7x paid conversions; ~10k AI-generated sites/day |
| **Daytona** | Built agent-native development infrastructure | **$1M ARR in 8 weeks** |
| **Cloudflare** | First toolkit to securely connect SaaS to Claude via MCP; agent-skills-discovery RFC | MCP server deployment reduced from weeks to days |
| **Linear** | Enabled @ mentioning AI agents (Devin, Codegen) from tickets | Bidirectional agent-human product interaction |

### Key Statistics

| Metric | Value | Source |
|--------|-------|--------|
| AI-referred web sessions growth | **+527%** (Jan-May 2025) | Industry data |
| LLM referral conversion rate | **6x** vs traditional search | Webflow |
| API designers considering agents | Only **24%** | Postman 2025 |
| AI traffic to retail growth | **+4,700%** YoY | BCG |
| Projected agent economy | **$1T** US retail, **$3-5T** global by 2030 | McKinsey |

---

## Research Notes

Detailed research notes compiled during the creation of this repository:

| Topic | File |
|-------|------|
| llms.txt deep dive | [research/llms-txt.md](research/llms-txt.md) |
| SKILL.md & OpenClaw/Moltbook | [research/skill-md.md](research/skill-md.md) |
| HEARTBEAT.md | [research/heartbeat-md.md](research/heartbeat-md.md) |
| AGENTS.md | [research/agents-md.md](research/agents-md.md) |
| Agent protocols (MCP, A2A, etc.) | [research/agent-protocols.md](research/agent-protocols.md) |
| Agent Search Optimization & GEO | [research/agent-search-optimization.md](research/agent-search-optimization.md) |
| AX perspectives & frameworks | [research/ax-perspectives.md](research/ax-perspectives.md) |
| Netlify's AX canon | [research/netlify-ax.md](research/netlify-ax.md) |
| Terminology mapping | [research/terminology.md](research/terminology.md) |

### Awesome Lists

| List | Focus |
|------|-------|
| [agentexperience.ax](https://agentexperience.ax/) | The AX community hub (Netlify) |
| [awesome-web-agents](https://github.com/steel-dev/awesome-web-agents) | Web-browsing AI agent tools |
| [awesome-autonomous-web](https://github.com/Agent-Tools/awesome-autonomous-web) | AI agent web interaction |
| [awesome_ai_agents](https://github.com/jim-schwoebel/awesome_ai_agents) | 1,500+ agent resources |
| [awesome-ai-agents](https://github.com/slavakurilyak/awesome-ai-agents) | 300+ agentic AI resources |
| [awesome-llm-agents](https://github.com/kaushikb11/awesome-llm-agents) | LLM agent frameworks |
| [awesome-GEO](https://github.com/amplifying-ai/awesome-generative-engine-optimization) | Generative Engine Optimization resources |
| [llms-txt-hub](https://github.com/thedaviddias/llms-txt-hub) | Directory of llms.txt implementations |

---

## Contributing

This is a living document. If you know of standards, tools, or best practices that should be included, please open an issue or PR.

---

## License

CC0 1.0 Universal - See [LICENSE](LICENSE)
