# HEARTBEAT.md

## What It Is

HEARTBEAT.md is an **OpenClaw-specific convention** (not a broad industry standard) -- a lightweight Markdown file placed in an agent's workspace directory (`~/.openclaw/workspace/HEARTBEAT.md`) that serves as a **periodic task checklist**.

When the OpenClaw gateway triggers a "heartbeat" (a scheduled, recurring agent turn), the agent reads HEARTBEAT.md and follows its instructions to decide whether anything needs the user's attention.

> "Think of it as your 'heartbeat checklist': small, stable, and safe to include every 30 minutes." -- OpenClaw documentation

## How It Works

1. The OpenClaw gateway runs periodic "heartbeat" turns at a configurable interval (default: 30 minutes)
2. The default prompt instructs the agent: "Read HEARTBEAT.md if it exists. Follow it strictly. Do not infer or repeat old tasks from prior chats. If nothing needs attention, reply HEARTBEAT_OK."
3. If nothing needs attention: agent replies `HEARTBEAT_OK` (silently suppressed)
4. If something does: agent sends a message to the configured target (Telegram, Slack, etc.)
5. **Optimization:** If HEARTBEAT.md contains only blank lines and headers, the heartbeat run is skipped to conserve tokens
6. **If the file is missing:** heartbeat still runs; model decides on its own what to do

## Format

Standard Markdown with a concise checklist:

```markdown
# Heartbeat checklist

- Quick scan: anything urgent in inboxes?
- If it's daytime, do a lightweight check-in if nothing else is pending.
- If a task is blocked, write down _what is missing_ and ask Peter next time.
```

### Time-Based Example

```markdown
# Heartbeat checklist

## Morning
- Check Gmail for urgent messages
- Pull calendar events
- Get local weather

## Throughout Day
- Scan inbox every 30 min
- Surface emails from VIPs only

## Evening
- Summarize unread Slack messages from #engineering channel

## Anytime
- If a flight is less than 12 hours away, check status and send update
```

## Configuration

Key parameters in `.openclaw.config.json`:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `every` | Time between heartbeat runs | `"30m"` |
| `model` | Model override for heartbeat runs | (agent default) |
| `target` | Where to deliver messages | `"last"` |
| `prompt` | Custom prompt override | (built-in) |
| `activeHours.start/end` | Restrict runs to a time window | (none) |
| `ackMaxChars` | Character limit for responses | (none) |

Setting `every: "0m"` disables heartbeats entirely.

## Advanced Pattern: Rotating Checks

Rather than running all checks simultaneously, rotate through checks based on how overdue each one is:

- **Email**: Every 30 minutes (9 AM - 9 PM)
- **Calendar**: Every 2 hours (8 AM - 10 PM)
- **Todoist**: Every 30 minutes
- **Git status**: Once daily
- **Proactive scans**: Once daily at 3 AM

On each heartbeat tick, the system runs whichever check is most overdue.

## Workspace Context

HEARTBEAT.md is one of several markdown files in the OpenClaw workspace:

| File | Purpose |
|------|---------|
| `HEARTBEAT.md` | Periodic task checklist |
| `SOUL.md` | Agent personality/identity |
| `IDENTITY.md` | Agent identity details |
| `USER.md` | User preferences/context |
| `AGENTS.md` | Agent instructions |
| `MEMORY.md` | Long-term memory storage |
| `TOOLS.md` | Available tools configuration |

## Security Warning

> "Don't put secrets (API keys, phone numbers, private tokens) into HEARTBEAT.md -- it becomes part of the prompt context." -- OpenClaw documentation

## Moltbook Usage

Moltbook uses HEARTBEAT.md as part of skill installation. The HEARTBEAT.md instructs bots to check Moltbook every 4+ hours. Simon Willison flagged a critical concern: agents periodically fetch and execute instructions from external URLs, creating a dependency on the remote site's security.

## Cost Considerations

Heartbeats run full agent turns and consume tokens on every wake-up. On Claude Opus 4.5: ~$5-30/day depending on frequency and context size.

Optimization strategies:
- Use cheaper models for heartbeat runs
- Keep HEARTBEAT.md small
- Use the rotating checks pattern
- Set appropriate `activeHours`

## Significance for Agent Experience

While HEARTBEAT.md is project-specific rather than an industry standard, it demonstrates an important **design pattern**: agents maintaining **ambient awareness** through periodic check-ins rather than being purely reactive. This pattern of scheduled autonomous behavior is likely to become more common as agents take on more proactive roles.

## Sources

- [OpenClaw Heartbeat Documentation](https://docs.openclaw.ai/gateway/heartbeat)
- [Simon Willison on Moltbook](https://simonw.substack.com/p/moltbook-is-the-most-interesting)
- [Running OpenClaw Without Burning Money](https://gist.github.com/digitalknk/ec360aab27ca47cb4106a183b2c25a98)
- [Heartbeats in OpenClaw: Cheap Checks First](https://dev.to/damogallagher/heartbeats-in-openclaw-cheap-checks-first-models-only-when-you-need-them-4bfi)
