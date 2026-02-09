# Netlify's AX Canon

A comprehensive index of Netlify and Matt Biilmann's Agent Experience writings.

## Biilmann Blog Articles

### "Introducing AX: Why Agent Experience Matters" (Jan 28, 2025)
- **URL:** https://biilmann.blog/articles/introducing-ax/
- Coined the term AX. Draws lineage: UX (1993) -> DX (2011) -> AX (2025)
- Core argument: autonomous AI agents are a new class of user; products that fail to design for them become irrelevant
- Open model (enabling external agents) vs. Closed model (proprietary agents locked in ecosystems)
- Essential AX components: simplified agent access, clean APIs, machine-readable docs, LLM-optimized context, collaboration flows

### "AX, Creativity and the Human Web" (Feb 18, 2025)
- **URL:** https://biilmann.blog/articles/ax-creativity-and-the-human-web/
- Good AX can enhance the web's creative potential rather than diminish it
- Threats: AI aggregators pulling interactions into proprietary platforms, content disintermediation
- Invokes Paul Virilio: "The invention of the ship was also the invention of the shipwreck"

### "AX in Practice: Real-World Examples" (Jul 14, 2025)
- **URL:** https://biilmann.blog/articles/ax-in-practice/
- Three production patterns:
  1. Agent-First Onboarding -- "Deploy anonymously, then claim" (Netlify, Clerk, Prisma, Neon)
  2. Agent-Human Interactions Within Products -- Bidirectional linking, @ mentions (Linear)
  3. Context Engineering for LLMs -- llms.txt, .cursorrules, AGENTS.md, MCP

### "AX -- Is it Agent or Agentic?" (Sep 8, 2025)
- **URL:** https://biilmann.blog/articles/ax-is-it-agent-or-agentic/
- Defends "Agent Experience" over "Agentic Experience"
- Just as "User Experience" not "Useric Experience"

### "3 Billion Developers" (Sep 12, 2025)
- **URL:** https://biilmann.blog/articles/3-billion-developers/
- AI code agents expand development from ~17M professionals to potentially 3 billion people

### "Predictions for 2026" (Jan 7, 2026)
- **URL:** https://biilmann.blog/articles/predictions-for-2026/
- AX expands beyond dev tools to all digital experiences
- "Agent Skills will become more relevant than MCP servers"
- Formal syntax and rigid data structures become obsolete

### "One Year of AX" (Jan 28, 2026)
- **URL:** https://biilmann.blog/articles/one-year-of-ax/
- The Four Pillars: Access, Context, Tools, Orchestration
- BVP named AX as "Law #1"; Sequoia: "product-led growth to agent-led growth"
- Netlify crossed 10M developers by shifting North Star from DX to AX

## Netlify Blog Articles

### "The Era of Agent Experience (AX)" -- Sean Roberts (Jan 28, 2025)
- **URL:** https://www.netlify.com/blog/the-era-of-agent-experience-ax/
- AX is "the experience agents have while working with content we produce or systems we expose"

### "The Agent Web and Its Interface" -- Dana Lawson (Feb 6, 2025)
- **URL:** https://www.netlify.com/blog/continuing-the-ax-conversation-the-agent-web-and-its-interface/
- Four innovations: Purposeful Views, Content Negotiation, Natural Language APIs, Rethinking Authentication

### "MCP: A Key Unlock for Delivering a Good AX" -- Sean Roberts (Apr 24, 2025)
- **URL:** https://www.netlify.com/blog/mcp-a-key-unlock-for-delivering-a-good-ax/
- Five community-defined AX principles: Human Centricity, Agent Accessibility, Contextual Alignment, Agent Interactivity Patterns, Differentiate Agent Interaction

### "AI as a Better Pair Programmer with AX" (2025)
- **URL:** https://www.netlify.com/blog/ai-better-pair-programmer-with-agent-experience/
- Context files (.mdc, .txt) providing agents with project architecture
- Without context: agents generate outdated patterns; with context: modern, correct code

### "Agent Week 2025" (Jun 2, 2025)
- **URL:** https://www.netlify.com/blog/agent-week-2025/
- "Agents excel at generating code but need infrastructure specifically designed for them"

## Talks and Presentations

### AI Native DevCon 2025 Keynote (Jun 2025)
- **Source:** https://tessl.io/blog/agentic-experience
- Canonical anecdote: Bolt.new generated code but failed because it couldn't toggle a Netlify setting documented only for humans
- 1,000+ ChatGPT-deployed sites daily, scaling to ~10,000

### Infobip Shift Conference (Oct 2025)
- **Source:** https://shiftmag.dev/matt-biilmann-on-mastering-agentic-experience-6237/
- Three core challenges: Access, Context, Tools
- Business impact: 5x daily signups, 7x paid conversions
- "Treat MCP like a user interface -- carefully designed with minimal necessary tools and context"

### Aviator Podcast
- **Source:** https://www.aviator.co/podcast/agent-experience-and-the-future-of-web-development
- "We're at the start of the decade of agents"

## agentexperience.ax Community Site

- **URL:** https://agentexperience.ax/
- Community-driven, open-source AX hub
- Published formal principles for both digital services and agents themselves
- Five-step implementation checklist
- Agent identity recommendation: User-Agent headers like `agent-TOOL claude-3.5-sonnet modality-plaintext`
