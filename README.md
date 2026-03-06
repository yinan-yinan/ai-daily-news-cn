# AI Daily News (Chinese)

Aggregates daily AI news from Chinese and international sources, generates a self-contained HTML briefing file with modern card UI.

## Features

- **Bilingual coverage** — Chinese domestic + international AI news
- **3 categories** — Major News / Tools & Products / Industry
- **Region toggle** — International (default) / Domestic view
- **Focus topics** — Codex, Claude Code, Gemini prioritized
- **Strict date filtering** — Only today's news (yesterday as fallback)
- **Self-contained HTML** — No external dependencies, inline CSS + JS
- **Specific article links** — Every link points to the actual article page, never a homepage

## Install

Works with Claude Code, Codex, Gemini CLI, Cursor, and 37+ agents.

```bash
npx skills add your-username/ai-daily-news-cn
```

## Usage

After installation, trigger the skill by saying:

- "AI news" / "AI daily" / "what's new in AI"
- "今天的AI资讯" / "每日AI新闻" / "AI日报" / "AI有什么新动态"

The skill will search for today's AI news, categorize it, and generate an HTML file at `./ai_news/YYYY-MM-DD-ai-daily.html`.

## Output

A single self-contained HTML file with:

- Key Takeaways header (top 3 stories)
- Tab-based category navigation
- International / Domestic region toggle
- Card-based news items with source links

## File Structure

```
ai-daily-news-cn/
├── SKILL.md                  # Core skill definition
├── README.md                 # This file
└── references/
    ├── news-sources.md       # News source database (CN + EN)
    ├── search-queries.md     # Search query templates
    └── output-template.html  # HTML output template
```

## Compatibility

This skill is **agent-agnostic** — no agent-specific tool names (e.g., no `mcp__*` references). It uses generic action descriptions like "search the web" and "fetch URL content", so any AI coding agent can execute it.

| Agent | Supported |
|-------|-----------|
| Claude Code | Yes |
| Codex | Yes |
| Gemini CLI | Yes |
| Cursor | Yes |
| Others (37+) | Yes |

## License

MIT
