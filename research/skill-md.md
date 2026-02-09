# SKILL.md & the OpenClaw/Moltbook Ecosystem

## Moltbook

**Moltbook** is the world's first social network designed exclusively for AI agents, launched in January 2026 by entrepreneur Matt Schlicht. It presents itself as "the front page of the agent internet."

- Only verified AI agents can post, comment, upvote, or create communities ("Submolts")
- By early February 2026: 1.5 million registered agents, ~17,000 human controllers
- Agents generated original content across 2,364+ topic-based communities
- Emergent behaviors included digital religions, economic exchange systems, and governance structures

**Note:** There is no "Molteo" platform -- the correct name is **Moltbook**, powered by the **OpenClaw** framework.

## OpenClaw (formerly Moltbot/Clawdbot)

**OpenClaw** is the free and open-source autonomous AI agent framework that powers Moltbook interactions, created by Peter Steinberger.

- Originally "Clawdbot" (Anthropic requested a name change), then "Moltbot," then "OpenClaw"
- Over 114,000 GitHub stars
- Bots run locally, integrate with LLMs (Claude, GPT, DeepSeek), use messaging platforms as UI
- Extended through a **skills system** -- folders of markdown instructions and optional scripts

## How Moltbook Uses SKILL.md

This is the mechanism where "agents access the site/service with /SKILLS.md":

1. A human sends their OpenClaw agent a link to `https://www.moltbook.com/skill.md`
2. The agent reads the markdown file containing installation instructions
3. The agent executes the instructions, downloading files into `~/.moltbot/skills/moltbook/`:
   - `SKILL.md` -- Core instructions
   - `HEARTBEAT.md` -- Periodic task instructions
   - `MESSAGING.md` -- Messaging capabilities
   - `package.json` -- Skill metadata
4. The agent registers itself with Moltbook's API
5. Alternatively: `clawhub install moltbook`

## SKILL.md as an Open Standard

SKILL.md has evolved from a Moltbook/OpenClaw mechanism into a **broad open standard for agent capability discovery**, now maintained by Anthropic.

**Official specification:** [agentskills.io/specification](https://agentskills.io/specification)

### File Format

```yaml
---
name: skill-name          # Required, max 64 chars, lowercase + hyphens
description: What it does  # Required, max 1024 chars
license: Apache-2.0       # Optional
compatibility: Requires git, docker  # Optional
metadata:                  # Optional
  author: example-org
  version: "1.0"
allowed-tools: Bash(git:*) Read  # Optional, experimental
---

[Markdown body with instructions, examples, edge cases]
```

### Directory Structure

```
my-skill/
  SKILL.md        # Required: instructions + metadata
  scripts/        # Optional: executable code
  references/     # Optional: documentation
  assets/         # Optional: templates, resources
```

### Progressive Disclosure (Context Efficiency)

| Level | Content | When Loaded | Cost |
|-------|---------|-------------|------|
| 1 - Discovery | Name + description only | At startup | ~100 tokens |
| 2 - Activation | Full SKILL.md body | When task matches | <5,000 tokens |
| 3 - Execution | Scripts, references, assets | On demand | Unlimited |

## Cloudflare's Agent Skills Discovery RFC

Cloudflare published an RFC for standardized web-based skill discovery using `.well-known` URIs (RFC 8615).

**Repository:** [cloudflare/agent-skills-discovery-rfc](https://github.com/cloudflare/agent-skills-discovery-rfc)

### URL Structure

```
/.well-known/skills/index.json              # Required index file
/.well-known/skills/{skill-name}/           # Skill directory
/.well-known/skills/{skill-name}/SKILL.md   # Skill instructions
```

### Discovery Index Format

```json
{
  "skills": [
    {
      "name": "skill-identifier",
      "description": "What this skill does",
      "files": ["SKILL.md", "references/docs.md"]
    }
  ]
}
```

### Agent Discovery Flow

1. Fetch `/.well-known/skills/index.json`
2. Enumerate available skills and metadata
3. Download and cache files
4. Apply progressive disclosure
5. Require user confirmation before executing scripts

**Mintlify adoption:** Now serves all docs sites with `/.well-known/skills/default/skill.md` plus a convenience path at `/skill.md`.

## Platform Adoption

| Platform | Skill Location | Notes |
|----------|----------------|-------|
| **Claude Code** | `~/.claude/skills/`, `.claude/skills/` | Original creator |
| **OpenAI Codex** | Built-in | "Builds on the open agent skills standard" |
| **GitHub Copilot** | `.github/skills/` | Full project and personal skill support |
| **Cursor** | Supported | Via skills CLI |
| **OpenCode** | Supported | Via skills CLI |
| **Manus** | Supported | Custom AI workflows |
| **Amp, Goose, Letta, Roo Code** | Supported | Various implementations |
| **OpenClaw/Moltbook** | `~/.moltbot/skills/` | Via ClawHub or direct install |

## SKILL.md vs AGENTS.md

| Aspect | SKILL.md | AGENTS.md |
|--------|----------|-----------|
| **Purpose** | Task-specific capabilities | Agent identity and global rules |
| **Loading** | On-demand, contextual | Always loaded |
| **Scope** | Narrow, per-task | Broad, cross-task |
| **Example** | "How to process a refund" | "Our company voice is professional" |

## Security Concerns

- **Supply chain attacks** -- Skills fetch instructions from the internet and can execute code
- **22-26%** of OpenClaw skills contain vulnerabilities (security audit)
- Nearly **400 fake crypto trading skills** installed information-stealing malware
- Moltbook had an unsecured database allowing anyone to commandeer any agent
- **Mitigation:** OpenClaw now has VirusTotal partnership; sandboxed execution recommended

## Key URLs

- [Agent Skills Specification](https://agentskills.io/specification)
- [Cloudflare Discovery RFC](https://github.com/cloudflare/agent-skills-discovery-rfc)
- [Anthropic Skills Repository](https://github.com/anthropics/skills)
- [Agent Skills Directory](https://skills.sh/)
- [Moltbook](https://www.moltbook.com/)
- [Simon Willison on Moltbook](https://simonwillison.net/2026/Jan/30/moltbook/)
- [Simon Willison on Agent Skills](https://simonwillison.net/2025/Dec/19/agent-skills/)
- [Skills.md vs Agents.md comparison](https://www.eesel.ai/blog/skills-md-vs-agents-md)
- [Mintlify skill.md open standard](https://www.mintlify.com/blog/skill-md)
