# File Type Accessibility for AI Agents

How file formats and data structures affect LLM agent performance, token efficiency, and accuracy.

## The Problem

AI agents consume context from files — configuration, schemas, documentation, code. But not all formats are equally accessible. Format choice affects:

- **Accuracy** — Can the model correctly interpret the data?
- **Token efficiency** — How many tokens does the format consume?
- **Runtime cost** — Does the format cause expensive search/retry loops?
- **Scalability** — Does the format hold up at thousands of files or tables?

Practitioners have lacked empirical guidance on which formats to use when structuring context for agents. Recent research (2025–2026) is beginning to fill that gap.

## Key Research

### McMillan 2026: Structured Context Engineering at Scale

The most comprehensive study to date. Damon McMillan ran 9,649 experiments across 11 models, 4 formats (YAML, Markdown, JSON, TOON), and SQL schemas ranging from 10 to 10,000 tables.

- **Paper:** [arXiv:2602.05447](https://arxiv.org/abs/2602.05447)
- **Commentary:** [Simon Willison's analysis](https://simonwillison.net/2026/Feb/9/structured-context-engineering-for-file-native-agentic-systems/)

#### Core findings

| Finding | Detail |
|---------|--------|
| Format ≠ accuracy | Format does not significantly affect aggregate accuracy (χ²=2.45, p=0.484) |
| Model capability dominates | 21 percentage-point accuracy gap between frontier and open-source tiers |
| File-based retrieval helps frontier models | +2.7% accuracy for Claude, GPT, Gemini (p=0.029) |
| File-based retrieval hurts some open-source models | Aggregate −7.7% (p<0.001), varies by model |
| Scalability works | File-native agents scale to 10,000 tables via domain-partitioned schemas |

#### Format accuracy (aggregate)

| Format | Accuracy |
|--------|----------|
| YAML | 75.4% |
| Markdown | 74.9% |
| JSON | 72.3% |
| TOON | 72.3% |

YAML was the best format for 5 of 11 models, Markdown for 4, JSON for 2, TOON for none.

#### The "Grep Tax"

The study's most surprising finding. TOON (Token-Oriented Object Notation) is ~25% smaller in file size than YAML, designed to minimize token usage. But models unfamiliar with TOON's syntax couldn't construct effective search patterns, causing dramatically more tokens to be consumed across iterative refinement:

- **500 tables:** TOON consumed 138% more tokens than YAML
- **10,000 tables:** TOON consumed 740% more tokens than YAML

The root cause: models trained predominantly on YAML/JSON/Markdown can `grep` those formats efficiently. Unfamiliar formats break search heuristics, causing costly retry loops. **File size does not predict runtime efficiency.**

#### Frontier vs. open-source gap

The study tested frontier models (Opus 4.5, GPT-5.2, Gemini 2.5 Pro) against leading open-source models (DeepSeek V3.2, Kimi K2, Llama 4). The frontier tier consistently outperformed open-source by ~21 percentage points regardless of format. File-native agentic loops remain better optimized for closed-weight models.

### Prompt Format Impact (Tam et al. 2024)

[Does Prompt Formatting Have Any Impact on LLM Performance?](https://arxiv.org/abs/2411.10541) tested plain text, Markdown, JSON, and YAML across GPT models.

- GPT-3.5-turbo performance varied up to **40%** depending on format choice
- GPT-4 showed much greater robustness across formats (consistency >0.5)
- No universal optimal format — GPT-3.5 favored JSON; GPT-4 favored Markdown
- Larger models are less sensitive to format choice

**Implication:** Format choice matters more for smaller/weaker models. As models improve, format sensitivity decreases — but it doesn't disappear.

### Nested Data Format Comparison (Improving Agents, 2026)

[Which Nested Data Format Do LLMs Understand Best?](https://www.improvingagents.com/blog/best-nested-data-format/) tested JSON, YAML, XML, and Markdown across GPT-5 Nano, Llama 3.2 3B, and Gemini 2.5 Flash Lite.

| Format | GPT-5 Nano | Llama 3.2 3B | Gemini 2.5 Flash Lite |
|--------|-----------|-------------|----------------------|
| YAML | 62.1% | 49.1% | 51.9% |
| Markdown | 54.3% | 48.0% | 48.2% |
| JSON | 50.3% | 52.7% | 43.1% |
| XML | 44.4% | 50.7% | 33.8% |

- YAML was the best format for 2 of 3 models
- XML was consistently the worst (and the most token-expensive)
- Llama 3.2 showed minimal format sensitivity

### Token Efficiency

Multiple studies converge on token efficiency rankings:

| Format | Relative to JSON |
|--------|-----------------|
| Markdown | ~15% fewer tokens |
| YAML | ~11% fewer tokens |
| JSON | Baseline |
| XML | ~80% more tokens |

Source: [OpenAI community analysis](https://community.openai.com/t/markdown-is-15-more-token-efficient-than-json/841742), confirmed by the Improving Agents study (Markdown uses 34–38% fewer tokens than JSON across models).

Markdown's efficiency comes from alignment with training data — most LLM training corpora contain natural language with Markdown formatting, so models have deep statistical associations between Markdown structure and semantic meaning.

## Practical Recommendations

### Format selection guide

| Priority | Recommended format | Rationale |
|----------|-------------------|-----------|
| Accuracy-first | YAML | Highest accuracy across most models |
| Cost-first | Markdown | Best token efficiency, good accuracy |
| Interoperability | JSON | Universal parsing support, well-understood |
| Avoid | XML | Worst accuracy, worst token efficiency |
| Avoid at scale | Novel/unfamiliar formats | The grep tax makes them expensive |

### Key principles for agent-accessible files

1. **Use formats models were trained on.** YAML, Markdown, and JSON are all well-represented in training data. Novel formats incur the grep tax.

2. **File size ≠ cost.** A compact but unfamiliar format can cost 7x more tokens than a verbose familiar one due to failed search patterns and retries.

3. **Match format to model tier.** Frontier models are robust to format choice. If targeting smaller/open-source models, format selection and testing become more important.

4. **Partition large contexts.** At scale (thousands of files/tables), domain-partitioned schemas with file-based retrieval outperform monolithic contexts for frontier models.

5. **Prefer Markdown for documentation.** This is why llms.txt uses Markdown — it aligns with training data, is token-efficient, and models parse it reliably.

6. **Prefer YAML for structured configuration.** When accuracy on structured data matters (schemas, configs, specs), YAML edges out other formats.

7. **Test with your target model.** Format preferences are model-specific. What works for GPT may not work for Llama. Benchmark before committing.

## Relationship to AX

File type accessibility is a core component of the **Context** pillar from Biilmann's Four Pillars of AX. Providing agents with the right information means providing it in formats they can efficiently consume. This research supports several AX best practices:

- **llms.txt uses Markdown** — validated by the token efficiency and accuracy data
- **AGENTS.md uses Markdown** — same rationale; familiar format, low token cost
- **SKILL.md uses YAML frontmatter + Markdown body** — combines the accuracy advantage of YAML for structured metadata with the efficiency of Markdown for prose
- **MCP uses JSON** — standard interchange format with universal parsing support
- **OpenAPI specs use YAML or JSON** — both well-supported by agents

The grep tax finding has direct implications for anyone designing new agent-facing formats: novelty is a liability. Familiarity with training data distributions is a feature.

## Sources

- [Structured Context Engineering for File-Native Agentic Systems](https://arxiv.org/abs/2602.05447) - McMillan, Feb 2026.
- [Simon Willison's analysis](https://simonwillison.net/2026/Feb/9/structured-context-engineering-for-file-native-agentic-systems/) - Commentary on McMillan 2026.
- [Does Prompt Formatting Have Any Impact on LLM Performance?](https://arxiv.org/abs/2411.10541) - Tam et al., Nov 2024.
- [Which Nested Data Format Do LLMs Understand Best?](https://www.improvingagents.com/blog/best-nested-data-format/) - Improving Agents, 2026.
- [Markdown is 15% more token efficient than JSON](https://community.openai.com/t/markdown-is-15-more-token-efficient-than-json/841742) - OpenAI Developer Community.
- [Boosting AI Performance: The Power of LLM-Friendly Content in Markdown](https://developer.webex.com/blog/boosting-ai-performance-the-power-of-llm-friendly-content-in-markdown) - Webex Developers.
