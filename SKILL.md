---
name: html2md
description: Convert HTML pages to clean, agent-friendly markdown using Readability + Turndown. Use when an agent needs to read web pages with minimal token waste — strips navigation, ads, footers, cookie banners, social CTAs. Supports URL fetch, local files, stdin, token budgeting, and output control flags. Ideal for research tasks, content extraction, and web scraping in agent workflows.
---

# html2md

Aggressive HTML-to-markdown converter for AI agents. Two-pass extraction: Mozilla Readability isolates main content, Turndown converts to markdown, then heavy post-processing strips remaining noise.

## Setup

```bash
cd <skill-dir>/scripts
npm install
npm link  # makes `html2md` globally available
```

Requires Node.js 22+.

## Usage

```bash
html2md <url>                     # fetch + convert
html2md --file <path>             # local HTML file
cat page.html | html2md --stdin   # pipe from stdin
html2md --max-tokens 2000 <url>   # budget-aware truncation
html2md --no-tables <url>         # tables → bullet lists
html2md --no-links <url>          # strip hrefs, keep text
html2md --no-images <url>         # remove image references
html2md --json <url>              # JSON output: {title, url, markdown, tokens}
```

## Key Features

- **Readability extraction** — kills navbars, sidebars, ads, cookie banners. Falls back to cleaned `<body>` when Readability returns too little (e.g. HN's table layout).
- **Token budgeting** — `--max-tokens N` keeps all headings, fills remaining budget in document order, appends `[truncated — N more tokens]`. Uses 1 token ≈ 4 chars heuristic.
- **Post-processing** — strips HTML comments, zero-width chars, social CTAs, breadcrumbs, empty headings, collapses excess blank lines.
- **Error handling** — bad URLs, timeouts (15s), non-HTML content, missing files all exit code 1 with descriptive stderr.

## When to Use Instead of web_fetch

Use `html2md` when:
- Reading web pages in cron jobs or sub-agents (cleaner output, fewer tokens)
- Token budget matters (use `--max-tokens`)
- Page has heavy navigation/ads that web_fetch doesn't strip well
- You need JSON output for programmatic use

## Examples

Read a Paul Graham essay within 2000 tokens:
```bash
html2md --max-tokens 2000 https://paulgraham.com/greatwork.html
```

Read HN front page as clean text (no links):
```bash
html2md --no-links https://news.ycombinator.com
```

Get structured output:
```bash
html2md --json https://example.com | jq .tokens
```
