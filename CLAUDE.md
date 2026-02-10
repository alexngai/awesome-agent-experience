# CLAUDE.md

This is an awesome-list repository tracking the Agent Experience (AX) ecosystem.

## Repository Structure

```
README.md                    # The awesome list (standard awesome-list format)
LICENSE                      # CC0 1.0
research/                    # Detailed research notes
  llms-txt.md               # llms.txt standard
  skill-md.md               # SKILL.md & OpenClaw/Moltbook
  heartbeat-md.md           # HEARTBEAT.md pattern
  agents-md.md              # AGENTS.md standard
  agent-protocols.md         # MCP, A2A, NLWeb, etc.
  agent-search-optimization.md # ASO, GEO
  ax-perspectives.md         # Industry perspectives on AX
  netlify-ax.md             # Netlify/Biilmann AX writings
  terminology.md            # Term mapping (AX, GEO, ASO, etc.)
.claude/skills/             # Agent skills
  update-awesome-list.md    # Skill for researching and updating the list
.github/workflows/          # GitHub Actions
  update-list.yml           # Scheduled/manual list update workflow
  claude.yml                # Interactive @claude trigger
```

## Conventions

### README Format

This repo follows [awesome-list conventions](https://github.com/sindresorhus/awesome):

- Every entry: `- [Name](url) - Description starting with uppercase, ending with period.`
- Items go at the bottom of their section.
- No tables for link lists -- bullet points only.
- Keep descriptions to one sentence.

### Adding New Items

1. Add to the correct section in README.md.
2. If the item represents a significant new development, also update the relevant file in `research/`.
3. Never remove existing items unless they are dead links or clearly deprecated.
4. If a new section is needed, add it logically and update the TOC.

### Commit Messages

- Updates: `Update awesome list: add N new resources (Mon YYYY)`
- Structural changes: descriptive message about what changed

## Key Context

- AX (Agent Experience) was coined by Matt Biilmann (Netlify) in January 2025.
- The field spans: content discovery (llms.txt, SKILL.md), protocols (MCP, A2A, NLWeb), optimization (GEO), and governance (Agentic AI Foundation, W3C, IETF).
- This is a fast-moving space. Standards and tools emerge frequently.
