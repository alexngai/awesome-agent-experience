# Agent Experience (AX): Perspectives from Industry

A survey of what different companies, thought leaders, VCs, analysts, and practitioners are saying about Agent Experience best practices as of early 2026.

---

## 1. Mathias Biilmann (Netlify CEO) — Coined the Term AX

**Source:** [Introducing AX: Why Agent Experience Matters](https://biilmann.blog/articles/introducing-ax/) (Jan 2025) and [One Year of AX](https://biilmann.blog/articles/one-year-of-ax/) (Jan 2026)

**Key arguments:**
- Coined the term AX (Agent Experience) in January 2025, defining it as "the holistic experience AI agents will have as the user of a product or platform."
- AX is positioned as the natural successor to UX and DX—just as companies optimized for human users and then developers, they must now optimize for AI agents.
- After one year: first AX job postings appeared, BVP named AX as their Law #1 in their AI Developer laws, Sequoia's Sonya Huang stated we are going from "the age of product-led growth to the age of agent-led growth."
- Netlify crossed 10 million developers by making AX their North Star, welcoming a new audience of AI agents building on the web.

**Framework — Four key areas of AX:**
1. **Access** — Can the agent access your product with the right permissions?
2. **Context** — Does the LLM know about your product and have the right context?
3. **Tools** — Are you building your product for agents?
4. (Fourth area referenced but the full detail requires the original article)

**Key quote:** "As agents emerge beyond development, AX will go from being primarily understood as a new type of developer experience to being as generally applicable as UX itself."

---

## 2. agentexperience.ax — The AX Principles Framework

**Source:** [Principles of AX](https://agentexperience.ax/concepts/principles-of-ax/) | [Getting Started](https://agentexperience.ax/concepts/getting-started/) | [Applying AX Practices](https://agentexperience.ax/concepts/applying-ax-practices/)

**Seven core principles:**
1. **Human-Centered Focus** — Agents are delegates of humans; the human end user never stops being the focus.
2. **Agents as First-Class Medium** — Agents are a first-class medium alongside browsers and mobile apps.
3. **Context Delivery** — Use MCP, llms.txt, Arazzo, and agents.json for delivering context to agents.
4. **Standardized Interactivity** — Incorporate patterns that inform agents how the service expects interactions.
5. **Agent Identification & Analytics** — Differentiate agent traffic from human traffic for debugging and insights.
6. **Mutual Respect** — Services blocking agents should expect agents to send users to competitors; agents operating outside boundaries should expect to be blocked.
7. **Optimized Consumption** — Agents consume services differently than humans; support the latest AX patterns for cost-effective consumption.

**Practical guidance:**
- Assess agent readiness: Are APIs well-documented and machine-readable?
- Optimize documentation for AI: Provide OpenAPI specs, structured metadata, and regularly updated docs.
- Determine key areas where users will want AI agents to act on their behalf (customer service, content creation, workflow automation, data management).

---

## 3. Stripe — Agentic Commerce Suite & Open Protocols

**Sources:**
- [Developing an Open Standard for Agentic Commerce](https://stripe.com/blog/developing-an-open-standard-for-agentic-commerce)
- [Introducing the Agentic Commerce Suite](https://stripe.com/blog/agentic-commerce-suite)
- [Add Stripe to Your Agentic Workflows](https://docs.stripe.com/agents)
- [Build on Stripe with LLMs](https://docs.stripe.com/building-with-llms)

**Key contributions:**
- Co-developed the **Agentic Commerce Protocol (ACP)** with OpenAI — an open standard (Apache 2.0) enabling programmatic commerce flows between buyers, AI agents, and businesses.
- Launched the **Agentic Commerce Suite** (Dec 2025) — a single integration to make products discoverable, simplify checkout, and accept agentic payments. Without it, supporting each new AI agent takes up to six months.
- Created **Shared Payment Tokens (SPTs)** — a new payment primitive for AI commerce. Tokens are scoped, time-limited, revocable, and work with existing PaymentIntents.
- Hosts a remote **MCP server** at mcp.stripe.com for secure OAuth-based access.
- All Stripe docs available as plain markdown by appending `.md` to any URL — a key AX pattern for LLM consumption.

**Best practices cited:**
- Use restricted API keys to limit agent permissions.
- Run in sandbox mode and use evaluations (outputs are contextual, not binary).
- Traditional metrics like test coverage don't work for agentic systems; the question is "Did it run the right tool, with the right data, in the right order?"
- Fraud detection must adapt: AI agents lack human variability and can be misflagged.

---

## 4. Shopify — Agentic Commerce Platform & Universal Commerce Protocol

**Sources:**
- [The Agentic Commerce Platform](https://www.shopify.com/news/ai-commerce-at-scale)
- [Agentic Commerce Developer Docs](https://shopify.dev/docs/agents)
- [AI-native, Developer-ready: Winter '26 Edition](https://www.shopify.com/news/winter-26-edition-dev)
- [Shopify Leans into Agentic Commerce](https://betakit.com/shopify-continues-agentic-commerce-push-with-new-open-standard-google-microsoft-deals/)

**Key contributions:**
- Co-developed the **Universal Commerce Protocol (UCP)** with Google — an open standard establishing common language and primitives for agents, merchants, PSPs, and credential providers.
- "Every Shopify store agent-ready by default" (Tobi Lutke).
- AI-driven traffic to Shopify stores surged **7x** and orders attributed to AI jumped **11x** in 2025.
- Morgan Stanley estimates agentic shoppers could capture **$190B-$385B** of US e-commerce spending by 2030.

**Best practices:**
- **Data quality is the key differentiator**: stores with incomplete product data, stale inventory, or thin descriptions are invisible to agents.
- Developers can build full agent flows: search, selection, and checkout with Checkout Kit, all within the agent experience.
- **Dev Dashboard** is the all-in-one workspace for Shopify's agentic commerce tools (APIs, MCPs, SDKs).
- Agentic Storefronts: tools for product discoverability and brand authenticity in agent conversations.

---

## 5. Postman — 2025 State of the API Report

**Sources:**
- [2025 State of the API Report](https://web.postman.com/state-of-api/2025/)
- [One in Four Developers Now Design APIs for AI Agents (BusinessWire)](https://www.businesswire.com/news/home/20251008162423/en/One-in-Four-Developers-Now-Design-APIs-for-AI-Agents-According-to-Postmans-2025-State-of-the-API-Report)
- [How to Orchestrate APIs for AI-Driven Workflows](https://blog.postman.com/how-to-orchestrate-apis-for-ai-workflows/)
- [Postman's Three Rules for Building Intelligent Enterprises](https://www.insightpartners.com/ideas/postman-ai-agents/)

**Key data:**
- **24.3% of developers** are already designing APIs with AI agents in mind.
- **60% still design APIs primarily for human consumption only.**
- Two-thirds of developers are aware of MCP, but only 10% use it regularly (24% plan to explore).
- Survey of 5,700+ developers, architects, and executives.

**Best practices for AI-ready APIs:**
1. Machine-readable schemas with comprehensive OpenAPI specs (detailed examples, error codes, response formats).
2. Predictable patterns across endpoints (consistent naming, standard HTTP codes, uniform auth).
3. Comprehensive documentation that explains *when and why* to use endpoints, not just *how*.
4. Robust error handling with typed error responses that provide actionable information.
5. Rate limiting and auth designed for high-frequency automated access patterns.

**Four priorities for organizations:**
1. Design APIs for AI agents, not just humans.
2. Evolve security models to handle non-human consumers.
3. Fix documentation and discovery to create a single source of truth.
4. Treat APIs as revenue-driving products, not technical projects.

**Key quote:** "AI agents fail when they encounter slow APIs, inconsistent error messages, or incomplete documentation. Unlike developers, agents can't adapt to poor interfaces."

---

## 6. Cloudflare — MCP Server Infrastructure for Agents

**Source:** [Cloudflare Helps Anthropic and Leading Tech Companies Unlock Real AI Agent Experiences (BusinessWire)](https://www.businesswire.com/news/home/20250501890304/en/Cloudflare-Helps-Anthropic-and-Leading-Tech-Companies-to-Unlock-Real-AI-Agent-Experiences-Through-Claude)

**Key contributions:**
- First and only simple toolkit to quickly, securely, and remotely connect SaaS services to Anthropic's Claude via MCP.
- Building and deploying remote MCP servers on Cloudflare takes **days instead of weeks**.
- Simplifies complex authentication/authorization, provides agent permission controls, and offers visibility into data access and actions.

**Companies deploying on Cloudflare:**
- **Asana:** Work Graph connected to AI tools via MCP.
- **Webflow:** Developers use AI agents/APIs to manage CMS, generate blogs, improve SEO.
- **PayPal:** Remote MCP server for managing inventory, processing payments, tracking shipping, handling refunds via natural language.

---

## 7. a16z (Andreessen Horowitz) — Agent-First Design

**Sources:**
- [Agent Experience: Building an Open Web for the AI Era (podcast)](https://a16z.com/podcast/agent-experience-building-an-open-web-for-the-ai-era/)
- [Emerging Developer Patterns for the AI Era](https://a16z.com/nine-emerging-developer-patterns-for-the-ai-era/)
- [Big Ideas 2026: Part 1](https://a16z.com/newsletter/big-ideas-2026-part-1/)
- [Notes on AI Apps in 2026](https://a16z.com/notes-on-ai-apps-in-2026/)

**Three major predictions (Big Ideas 2026):**
1. **The Disappearance of the Input Box** — Marc Andrusko: "By 2026, the input box as the main UI for AI applications will disappear."
2. **Create for Agents, Not Humans** — Stephanie Zhang: "What is important for human consumption may no longer be important for agent consumption. The new optimization direction is not visual hierarchy, but machine legibility."
3. **Voice agents transition from demos to large-scale deployment.**

**Core design principles:**
- **Machine legibility over visual hierarchy** — optimize for how agents parse and act.
- **Dual-mode interfaces** — build both human-facing and agent-facing views.
- **Clean APIs and machine-ready documentation.**
- **Move from prompting to execution** — interfaces should enable agents to take direct action.
- **Design for exploration, not just execution** — help users think about *what* to build.

**Key quote:** "We're no longer designing for humans, but for agents."

---

## 8. Sequoia Capital — The Agent Economy

**Sources:**
- [AI in 2026: A Tale of Two AIs](https://sequoiacap.com/article/ai-in-2026-the-tale-of-two-ais/)
- [AI Ascent 2025 Conference](https://sequoiacap.com/article/ai-ascent-2025/)
- [AI 50: AI Agents Move Beyond Chat](https://sequoiacap.com/article/ai-50-2025/)

**Key arguments:**
- Konstantine Buhler outlined the "agent economy" where agents transfer resources, make transactions, and develop their own economic relationships.
- Three technical challenges for the agent economy: **persistent identity**, **seamless communication protocols** (TCP/IP equivalent for agents), **security**.
- Sonya Huang: "We are going from the age of product-led growth to the age of agent-led growth."
- Greatest value will be created at the application layer, not foundation models.
- MCP may become as foundational as TCP/IP.

**Design advice for founders:**
- Design for composability: agents, tools, and platforms that integrate well will win.
- Watch protocol layers as infrastructure.
- Two vectors for agent capability: RL (intrinsic training) and Agent Harnesses/Scaffolding (external engineering — memory, state handoff, guardrails, retry logic).

---

## 9. Bessemer Venture Partners — AI Agent Autonomy Scale

**Sources:**
- [The State of AI 2025](https://www.bvp.com/atlas/the-state-of-ai-2025)
- [Bessemer's AI Agent Autonomy Scale](https://www.bvp.com/atlas/bessemers-ai-agent-autonomy-scale)
- [Roadmap: AI Systems of Action](https://www.bvp.com/atlas/roadmap-ai-systems-of-action)

**Key contributions:**
- Named **AX as their Law #1** in their AI Developer laws.
- Developed the **AI Agent Autonomy Scale** — a framework inspired by self-driving car levels, comparing AI agent readiness across industries and use cases.
- Define an AI agent as "a software application of a foundation model that can execute chain-of-thought reasoning to take action on sequenced workflows accurately."
- MCP expected to become "as foundational to an agent-native web as HTTP was to the internet."

---

## 10. Forrester — AX as Organizational Discipline

**Source:** [Prepare Your Workforce For An Agentic Future With An Agent Experience Program](https://www.forrester.com/blogs/prepare-your-workforce-for-an-agentic-future-with-an-agent-experience-program/) (Nov 2025)

**Key arguments:**
- AX (Agent Experience) is "the discipline to prepare an organization to successfully integrate agents as collaborative partners with the human workforce."
- For every dollar spent on AI agent licensing, organizations spend **nearly five dollars** on services to get them running at scale.
- The transition to a hybrid agent/human workforce is expensive and not well understood.

**Five critical AX skills:**
1. Knowledge curation
2. Change management
3. Critical thinking
4. Interaction skills
5. Agent oversight

**Key insight:** Organizations must redesign systems around "new digital minds" — just as modern warehouses are designed around physical robotics, organizations must design operating models around cognitive automation.

---

## 11. McKinsey — The Agentic Commerce Opportunity

**Sources:**
- [The Agentic Commerce Opportunity](https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-agentic-commerce-opportunity-how-ai-agents-are-ushering-in-a-new-era-for-consumers-and-merchants) (Oct 2025)
- [The Automation Curve in Agentic Commerce](https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-automation-curve-in-agentic-commerce)

**Key data:**
- By 2030, up to **$1 trillion** in US B2C retail revenue could be directed by agentic commerce; **$3-5 trillion** globally.
- ChatGPT processes approximately **50 million shopping-related queries daily**.
- Half of all consumers now use AI when searching the internet.

**Framework — The Automation Curve (levels of delegation):**
- Level 1: Agents help shoppers think/decide but don't execute (scan catalogs, parse reviews, compare features).
- Higher levels: Increasing autonomous execution through to full agent-mediated purchasing.

**Three interaction models:**
1. Agent-to-site
2. Agent-to-agent
3. Brokered agent-to-site

**Key recommendation:** "Retailers must treat AI agents almost as a new customer class. If your catalog, policies, and value proposition are not machine-readable, agents — and by extension, shoppers — simply will not find you."

---

## 12. BCG — Agentic Commerce Redefining Retail

**Source:** [Agentic Commerce is Redefining Retail — How to Respond](https://www.bcg.com/publications/2025/agentic-commerce-redefining-retail-how-to-respond) (Oct 2025)

**Key data:**
- AI traffic to US retail sites increased **4,700%** year-over-year (July 2025, Adobe data).
- Shoppers arriving via AI agents spend **32% more time** on sites and have **27% lower bounce rate**.
- AI agents are 10% more engaged than traditional visitors.
- By 2029, spending on AI search ads in the US will reach **$26 billion** (~14% of total search ad spend).
- 96% of global retailers are exploring or implementing AI agents.

**Three-pronged strategy:**
1. **Optimize Visibility on Third-Party AI Platforms** — master "answer engine optimization" so chatbots can understand and recommend products.
2. **Build Proprietary Agentic Experiences** — branded AI agents, workforce agents for associates, partner agents for suppliers.
3. **Establish Foundational Capabilities** — scalable AI platforms, new measurement systems, governance for ethical risks, workforce training.

**Key warning:** "This is not a future-state ambition — it's a strategic imperative today. Those who move now will define the next era of customer engagement. Those who wait risk becoming invisible."

---

## 13. Simon Willison — Designing Agentic Loops & "Desire Paths"

**Sources:**
- [Designing Agentic Loops](https://simonwillison.net/2025/Sep/30/designing-agentic-loops/)
- [Agentic Coding: The Future of Software Development with Agents](https://simonwillison.net/2025/Jun/29/agentic-coding/)
- [A Quote from Steve Yegge (on Desire Paths)](https://simonwillison.net/2026/Jan/30/steve-yegge/)

**Key concepts:**
- **Designing agentic loops** is a critical new skill: carefully selecting tools to run in a loop to achieve a specified goal. "Do this well and you can solve many coding problems with brute force."
- **"Desire Paths" design** (via Steve Yegge's Beads project): build CLIs and tools to match what agents *expect* to exist. "Make their hallucinations real, over and over, by implementing whatever I saw the agents trying to do, until nearly every guess by an agent is now correct."
- Tools should provide **very clear errors** so agents can recover when things go wrong.
- The human role shifts to designing systems that help agents work effectively — researching approaches, designing agentic loops, planning QA, managing digital workers.
- Coding agents are "brute force tools": if you can reduce your problem to a clear goal + a set of tools that iterate toward that goal, agents can brute force a solution.

**Key quote:** "You're not just responsible for writing code — you're researching approaches, designing agentic loops, planning QA, and managing a growing army of weird digital interns."

---

## 14. Dharmesh Shah (HubSpot CTO) — Agent.ai & The Decade of Agents

**Sources:**
- [HubSpot Cofounder Rolls Out Marketplace for AI Agents (Boston Globe)](https://www.bostonglobe.com/2025/01/31/business/hubspot-dharmesh-shah-ai-artificial-intelligence-agents/)
- [Agent.ai](https://agent.ai/profile/dharmeshai)
- [simple.ai Newsletter](https://simple.ai/)

**Key contributions:**
- Built **Agent.ai** — "the professional network for AI agents" — reaching **2+ million users** and **26,000+ agent builders** by end of 2025.
- At INBOUND 2025: "This is not the year of AI agents. This is the **decade** of AI agents."
- Named by Biilmann as one of the early visionaries adopting AX outside developer tools.

**TEAM Framework for organizations:**
1. **T**riage — list and prioritize AI use cases
2. **E**xperiment — try, iterate, refine
3. **A**utomate — build workflows or agents to scale
4. **M**easure — track results

**Key quote:** "AI is the most consequential, and also the most controversial, technology of our time."

---

## 15. John Maeda — Simplicity and AX

**Source:** [Simplicity and Agentic Experience (AX)](https://johnmaeda.medium.com/simplicity-and-agentic-experience-ax-0087553b73d8) (Apr 2025)

**Key arguments:**
- Traditional interfaces are "obstacle courses" requiring users to navigate complex pathways. Agentic experiences are the **ultimate expression of the simplicity principle**.
- Applies his Tenth Law of Simplicity: "Simplicity is about subtracting the obvious and adding the meaningful."
- The shift from UX to AX means designers become **orchestrators of experiences** rather than crafters of interfaces.
- Challenge: create agents that understand users deeply enough that technology seems to disappear, leaving only effortless accomplishment of goals.
- Advances in **agentic memory architectures** will be critical for this vision.

---

## 16. Resend — Practical AX for Developer Tools

**Source:** [What is AX (Agent Experience) and How to Improve It](https://resend.com/blog/agent-experience)

**Key best practices:**
1. **APIs over SDKs** — Agents can write their own SDKs; a well-structured REST API with OpenAPI spec is the best "SDK" for an agent.
2. **Frictionless onboarding** — Agents can't "contact sales" or "book a demo." They pick whatever tool is easiest.
3. **Audit logs** — Differentiate between human and agent actions for triage.
4. **API key management** — Keys that can create other, less permissive keys. Agents must be able to create, delete, and rotate keys.
5. **Granular RBAC** — Agents need more granular permissions than humans. High-risk/destructive actions may need human confirmation.

**Poor AX vs. Great AX:**
- Poor: Agent fails, burns tokens on multiple paths, requires human takeover.
- Great: Agent completes task in a single run, cost-effectively, no human intervention.

---

## 17. Speakeasy — Practical Guide to AX Architecture

**Source:** [Designing Agent Experience: A Practical Guide for the Era of AX](https://www.speakeasy.com/blog/agent-experience-introduction)

**Core AX principles:**
- **Toolability** — Expose only tools agents actually need, with clear docs and proper scoping. Don't overwhelm an agent with 300 operations across all departments.
- **Recoverability** — Agents must handle failures gracefully with retry logic, alternate paths, and user communication.
- **Security** — Core pillar of AX; poorly designed access controls lead to data leaks, unintended behavior, or dangerous operations.
- **Tool Curation** — Speakeasy supports automated tool curation using `x-speakeasy-mcp` extension for scoped MCP server generation.

**AX bridges UX and DX:** Agents may need to understand/serve users AND interface with APIs, databases, and infrastructure.

---

## 18. Twilio — Dual Agent Strategy (Virtual + Human)

**Sources:**
- [Conversational AI](https://www.twilio.com/en-us/products/conversational-ai)
- [Agent Productivity](https://www.twilio.com/en-us/lp/agent-productivity)

**Approach:**
- Dual strategy: empowering **virtual AI agents** for self-service AND augmenting **live human agents** through AI copilots.
- **ConversationRelay** — virtual agent solution supporting voice calls with human-like experiences; developers bring their own LLM.
- **Agent Copilot** — real-time suggestions, auto-surfaced knowledge base articles, conversation summaries, automated wrap-ups.
- Integration with OpenAI Realtime API for reduced latency, tone/pitch analysis, interruption handling.

---

## 19. UX Design Perspectives — Designing for AI Agents

**Sources:**
- [Aubergine — Designing for AI Agents: A Human-Centered Approach](https://www.aubergine.co/insights/designing-for-ai-agents)
- [UX Design Institute — How to Design Experiences for AI Agents](https://www.uxdesigninstitute.com/blog/design-experiences-for-ai-agents/)

**Key principles:**
1. **Clarify the agent's role** — Is it a helper, collaborator, or orchestrator?
2. **Design for outcomes, not inputs** — Anticipate and pursue goals rather than expecting explicit commands.
3. **Design for orchestration across platforms** — Agents thrive when not siloed.
4. **Make the invisible visible** — Lightweight cues showing how/where the agent is acting.
5. **Build trust over time** — Frame agents as adaptive partners; trust compounds.

**Data cited:** PwC's May 2025 survey indicates 79% of senior executives report their companies are already utilizing AI agents.

---

## 20. Walmart — "Super Agent" Architecture (Case Study)

**Source:** [Agentic Commerce in 2025: What We Learned (MetaRouter)](https://www.metarouter.io/post/agentic-commerce-in-2025-what-we-learned)

**Architecture:**
- Built a "Super Agent" architecture powered by MCP with three agent personas:
  - **Sparky** (customer-facing)
  - **Associate** (employee-facing)
  - **Marty** (supplier-facing)
- All share a single data plane; when inventory updates, all agents read from the same source automatically.
- **Data consistency across surfaces** is what makes agent commerce work.
- Cut out-of-stock events by **30%** in a pilot store within six months using agentic AI for inventory management.

---

## Cross-Cutting Themes

### Theme 1: Machine Legibility is the New SEO
Every source emphasizes that products/services must be **machine-readable** to be visible to agents. This encompasses OpenAPI specs, structured data, llms.txt, markdown docs, and consistent API patterns.

### Theme 2: Agents as a New Customer Class
McKinsey, BCG, and Shopify all frame agents as a **new type of customer** that must be designed for explicitly, with their own needs around data format, authentication, error handling, and trust.

### Theme 3: Security and Permissions Must Be Rethought
Stripe (restricted API keys, SPTs), Resend (granular RBAC), Speakeasy (security as AX pillar), and a16z (dual-mode interfaces) all stress that agent permissions require fundamentally different security models than human users.

### Theme 4: Speed of Transformation
BCG's 4,700% traffic increase, Shopify's 7x/11x surge, and McKinsey's comparison to "a transformation akin to e-commerce — only faster" all indicate this shift is happening now, not in some distant future.

### Theme 5: From DX to AX
Multiple sources (Biilmann, BVP, a16z, Resend) argue that just as DX emerged as a discipline from UX, AX is emerging from DX. Companies that invest in AX early will capture outsized value.

### Theme 6: Open Protocols are Critical
The proliferation of open standards — ACP (Stripe/OpenAI), UCP (Shopify/Google), MCP (Anthropic), AP2 (Google/Mastercard), A2A (Google) — suggests the infrastructure layer is being built now, and participation in these standards is a strategic imperative.
