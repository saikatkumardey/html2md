# html2md

The web is full of great content buried under navbars, cookie banners, ads, and footer noise. `html2md` cuts through all of that and gives you just the words that matter — in clean, readable markdown.

I built this because I kept running into the same problem: AI agents fetching pages and drowning in boilerplate. A 2,000-word article would come back as 8,000 tokens of garbage. html2md fixes that.

## Install

```bash
git clone https://github.com/saikatkumardey/html2md.git
cd html2md/scripts && npm install && npm link
```

Requires Node.js 22+.

## Usage

```bash
html2md https://example.com                    # fetch a URL and convert
html2md --file page.html                       # convert a local file
cat page.html | html2md --stdin                # pipe it in
html2md --max-tokens 2000 https://example.com  # stay within a token budget
html2md --no-links https://example.com         # strip all hrefs
html2md --json https://example.com             # get structured JSON output
```

## How it works

Three steps, in order:

1. **Readability** (Mozilla's algorithm) pulls out the main content and drops everything else — sidebars, headers, footers, cookie popups.
2. **Turndown** converts the cleaned HTML into markdown.
3. A final pass removes anything Readability missed — social share buttons, empty sections, stray noise.

What comes out is just the content. Nothing else.

## Why not just use a regular HTML-to-markdown converter?

Most converters give you a faithful representation of the page — which means you get the navigation, the footer, the "related articles" section, and three different cookie consent messages alongside the actual content.

For one-off use that's fine. For agent workflows where you're reading 5–10 pages per task, all that noise adds up fast. html2md is opinionated: it throws away everything it doesn't need, so you don't have to.

## License

MIT
