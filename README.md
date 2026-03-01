# Awesome Agent Experience (AX) [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of standards, protocols, tools, and resources for making technology systems accessible and usable by AI agents.

Agent Experience (AX) is to AI agents what User Experience (UX) is to humans and Developer Experience (DX) is to developers.

## Contents

- [Frameworks & Best Practices](#frameworks--best-practices)
- [Standards](#standards)
  - [Content Discovery](#content-discovery)
  - [Communication Protocols](#communication-protocols)
  - [Discovery Mechanisms](#discovery-mechanisms)
  - [Access Control](#access-control)
  - [API Description](#api-description)
  - [Governance](#governance)
- [Tools](#tools)
  - [Agent-Readable Content](#agent-readable-content)
  - [Agent Discovery & Registration](#agent-discovery--registration)
  - [Agent-Friendly APIs](#agent-friendly-apis)
  - [Agent Web Interaction](#agent-web-interaction)
  - [MCP Ecosystem](#mcp-ecosystem)
  - [Skills & Instructions](#skills--instructions)
  - [GEO & Agent SEO](#geo--agent-seo)
  - [Benchmarking & Testing](#benchmarking--testing)
- [Articles & Talks](#articles--talks)
  - [Foundational](#foundational)
  - [Company Perspectives](#company-perspectives)
  - [Thought Leadership](#thought-leadership)
  - [VC & Analyst Takes](#vc--analyst-takes)
- [Case Studies](#case-studies)
  - [Agentic Commerce](#agentic-commerce)
  - [Platform AX](#platform-ax)
- [Academic Papers](#academic-papers)
- [Related Awesome Lists](#related-awesome-lists)
- [Research Notes](#research-notes)

## Frameworks & Best Practices

Established frameworks for designing agent-friendly systems. See [research/ax-perspectives.md](research/ax-perspectives.md) for detailed breakdowns.

### The Four Pillars of AX

*[Matt Biilmann](https://biilmann.blog/articles/one-year-of-ax/) (Netlify), Jan 2026*

1. **Access** - Can the agent reach your product? Remove friction. Enable anonymous flows.
2. **Context** - Does the LLM have the right information? Context engineering > prompt engineering.
3. **Tools** - Are you building agent-first tooling? MCP servers, agent-specific CLIs, intuitive APIs.
4. **Orchestration** - Can you trigger agent runs and provide sandboxes?

### The Five AX Principles

*[agentexperience.ax](https://agentexperience.ax/concepts/principles-of-ax/) community*

1. **Human Centricity** - Agents serve human needs as a medium, alongside browsers and apps.
2. **Agent Accessibility** - Remove barriers. Requiring a human in the loop is an anti-pattern where not strictly necessary.
3. **Contextual Alignment** - Provide robust, consistent context. Don't assume agents know enough.
4. **Agent Interactivity Patterns** - Standardize communication, branding, and sensitive-flow handling.
5. **Differentiate Agent Interaction** - Track agent actions separately in metrics, logs, and audit trails.

### Three Production Patterns

*[Matt Biilmann](https://biilmann.blog/articles/ax-in-practice/) (Netlify), Jul 2025*

1. **Agent-First Onboarding** - Deploy anonymously, then claim. Used by Netlify, Clerk, Prisma, Neon.
2. **Agent-Human Interactions** - Bidirectional linking. Linear lets users @ mention agents from tickets.
3. **Context Engineering** - llms.txt, .cursorrules, AGENTS.md, MCP. Documentation must be precise about post-cutoff changes.

### Six DX-to-AX Dimensions

*[Zeno Rocha](https://resend.com/blog/agent-experience) (Resend)*

1. **Onboarding** - Millisecond activation; agents won't wait for manual reviews.
2. **Documentation** - LLM-readable formats (llms.txt) for context windows.
3. **SDKs** - Agents write their own; REST APIs and OpenAPI specs matter more.
4. **Audit Logs** - Differentiate human vs. agent actions with precision.
5. **API Keys** - Agents must create, delete, and rotate keys autonomously.
6. **RBAC** - Granular task-specific permissions; high-risk actions need human confirmation.

### Implementation Checklist

*[agentexperience.ax](https://agentexperience.ax/concepts/applying-ax-practices/)*

1. Identify where users want agents to act.
2. Assess whether APIs are documented and machine-readable.
3. Optimize documentation for AI (OpenAPI specs, structured metadata).
4. Simplify access controls (token-based auth, role-based access for agents).
5. Use agents to test your own product.

## Standards

### Content Discovery

- [llms.txt](https://llmstxt.org/) - Curated Markdown index of a site's most valuable content for LLMs. Created by Jeremy Howard (Answer.AI). ~844k sites adopted.
- [llms-full.txt](https://llmstxt.org/) - Companion to llms.txt with full documentation text in one file. Agents visit it 2x more often than llms.txt.
- [SKILL.md](https://agentskills.io/specification) - Agent capability descriptions with YAML frontmatter and progressive disclosure. Originated from OpenClaw/Moltbook, formalized by Anthropic.
- [AGENTS.md](https://agents.md/) - Project-level instructions for coding agents (build commands, architecture, conventions). Created by OpenAI, now part of the Agentic AI Foundation. 60k+ repos.
- [HEARTBEAT.md](https://docs.openclaw.ai/gateway/heartbeat) - Periodic task checklist for autonomous agent check-ins. OpenClaw ecosystem.

### Communication Protocols

- [MCP](https://modelcontextprotocol.io/specification/2025-11-25) - Model Context Protocol. Agent-to-tool connections. Often called "USB-C for AI." Created by Anthropic (2024), now under the Agentic AI Foundation. 13k+ servers on GitHub.
- [A2A](https://a2a-protocol.org/latest/specification/) - Agent-to-Agent Protocol. Peer-to-peer communication between independently built agents. Created by Google (2025), now under Linux Foundation. 150+ partner organizations.
- [NLWeb](https://nlweb.ai/) - Natural Language Web. Adds conversational `/ask` and `/mcp` endpoints to websites using Schema.org data. Created by R.V. Guha (creator of Schema.org) at Microsoft.
- [Agent Protocol](https://agentprotocol.ai/specification/) - Framework-agnostic REST API for communicating with any agent. Tasks, steps, and artifacts. AI Engineer Foundation.
- [ACP](https://github.com/ibm/acp) - Agent Communication Protocol. Lightweight HTTP-based agent messaging. IBM BeeAI.
- [ANP](https://github.com/agent-network-protocol) - Agent Network Protocol. Decentralized agent networking with W3C DID identity and end-to-end encryption.
- [AG-UI](https://github.com/ag-ui-protocol) - Agent-User Interaction Protocol. Standardizes how agents interact with end users.
- [A2UI](https://a2aprotocol.ai/blog/2026-a2ui-developer-guide) - Agent to UI Protocol. Enables AI agents to generate rich, interactive user interfaces using declarative JSON messages.
- [UCP](https://ucp.dev/) - Universal Commerce Protocol. Open standard co-developed by Google and Shopify enabling AI agents to connect and transact with merchants. Covers discovery, cart assembly, checkout, and post-purchase support.

### Discovery Mechanisms

Well-known URIs (RFC 8615) for agent discovery:

- `/.well-known/agent.json` - A2A Agent Card (identity, capabilities, auth).
- `/.well-known/agents.json` - API contracts optimized for agent consumption.
- `/.well-known/skills/index.json` - Agent skill discovery index ([Cloudflare RFC](https://github.com/cloudflare/agent-skills-discovery-rfc)).
- `/llms.txt` - Content index for LLMs.
- `/llms-full.txt` - Full content for LLMs.

IETF Drafts:

- [HTTP-Based AI Agent Discovery and Invocation Protocol](https://www.ietf.org/archive/id/draft-cui-ai-agent-discovery-invocation-00.html) - IETF draft for standardized agent discovery and invocation over HTTP. Published October 2025.
- [Agent Directory Service](https://datatracker.ietf.org/doc/draft-mp-agntcy-ads/) - IETF draft for distributed directory service to store AI agent metadata and enable discovery.
- [BANDAID](https://www.ietf.org/archive/id/draft-mozleywilliams-dnsop-bandaid-00.html) - Brokered Agent Network for DNS AI Discovery. Uses DNS with SVCB records for scalable agent discovery. Published October 2025.
- [DNS-Native AI Agent Naming and Resolution](https://datatracker.ietf.org/doc/draft-cui-dns-native-agent-naming-resolution/) - DNS-native mechanism for agent naming using FQDNs and SVCB records. Published December 2025.
- [AgentDNS](https://datatracker.ietf.org/doc/draft-liang-agentdns/) - Root domain naming and service discovery system for LLM agents. Published October 2025.

### Access Control

- [IETF robots.txt Update](https://www.ietf.org/archive/id/draft-jimenez-tbd-robotstxt-update-00.html) - Adds intent-based policies (training vs. indexing vs. inference), API endpoint discovery, and cryptographic verification.
- [Really Simple Licensing (RSL)](https://rsl.ink/) - AI bot licensing terms embedded in robots.txt. Adopted by Medium, Reddit, Yahoo.
- ai.txt - UK publisher proposal for AI bot permissions (policy-level, not a technical spec).

### API Description

- [agents.json (Wildcard AI)](https://github.com/wild-card-ai/agents-json) - Extends OpenAPI with flows and links optimized for agent consumption.
- [agents.json (jmilinovich)](https://github.com/jmilinovich/agents.json) - Agent permissions and interaction rules, analogous to robots.txt for agents.
- [JSON Agents / PAM](https://jsonagents.org/) - Portable Agent Manifest. Universal JSON format for describing agent capabilities, tools, security, and orchestration.

### Governance

- [Agentic AI Foundation](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation) - Neutral consortium under Linux Foundation (Anthropic, OpenAI, Block). Governs MCP, AGENTS.md, Goose.
- [W3C AI Agent Protocol Community Group](https://www.w3.org/community/agentprotocol/) - Developing open web standards for agent discovery, identification, and collaboration.
- [OWASP Agent Name Service](https://genai.owasp.org/resource/agent-name-service-ans-for-secure-al-agent-discovery-v1-0/) - PKI and JSON schemas for secure agent discovery.

## Tools

### Agent-Readable Content

- [Firecrawl](https://github.com/firecrawl/firecrawl) - Web data API that turns websites into LLM-ready markdown.
- [Crawl4AI](https://github.com/unclecode/crawl4ai) - Open-source LLM-friendly web crawler.
- [llms-txt](https://github.com/AnswerDotAI/llms-txt) - Official llms.txt specification, CLI tools, and Python library.
- [llms-txt-hub](https://github.com/thedaviddias/llms-txt-hub) - Largest curated directory of llms.txt implementations.
- [llmstxt-generator](https://github.com/firecrawl/llmstxt-generator) - Generates llms.txt files by crawling a website.
- [llms-txt-generator (aircode)](https://github.com/aircodelabs/llms-txt-generator) - AI-powered llms.txt generator with MCP integration.

### Agent Discovery & Registration

- [A2A](https://github.com/a2aproject/A2A) - Google's Agent-to-Agent protocol reference implementation.
- [Agent Network Protocol](https://github.com/agent-network-protocol/AgentNetworkProtocol) - Decentralized agent networking with W3C DID-based identity.
- [Agent Cards](https://github.com/commandlayer/agent-cards) - Verifiable identity and capability declarations for autonomous agents.
- [AGNTCY](https://github.com/agntcy) - Open-source infrastructure for inter-agent collaboration.
- [OpenAgents](https://github.com/openagents-org/openagents) - AI agent network infrastructure with MCP and AsyncAPI support.

### Agent-Friendly APIs

- [NLWeb](https://github.com/microsoft/NLWeb) - Natural language endpoints for websites, built on Schema.org. Every instance is also an MCP server.
- [wpnlweb](https://github.com/gigabit-eth/wpnlweb) - WordPress plugin implementing the NLWeb protocol.
- [Manufact](https://www.manufact.com/) - Open-source SDK and platform for building, deploying, and managing MCP servers and AI agents. Y Combinator-backed with 8k+ GitHub stars.

### Agent Web Interaction

- [browser-use](https://github.com/browser-use/browser-use) - Makes websites accessible for AI agents via browser automation.
- [Stagehand](https://github.com/browserbase/stagehand) - SDK for AI browser automation with built-in fail-safes.
- [agent-browser](https://github.com/vercel-labs/agent-browser) - Browser automation CLI for AI agents by Vercel.
- [Notte](https://github.com/nottelabs/notte) - Full-stack framework for building web agents.
- [Steel Browser](https://github.com/steel-dev/steel-browser) - Open-source browser API designed for AI agents.
- [Web Agent Protocol](https://github.com/OTA-Tech-AI/web-agent-protocol) - Standardized framework for recording and replaying browser interactions.
- [TheAgenticBrowser](https://github.com/TheAgenticAI/TheAgenticBrowser) - Open-source AI agent for web automation and scraping.
- [mcp-browser-agent](https://github.com/imprvhub/mcp-browser-agent) - MCP integration providing Claude Desktop with autonomous browser automation capabilities including DOM manipulation and JavaScript execution.
- [Fuji](https://github.com/normal-computing/fuji-web) - AI agent that lives in browser sidepanel for getting tasks done online with a single command.
- [Browser Operator](https://github.com/browseroperator/browser-operator) - AI browser with built-in multi-agent platform, open-source alternative to ChatGPT Atlas and Perplexity Comet.

### MCP Ecosystem

- [MCP Servers (official)](https://github.com/modelcontextprotocol/servers) - Reference server implementations by Anthropic.
- [GitHub MCP Server](https://github.com/github/github-mcp-server) - GitHub's official MCP server in Go.
- [awesome-mcp-servers (punkpeye)](https://github.com/punkpeye/awesome-mcp-servers) - Curated list of MCP servers.
- [awesome-mcp-servers (wong2)](https://github.com/wong2/awesome-mcp-servers) - Another curated list of MCP servers.
- [crawl4ai-mcp-server](https://github.com/sadiuysal/crawl4ai-mcp-server) - Web scraping exposed as MCP tools.
- [AWS MCP Servers (awslabs/mcp)](https://github.com/awslabs/mcp) - Official suite of MCP servers for AWS giving AI applications access to AWS APIs, documentation, pricing, and contextual guidance.

### Skills & Instructions

- [AGENTS.md](https://github.com/agentsmd/agents.md) - Open format for giving coding agents project-specific instructions. 60k+ repos.
- [ClawHub](https://github.com/openclaw/clawhub) - Public skill registry for OpenClaw agents.
- [awesome-openclaw-skills](https://github.com/VoltAgent/awesome-openclaw-skills) - Curated collection of OpenClaw skills.
- [agent-trace](https://github.com/cursor/agent-trace) - Standard format for tracing AI-generated code provenance.
- [microsoft/skills](https://github.com/microsoft/skills) - Skills, MCP servers, and AGENTS.md templates for grounding AI coding agents with Azure SDK and Microsoft AI Foundry knowledge. 131 skills across 6 languages.
- [awesome-agent-skills](https://github.com/skillmatic-ai/awesome-agent-skills) - Comprehensive guide to building and using Agent Skills with learning phases, platforms, and implementation resources.

### GEO & Agent SEO

- [GEO](https://github.com/GEO-optim/GEO) - Research framework for Generative Engine Optimization from Princeton.
- [GetCito](https://github.com/ai-search-guru/getcito-worlds-first-open-source-aio-aeo-or-geo-tool) - Open-source AI search optimization tool.
- [Gego](https://github.com/AI2HU/gego) - Open-source GEO tracker across multiple LLMs.
- [awesome-GEO](https://github.com/amplifying-ai/awesome-generative-engine-optimization) - Curated list of GEO resources and tools.
- [GEO Tools List](https://github.com/izak-fisher/generative-engine-optimization-tools) - Extensive list of commercial and free GEO tools.
- [Profound](https://www.profound.so/) - Market-leading Generative Engine Optimization tracking platform, named G2's Winter 2026 AEO category Leader.
- [Goodie AI](https://higoodie.com/) - Comprehensive GEO platform tracking brand visibility across ChatGPT, Gemini, Perplexity, Claude, Copilot, and DeepSeek with optimization guidance.
- [Birdeye Search AI](https://birdeye.com/products/search-ai) - Tracks and improves how brands and locations appear across AI-powered discovery engines like ChatGPT, Google Gemini, and Perplexity.
- [Geoptie](https://geoptie.com/) - Entry-level GEO tool with accessible $49/mo pricing and 14-day free trial for beginners.
- [Otterly.AI](https://otterly.ai/) - Democratizes GEO monitoring with entry-level tier at $25/month for tracking AI search visibility.
- [Peec AI](https://peec.ai/) - GEO optimization platform with pricing ranging from €89/mo starter to €499/mo enterprise tiers.

### Benchmarking & Testing

- [AI Agent Benchmark Compendium](https://github.com/philschmid/ai-agent-benchmark-compendium) - Directory of 50+ agent benchmarks.
- [TheAgentCompany](https://github.com/TheAgentCompany/TheAgentCompany) - 175-task benchmark in a simulated software company environment.
- [best-of-mcp-servers](https://github.com/tolkonepiu/best-of-mcp-servers) - Ranked list of MCP servers, updated weekly.
- [Terminal-Bench 2.0](https://github.com/laude-institute/terminal-bench) - 89-task hard benchmark for AI agents on real-world terminal tasks, with the Harbor framework for containerized evaluation environments; frontier agents score below 65%. Laude Institute.
- [FeatureBench](https://github.com/LiberCoders/FeatureBench) - ICLR 2026 benchmark of 200 complex feature-development tasks across 24 OSS repos; top agents achieve only 11% vs 74% on SWE-bench, exposing a gap in real-world feature implementation.

## Articles & Talks

### Foundational

- [Introducing AX: Why Agent Experience Matters](https://biilmann.blog/articles/introducing-ax/) - The original AX manifesto. Matt Biilmann, Jan 2025.
- [One Year of AX](https://biilmann.blog/articles/one-year-of-ax/) - Four Pillars framework and AX retrospective. Matt Biilmann, Jan 2026.
- [AX in Practice](https://biilmann.blog/articles/ax-in-practice/) - Three production patterns from Netlify and industry. Matt Biilmann, Jul 2025.
- [Principles of AX](https://agentexperience.ax/concepts/principles-of-ax/) - Community-defined AX principles. agentexperience.ax.
- [Applying AX Practices](https://agentexperience.ax/concepts/applying-ax-practices/) - Five-step implementation checklist. agentexperience.ax.
- [AX, Creativity and the Human Web](https://biilmann.blog/articles/ax-creativity-and-the-human-web/) - How good AX can enhance rather than diminish the open web. Matt Biilmann, Feb 2025.
- [The /llms.txt File Proposal](https://www.answer.ai/posts/2024-09-03-llmstxt.html) - Original llms.txt proposal. Jeremy Howard, Sep 2024.
- [Predictions for 2026: 5 Topics](https://biilmann.blog/articles/predictions-for-2026/) - Predictions on autonomous agents, AX adoption, true computer literacy, and development pipelines. Matt Biilmann, Jan 2026.
- [AX - is it Agent or Agentic?](https://biilmann.blog/articles/ax-is-it-agent-or-agentic/) - Clarifies that AX stands for Agent Experience (not Agentic Experience), by direct analogy with UX and DX. Matt Biilmann.

### Company Perspectives

- [What is AX and How to Improve It](https://resend.com/blog/agent-experience) - Six practical DX-to-AX dimensions. Zeno Rocha / Resend.
- [Agent Experience Is the Only Experience That Matters](https://www.daytona.io/dotfiles/agent-experience-is-the-only-experience-that-matters) - Three requirements for agent-native tools. Ivan Burazin / Daytona.
- [The Age of Agent Experience](https://stytch.com/blog/the-age-of-agent-experience/) - Auth and identity for agent-mediated interactions. Julianna Lamb / Stytch.
- [MCP: A Key Unlock for Delivering a Good AX](https://www.netlify.com/blog/mcp-a-key-unlock-for-delivering-a-good-ax/) - Five community AX principles and MCP's role. Sean Roberts / Netlify.
- [The Agent Web and Its Interface](https://www.netlify.com/blog/continuing-the-ax-conversation-the-agent-web-and-its-interface/) - Content negotiation, natural language APIs, rethinking auth. Dana Lawson / Netlify.
- [Agent-Facing Analytics](https://clickhouse.com/blog/agent-facing-analytics) - Designing analytics systems for agent consumption. Ryadh Dahimene / ClickHouse.
- [Great AX Starts with Great Collaboration](https://liveblocks.io/blog/great-agent-experience-great-collaboration) - Collaborative agent workflows. Steven Fabre / Liveblocks.
- [Making Content AI-Ready](https://www.sanity.io/blog/improving-the-agent-experience-for-sanity-learn) - Plain text content strategy for agent readability. Knut Melvaer / Sanity.
- [Designing APIs for AI](https://abhiaiyer.medium.com/designing-apis-for-ai-the-need-for-new-standards-700a606e9a10) - The case for new API design standards. Abhi Aiyer.
- [AI Go-To-Market](https://docs.buildwithlayer.com/ai_gtm) - Agents as a new path to product adoption. Jonah Katz / Layer.
- [Every Website Needs to be Redesigned for AX](https://www.daeila.com/blog/post-6/) - The case for wholesale redesign. Nathan Daeila.
- [Service Design for AI: Why HX Matters](https://blog.ronbronson.com/service-design-for-ai-why-human-experience-hx-matters) - Counterpoint on keeping humans in the loop. Ron Bronson.
- [Welcome to a New Era of Experience with AI Agents](https://www.salesforce.com/blog/agent-experience-design/) - Introduction to agent experience design as a new expertise area. Salesforce, May 2025.
- [The three biggest agentic commerce trends from NRF 2026](https://stripe.com/blog/three-agentic-commerce-trends-nrf-2026) - Stripe's analysis of emerging agentic commerce patterns from the National Retail Federation conference. Stripe, Jan 2026.
- [Why agentic commerce is the new front door to retail](https://www.microsoft.com/en-us/industry/blog/retail/2026/02/09/how-agentic-commerce-is-becoming-the-new-front-door-to-retail/) - Analysis of how agentic AI is reshaping retail customer experiences and operations. Microsoft, Feb 2026.
- [What is Agent Experience (AX)?](https://nordicapis.com/what-is-agent-experience-ax/) - Foundational explanation of AX with five essential practices for API design. Nordic APIs, Feb 2026.
- [Agent Experience (AX): Why AI Agents Need Their Own Experience Design for B2B](https://www.eglobalis.com/agent-experience-ax-why-ai-agents-need-their-own-experience-design-for-b2b/) - Enterprise-focused AX deployment with emphasis on trusted context and governance. eGlobalis, Feb 2026.
- [AX: Optimizing Your Brand for AI Agents](https://higoodie.com/blog/ax-agent-experience-optimizing-your-brand-for-ai-agents) - How AI agents are reshaping brand discovery and interpretation. Goodie AI, Feb 2026.

### Thought Leadership

- [Simplicity and Agentic Experience](https://johnmaeda.medium.com/simplicity-and-agentic-experience-ax-0087553b73d8) - Simplicity principles applied to AX. John Maeda.
- [Beyond DX: Developers Must Now Learn AX](https://thenewstack.io/beyond-dx-developers-must-now-learn-agent-experience-ax/) - Industry analysis of emerging AX patterns. Richard MacManus / The New Stack.
- [Mastering Agentic Experience](https://shiftmag.dev/matt-biilmann-on-mastering-agentic-experience-6237/) - Biilmann at Shift Conference: 5x signups, 7x conversions after AX focus. ShiftMag.
- [Moltbook Is the Most Interesting Place on the Internet](https://simonwillison.net/2026/Jan/30/moltbook/) - Analysis of the first agent social network and SKILL.md. Simon Willison.
- [Agent Experience and the Future of Web Development](https://www.aviator.co/podcast/agent-experience-and-the-future-of-web-development) - Podcast on the decade of agents. Matt Biilmann / Aviator.
- [First impressions of Claude Cowork](https://simonwillison.net/2026/Jan/12/claude-cowork/) - Analysis of Anthropic's general-purpose agent extending Claude Code functionality to non-developer users. Simon Willison, Jan 2026.
- [Structured Context Engineering for File-Native Agentic Systems](https://simonwillison.net/2026/Feb/9/structured-context-engineering-for-file-native-agentic-systems/) - Analysis of how file formats (YAML, Markdown, JSON, TOON) affect agent accuracy and the "grep tax" phenomenon. Simon Willison, Feb 2026.
- [Introducing the Codex app](https://simonwillison.net/2026/Feb/2/introducing-the-codex-app/) - OpenAI's macOS app for Codex coding agent with first-class Skills and Automations support. Simon Willison, Feb 2026.
- [One Human + One Agent = One Browser From Scratch](https://simonwillison.net/2026/Jan/27/one-human-one-agent-one-browser/) - Case study of building a browser in Rust with one agent and talented engineer in three days. Simon Willison, Jan 2026.
- [An AI Agent Published a Hit Piece on Me](https://simonwillison.net/2026/Feb/12/an-ai-agent-published-a-hit-piece-on-me/) - Analysis of autonomous influence operation targeting supply chain gatekeepers. Simon Willison, Feb 2026.
- [Andrej Karpathy talks about "Claws"](https://simonwillison.net/2026/Feb/21/claws/) - Karpathy's framing of "Claws" as a new orchestration layer above LLM agents: scheduling, context, tool calls, and persistence on personal hardware. Simon Willison, Feb 2026.
- [Writing about Agentic Engineering Patterns](https://simonwillison.net/2026/Feb/23/agentic-engineering-patterns/) - Ongoing pattern series for professional software engineers using coding agents, distinguishing agentic engineering from vibe coding. Simon Willison, Feb 2026.

### VC & Analyst Takes

- **a16z** "Big Ideas 2026" - "We're no longer designing for humans, but for agents." Proposed dual-mode interfaces.
- **Sequoia Capital** - "MCP may become as foundational as TCP/IP." Agent economy requires persistent identity and communication protocols.
- **Bessemer Venture Partners** - Named AX as "Law #1" in AI Developer Laws. Created the AI Agent Autonomy Scale.
- **Forrester** - Five critical AX skills: knowledge curation, change management, critical thinking, interaction skills, agent oversight.
- **McKinsey** - Up to $1T in US retail, $3-5T globally by 2030. "If your catalog is not machine-readable, agents will not find you."
- **BCG** - AI traffic to retail up 4,700% YoY. "Those who wait risk becoming invisible."

## Case Studies

### Agentic Commerce

- **Stripe** - Co-developed Agentic Commerce Protocol (ACP) with OpenAI. Created Shared Payment Tokens (SPTs) as a new payment primitive. Hosts remote MCP server. All docs available as markdown.
- **Shopify** - Co-developed Universal Commerce Protocol (UCP) with Google. "Every store agent-ready by default." AI traffic surged 7x, orders 11x. Key lesson: data quality is the differentiator.
- **Walmart** - "Super Agent" architecture with three personas sharing a single MCP data plane. Cut out-of-stock events by 30% in pilot stores. Partnership with Google Gemini announced Jan 2026.
- **Michael Kors** - Shopping Muse semantic styling agent. 15-20% conversion rate improvement over keyword search.
- **Estée Lauder** - Jo Malone London AI Scent Advisor recreates in-store consultation digitally using Vertex AI and Gemini. 2026.
- **Google/Shopify** - Co-developed Universal Commerce Protocol (UCP) enabling AI agents to transact with merchants. Partners include Etsy, Wayfair, Target, Walmart, Best Buy, and Macy's. Native shopping rolling out in Google Search AI Mode and Gemini app. Jan 2026.
- **Ralph Lauren** - Ask Ralph AI-powered virtual shopping tool creates shoppable outfit combinations personalized to user prompts from Polo collections. Sep 2025.
- **URBN (Anthropologie, Free People, Urban Outfitters)** - Started small with popular categories like dresses and denim, standardizing language and taxonomy for highest impact. 2026.
- **Ulta Beauty** - Strategy focuses on exclusive products and "Only at Ulta" offerings as competitive advantage in agentic AI era. 2026.
- **Mastercard** - Launched Agent Pay, agentic payment infrastructure using Agentic Tokens enabling AI agents to transact securely on behalf of users with full consumer consent and auditability. Integrated with Microsoft Copilot Checkout, OpenAI Instant Checkout, PayPal, Google UCP, and Fiserv. First authenticated agentic transactions completed in Australia, 2026.

### Platform AX

- **Netlify** - Shifted North Star from DX to AX. Anonymous deploy flows, MCP server, context files. Result: 10M developers, 5x daily signups, 7x paid conversions, ~10k AI-generated sites/day.
- **Daytona** - Built agent-native development infrastructure. $1M ARR in 8 weeks.
- **Cloudflare** - First toolkit to securely connect SaaS to Claude via MCP. Published agent-skills-discovery RFC. MCP server deployment reduced from weeks to days.
- **Linear** - Enabled @ mentioning AI agents (Devin, Codegen) directly from tickets. Bidirectional agent-human product interaction.
- **Home Depot** - Magic Apron AI companion provides specialized customer support with access to customer and purchase data for personalized assistance. 2026.
- **Microsoft** - Launched agentic AI solutions for retail including Copilot Checkout (sell within Copilot), Brand Agents for Shopify merchants, personalized shopping agent template, and store operations agent template. Dynamics 365 Commerce MCP Server in preview. Jan 2026.

## Academic Papers

- [GEO: Generative Engine Optimization](https://arxiv.org/abs/2311.09735) - Foundational paper on optimizing content for AI-generated responses. Aggarwal et al., KDD 2024.
- [How to Dominate AI Search](https://arxiv.org/abs/2509.08919) - Strategies for generative engine optimization. Chen et al., 2025.
- [A Survey of AI Agent Protocols](https://arxiv.org/pdf/2504.16736) - Comprehensive survey of the protocol landscape. April 2025.
- [A Survey of Agent Interoperability Protocols](https://arxiv.org/html/2505.02279v1) - Analysis of MCP, A2A, ACP, and other interop standards. May 2025.
- [Structured Context Engineering for File-Native Agentic Systems](https://arxiv.org/abs/2602.05447) - 9,649 experiments showing how file formats affect agent accuracy and token efficiency at scale. McMillan, Feb 2026.
- [Does Prompt Formatting Have Any Impact on LLM Performance?](https://arxiv.org/abs/2411.10541) - Demonstrates up to 40% performance variation from format choice (plain text, Markdown, JSON, YAML). Tam et al., Nov 2024.
- [FeatureBench: Benchmarking Agentic Coding for Complex Feature Development](https://arxiv.org/abs/2602.10975) - 200-task ICLR 2026 benchmark for end-to-end feature development across 24 OSS repos; top agents score 11% vs 74% on SWE-bench, revealing the gap in complex feature implementation capability.

## Related Awesome Lists

- [agentexperience.ax](https://agentexperience.ax/) - The AX community hub by Netlify.
- [awesome-web-agents](https://github.com/steel-dev/awesome-web-agents) - Tools and frameworks for building web-browsing AI agents.
- [awesome-autonomous-web](https://github.com/Agent-Tools/awesome-autonomous-web) - AI agent web interaction tools.
- [awesome_ai_agents](https://github.com/jim-schwoebel/awesome_ai_agents) - 1,500+ resources and tools for AI agents.
- [awesome-ai-agents](https://github.com/slavakurilyak/awesome-ai-agents) - 300+ agentic AI resources.
- [awesome-llm-agents](https://github.com/kaushikb11/awesome-llm-agents) - LLM agent frameworks.

## Research Notes

Detailed research notes compiled during the creation of this repository:

- [llms.txt Deep Dive](research/llms-txt.md) - Spec, adoption, criticism, tools, and generators.
- [SKILL.md & OpenClaw/Moltbook](research/skill-md.md) - Skills standard, Moltbook ecosystem, Cloudflare discovery RFC.
- [HEARTBEAT.md](research/heartbeat-md.md) - Periodic agent check-in pattern.
- [AGENTS.md](research/agents-md.md) - Project instruction standard.
- [Agent Protocols](research/agent-protocols.md) - MCP, A2A, NLWeb, Agent Protocol, IETF drafts.
- [Agent Search Optimization & GEO](research/agent-search-optimization.md) - ASO, GEO, AX as a discipline.
- [AX Perspectives & Frameworks](research/ax-perspectives.md) - 20 industry perspectives on AX best practices.
- [Netlify's AX Canon](research/netlify-ax.md) - Complete index of Netlify/Biilmann AX writings and talks.
- [Terminology Mapping](research/terminology.md) - AX, GEO, ASO, AEO, LLMO -- how the terms relate.
- [File Type Agent Accessibility](research/file-type-agent-accessibility.md) - How file formats affect agent accuracy, token efficiency, and the "grep tax."

## Contribute

[Contributions welcome!](contributing.md) If you know of standards, tools, or resources that should be included, please open an issue or PR.

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the contributors have waived all copyright and related rights to this work.
