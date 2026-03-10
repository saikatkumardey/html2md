# html2md

Convert HTML pages to clean, agent-friendly markdown. Strips nav, ads, footers, cookie banners — keeps the content.

Built for AI agents that need to read the web without the noise.

## Install

```bash
# As an OpenClaw skill
smolclaw install html2md

# Or manually
cd scripts && npm install && npm link
```

Requires Node.js 22+.

## Usage

```bash
html2md https://example.com                    # Fetch + convert
html2md --file page.html                       # Local file
cat page.html | html2md --stdin                # Stdin
html2md --max-tokens 2000 https://example.com  # Token budget
html2md --no-links https://example.com         # Strip hrefs
html2md --json https://example.com             # JSON output
```

## How It Works

1. **Readability** (Mozilla) extracts main content, kills boilerplate
2. **Turndown** converts HTML to markdown
3. **Post-processing** strips remaining noise — cookie banners, social buttons, empty sections

## Why Not Just Use web_fetch?

`web_fetch` gives you raw markdown with all the navigation, sidebars, and footer garbage. `html2md` gives you just the article. For agent workflows that need to read 5-10 pages per task, that's the difference between staying in context and blowing it.

## License

MIT
