# llms.txt Deep Dive

## Origin

**llms.txt** was proposed on September 3, 2024 by **Jeremy Howard**, co-founder of Answer.AI and fast.ai, and lecturer at the Universities of Queensland and Stanford.

Howard observed how `robots.txt` serves as a simple, effective way to instruct web crawlers, and was inspired to create an analogous mechanism for AI systems -- but for **content curation** rather than access control.

- [Original blog post](https://www.answer.ai/posts/2024-09-03-llmstxt.html)
- [Jeremy Howard's announcement on X](https://x.com/jeremyphoward/status/1831089138571133290)

## The Problem It Solves

LLMs face two key challenges with web content:

1. **Context window limitations** -- LLMs cannot ingest entire websites
2. **HTML noise** -- Navigation menus, ads, tracking scripts, and boilerplate waste tokens without adding informational value

## Specification Format

The file is placed at `/llms.txt` in the root of a website. It uses **Markdown** because the files are expected to be read directly by language models.

### Required Structure (in order)

1. **H1 header** -- Project/site name (the only required element)
2. **Blockquote** -- Short summary with key information (optional but recommended)
3. **Zero or more markdown body sections** -- Additional detail (optional)
4. **Zero or more H2-delimited sections** -- Each contains a "file list" of URLs. Each item is a markdown hyperlink `[name](url)`, optionally followed by `: description` (optional)

### Special "Optional" Section

An H2 section titled "Optional" has special semantics: URLs listed there can be skipped if a shorter context is needed.

### Example

```markdown
# Project Name

> Brief description of the project and its purpose.

Additional context or guidance for interpreting the documentation.

## Docs

- [Getting Started](https://example.com/docs/getting-started.md): Introduction and setup guide
- [API Reference](https://example.com/docs/api.md): Complete API documentation
- [Configuration](https://example.com/docs/config.md): Configuration options

## Optional

- [Changelog](https://example.com/docs/changelog.md): Version history
- [Contributing](https://example.com/docs/contributing.md): How to contribute
```

### Companion Proposal: `.md` URL Extensions

Howard also proposes that websites provide clean Markdown versions of their pages by appending `.md` to the URL. For example, `https://example.com/docs/api` would have a Markdown version at `https://example.com/docs/api.md`.

## File Variants

| File | Purpose |
|------|---------|
| `/llms.txt` | Lightweight navigation/index file |
| `/llms-full.txt` | Full text of all documentation in one place. Developed by Mintlify in collaboration with Anthropic. |
| `/llms-ctx.txt` | Expanded version where linked URLs are fetched and inlined (excluding Optional section) |
| `/llms-ctx-full.txt` | Same as llms-ctx.txt but includes Optional section URLs |
| Per-page `.md` files | Individual Markdown versions of each page |

Traffic data from Mintlify shows that **AI agents visit `llms-full.txt` over 2x as frequently** as `llms.txt`.

## Adoption

### Key Adopters

Anthropic, Stripe, Cloudflare, Vercel, Cursor, Hugging Face, Perplexity, Zapier, ElevenLabs, Raycast, Solana, Astro, LangChain/LangGraph, FastHTML/fast.ai/nbdev, Yoast.

### Adoption Numbers

- ~600-950 domains had published llms.txt files per NerdyData tracking
- Up to 844,000 websites per BuiltWith (likely inflated by Mintlify's mass rollout)
- Major inflection point: November 2024 when Mintlify rolled out support across all hosted docs sites

### Who Does NOT Support It

- **No major LLM provider** has officially committed to reading llms.txt files
- **Google** has explicitly rejected it (John Mueller compared it to the `<meta keywords>` tag)
- **OpenAI** honors robots.txt but has not confirmed llms.txt usage
- **Anthropic** publishes its own llms.txt but hasn't stated its crawlers use the standard

## Criticism

### Arguments Against

1. **No official consumer** -- no major LLM provider has committed to using these files
2. **No discovery mechanism** -- unlike robots.txt, there's no established mechanism for LLMs to discover llms.txt files
3. **Solving a temporary problem** -- HTML parsing and context windows are rapidly improving
4. **Misinformation loops** -- SEO tools flag missing llms.txt as "issues," creating pressure without evidence of value
5. **Redundancy** -- if a crawler already has the original content with structured data, a Markdown file is redundant

### Arguments For

1. **Low cost, low risk** -- trivial to implement
2. **Developer tooling benefit** -- tools like Cursor and Windsurf report measurable time/token savings
3. **Future-proofing** -- if any major provider announces support, early adopters benefit
4. **Google does index them** -- despite stated non-support, Google had indexed 30,000-60,000 llms.txt files by October 2025

## Relationship to robots.txt

| | robots.txt | llms.txt |
|---|---|---|
| Purpose | Access control (block/allow) | Content curation (guide to best content) |
| Format | Directive-based | Markdown with structured sections |
| Established | 1994, universally respected | 2024, proposed standard |
| Content | Rules only | Summary + links to key resources |
| Audience | Search engine crawlers | AI language models and agents |

## Tools, Generators, Validators, and Related Projects

### Official Tooling

- **`llms_txt2ctx`** -- CLI and Python module for parsing llms.txt files
- **`llms_txt` Python package** -- Helpers for creating and parsing files
- **GitHub**: [AnswerDotAI/llms-txt](https://github.com/AnswerDotAI/llms-txt)

### Generators

- [llms-txt.io](https://llms-txt.io/) -- Free generator
- [Rankability](https://www.rankability.com/tools/llms-txt-generator/) -- Generator and validator
- [Writesonic](https://writesonic.com/free-tools/llms-txt-generator) -- Free generator
- [AIOSEO](https://aioseo.com/) -- WordPress plugin with llms.txt generation
- [WordLift](https://wordlift.io/) -- Generator with smart URL selection
- [Yoast SEO](https://developer.yoast.com/features/llms-txt/functional-specification/) -- WordPress plugin support
- **Mintlify** -- Auto-generates both `/llms.txt` and `/llms-full.txt`

### Validators

- [llmstxtvalidator.dev](https://llmstxtvalidator.dev/) -- Syntax, structure, spec compliance
- [llmstxtchecker.net](https://llmstxtchecker.net/) -- Markdown formatting, required elements, link integrity
- [RankRay Checker](https://rankray.com/free-seo-tools/llms-txt-checker/) -- Validates all critical components

### Framework Plugins

- `vitepress-plugin-llms` -- Auto-generates for VitePress
- `docusaurus-plugin-llms` -- Auto-generates for Docusaurus
- Drupal LLM Support -- Drupal Recipe for Drupal 10.3+
- `llms-txt-php` -- PHP library
- VS Code PagePilot Extension -- Loads llms.txt context into VS Code chat

### Directories

- [directory.llmstxt.cloud](https://directory.llmstxt.cloud/) -- Community-maintained directory
- [llmstxt.site](https://llmstxt.site/) -- Explorer/finder with stats
- [llms-txt-hub](https://github.com/thedaviddias/llms-txt-hub) -- Largest curated directory (by David Dias)
- [BuiltWith](https://blog.builtwith.com/2025/06/23/discover-websites-using-llms.txt) -- Now tracks adoption

## Key URLs

| Resource | URL |
|----------|-----|
| Official Spec | https://llmstxt.org/ |
| Original Blog Post | https://www.answer.ai/posts/2024-09-03-llmstxt.html |
| GitHub Repository | https://github.com/AnswerDotAI/llms-txt |
| Community Directory | https://directory.llmstxt.cloud/ |
| Hub / Largest Directory | https://github.com/thedaviddias/llms-txt-hub |

## Sources

- [Official llms.txt Specification](https://llmstxt.org/)
- [Jeremy Howard's Original Proposal](https://www.answer.ai/posts/2024-09-03-llmstxt.html)
- [LLMs.txt Explained - Towards Data Science](https://towardsdatascience.com/llms-txt-414d5121bcb3/)
- [What is llms.txt? Breaking down the skepticism - Mintlify](https://www.mintlify.com/blog/what-is-llms-txt)
- [The Case Against llms.txt - Daydream](https://www.withdaydream.com/library/llms-txt-hype-vs-reality)
- [What Is LLMs.txt & Should You Use It? - Semrush](https://www.semrush.com/blog/llms-txt/)
- [What Is llms.txt? - Ahrefs](https://ahrefs.com/blog/what-is-llms-txt/)
- [LLMs.txt: Why Brands Rely On It and Why It Doesn't Work - SE Ranking](https://seranking.com/blog/llms-txt/)
- [Google Says LLMs.txt Comparable To Keywords Meta Tag - SEJ](https://www.searchenginejournal.com/google-says-llms-txt-comparable-to-keywords-meta-tag/544804/)
