[中文版](README_CN.md)

# Paper Checking Prompt

A meta prompt for checking academic ML papers using [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (or any LLM coding agent). Built by [Zhuang Liu](https://liuzhuang13.github.io/).

## What This Is

A prompt that instructs an LLM coding agent to systematically check your paper against comprehensive writing and figure standards. The agent will:

1. Download and read the latest [Figure & Table Guide](https://github.com/zlab-princeton-internal/figure-guide) and [Writing Guide](https://github.com/zlab-princeton-internal/wiki)
2. Classify every rule as Python-checkable or LLM-only
3. Write and run a Python script for automated checks
4. Use LLM judgment for visual, semantic, and structural checks (double-checking Python results)
5. Verify all references via web search
6. Generate a bilingual (English + Chinese) report with color-coded severity

Because the agent reads the guides at runtime, the prompt stays valid even as the guides are updated.

## How to Use

### Option A: Copy-paste the prompt

1. Open Claude Code (or your preferred LLM coding agent)
2. Copy the contents of [`PROMPT_EN.md`](PROMPT_EN.md) (English) or [`PROMPT.md`](PROMPT.md) (Chinese) into the conversation
3. Tell it the path to your Overleaf project folder

### Option B: Save as a custom slash command

Save `PROMPT.md` or `PROMPT_EN.md` as a Claude Code custom command (e.g., `~/.claude/commands/check-paper.md`) and invoke it with `/check-paper /path/to/project`.

## Files

| File | Language | Description |
|------|----------|-------------|
| [`PROMPT.md`](PROMPT.md) | Chinese | The complete meta prompt (Chinese) |
| [`PROMPT_EN.md`](PROMPT_EN.md) | English | The complete meta prompt (English) |

## What Gets Checked

The prompt references two external guides that define the full set of rules:

- **[Figure & Table Guide](https://github.com/zlab-princeton-internal/figure-guide)** — vector format, font, colors, borders, arrows, layout, plots, diagrams, captions
- **[Writing Guide](https://github.com/zlab-princeton-internal/wiki)** — structure, language, citations, claims, paragraph length, appendix standards, project hygiene

The agent reads these guides at runtime and creates its own checking plan, so any updates to the guides are automatically reflected.

## Output

- `PAPER_CHECK_REPORT.md` — Full bilingual report (English + Chinese, equally detailed)
- `PAPER_CHECK_REPORT.pdf` — Wide-page PDF version

Every issue includes a **searchable string** quoted from the paper, so you can Ctrl+F to find it immediately.

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) or any LLM coding agent that can read files and run Python
- Python 3.9+
- A LaTeX project with `.tex` and `.bib` files
- Internet access (for reference verification)
- pandoc + xelatex (optional, for PDF report generation)

## License

MIT
