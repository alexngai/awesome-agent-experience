---
name: update-awesome-list
description: Research and update the awesome-agent-experience list with new standards, tools, articles, and case studies
allowed-tools: WebSearch WebFetch Read Edit Write Bash(git:*) Bash(wc:*) Bash(date:*)
---

# Update Awesome Agent Experience List

You are maintaining an awesome-list that tracks the Agent Experience (AX) ecosystem -- standards, protocols, tools, articles, and case studies for making technology systems accessible and usable by AI agents.

## What to Research

Search the web for new developments across these categories. For each search, focus on content published **in the last 30 days** unless doing a broader catch-up.

### 1. Standards & Specifications

Look for new or updated standards in the AX space:

- **Content discovery**: New versions or competitors to llms.txt, SKILL.md, AGENTS.md. Search for `"llms.txt" OR "SKILL.md" OR "AGENTS.md" new standard 2026`.
- **Communication protocols**: Updates to MCP, A2A, NLWeb, Agent Protocol, or new protocols. Search for `"model context protocol" OR "agent-to-agent" OR "NLWeb" update 2026`.
- **Discovery mechanisms**: New well-known URIs, agent discovery proposals, IETF drafts. Search for `agent discovery protocol new draft 2026`.
- **Access control**: Updates to robots.txt for AI, RSL, new licensing approaches. Search for `"robots.txt" AI agents update 2026`.
- **API description**: New agents.json variants, OpenAPI extensions for agents. Search for `"agents.json" OR "API for AI agents" standard 2026`.

### 2. Tools & Projects

Look for new or notable open-source projects:

- **Agent-readable content**: LLM crawlers, markdown converters, llms.txt generators. Search GitHub for `llms.txt generator`, `agent readable content`.
- **Agent discovery**: A2A implementations, agent card tools, registries. Search GitHub for `agent card`, `agent discovery`, `a2a protocol`.
- **Agent-friendly APIs**: NLWeb implementations, API adapters for agents. Search GitHub for `NLWeb`, `agent friendly API`.
- **Agent web interaction**: Browser automation for agents, web agent frameworks. Search GitHub for `web agent`, `browser agent`, `browser-use`.
- **MCP ecosystem**: New notable MCP servers. Search GitHub for `mcp server` sorted by stars/recent.
- **Skills**: New skill registries, SKILL.md tooling. Search GitHub for `agent skills`, `SKILL.md`.
- **GEO/Agent SEO**: Optimization tools for AI discovery. Search GitHub for `generative engine optimization`, `GEO tool`.
- **Benchmarking**: Agent testing frameworks. Search GitHub for `agent benchmark`, `agent evaluation`.

### 3. Articles & Thought Leadership

Look for new perspectives on AX:

- **Company perspectives**: Blog posts from tech companies about AX/agent-readiness. Search for `"agent experience" blog 2026`, `designing for AI agents`.
- **Thought leaders**: Posts from Matt Biilmann, Simon Willison, Dharmesh Shah, or others. Search for `site:biilmann.blog`, `site:simonwillison.net agent`.
- **VC/analyst takes**: New reports or predictions. Search for `"agent experience" OR "agentic commerce" report 2026`.
- **Conferences**: New AX-related events. Search for `"agent experience" conference 2026`.

### 4. Case Studies

Look for companies implementing AX:

- **Agentic commerce**: New commerce protocols, agent shopping experiences. Search for `"agentic commerce" case study 2026`.
- **Platform AX**: Companies redesigning for agents. Search for `"agent experience" launch OR redesign 2026`.

## How to Evaluate Items

Before adding an item to the list, verify it meets these criteria:

1. **Relevance**: Directly related to making systems accessible/usable by AI agents.
2. **Quality**: Well-maintained (for projects), well-argued (for articles), credible source.
3. **Novelty**: Not already in the list. Read the current README.md first.
4. **Significance**: Notable enough to be worth including -- not every minor tool or blog post qualifies.

For GitHub projects specifically:
- Prefer projects with meaningful adoption (stars, forks, or known users).
- Verify the repo is active (commits in last 3 months for tools, or established for standards).
- Check that the project description and README are substantive.

For articles:
- Prefer articles with original insights, not summaries of other articles.
- Include the author and their affiliation.
- Prioritize pieces that propose frameworks, share data, or document real implementations.

## How to Update the README

The README follows standard awesome-list conventions:

### Entry Format

Every entry must follow this exact format:
```
- [Name](url) - Description that starts with uppercase and ends with a period.
```

### Section Structure

Add items to the appropriate existing section. The sections are:

```
## Standards
  ### Content Discovery
  ### Communication Protocols
  ### Discovery Mechanisms
  ### Access Control
  ### API Description
  ### Governance
## Tools
  ### Agent-Readable Content
  ### Agent Discovery & Registration
  ### Agent-Friendly APIs
  ### Agent Web Interaction
  ### MCP Ecosystem
  ### Skills & Instructions
  ### GEO & Agent SEO
  ### Benchmarking & Testing
## Articles & Talks
  ### Foundational
  ### Company Perspectives
  ### Thought Leadership
  ### VC & Analyst Takes
## Case Studies
  ### Agentic Commerce
  ### Platform AX
## Academic Papers
## Related Awesome Lists
```

### Rules

1. Add new items at the **bottom** of their section.
2. Do **not** remove existing items unless they are dead links or clearly deprecated.
3. Do **not** rewrite existing item descriptions.
4. If a new section is needed, add it in a logical position and update the TOC.
5. Keep descriptions concise (one sentence).
6. Verify URLs are reachable before adding.

## Workflow

1. Read the current `README.md` to understand what's already listed.
2. Perform web searches across all categories above.
3. Filter results against the evaluation criteria.
4. For each new item, draft the entry in the correct format.
5. Edit `README.md` to add the new entries to the correct sections.
6. If you found enough new items (3+), also update the research notes in `research/` with any significant findings.
7. Commit with a message like: `Update awesome list: add N new resources (Mon YYYY)`.
8. Provide a summary of what was added and what categories were updated.

## Example Output

After running, you should produce a commit that looks like:

```
Update awesome list: add 7 new resources (Feb 2026)

Standards:
- Added FooProtocol to Communication Protocols

Tools:
- Added bar-tool to Agent-Readable Content
- Added baz-mcp to MCP Ecosystem

Articles:
- Added "Title" by Author to Company Perspectives
- Added "Title" by Author to Thought Leadership

Case Studies:
- Added CompanyName to Platform AX
```
