---
name: ai-daily-news-cn
description: "Aggregates and summarizes the latest AI news from Chinese and international sources. Generates a self-contained HTML file with modern card UI. Activates when user asks for 'AI news', 'AI daily', 'today's AI updates', '今天的AI资讯', 'AI有什么新动态', '每日AI新闻', or 'AI日报'."
---

# AI Daily News Briefing (Chinese)

> Aggregates AI news from domestic and international sources, generates a beautiful HTML briefing file.

## When to Use This Skill

Activate this skill when the user:
- Asks for today's AI news or latest AI developments
- Requests a daily AI briefing or updates
- Mentions wanting to know what's happening in AI
- Says: "今天的AI资讯", "AI有什么新动态", "每日AI新闻", "AI日报"
- Says: "AI news", "AI daily", "what's new in AI"

## Focus Topics

Prioritize content related to these AI tools and platforms:
- **Codex** (OpenAI's coding agent)
- **Claude Code** (Anthropic's coding agent)
- **Gemini** (Google's AI model and CLI)

These are the primary tools of interest. Other AI news is still included but given lower priority.

## Workflow Overview

```
Phase 1: Information Gathering
  ├─ Web search with date filters (Chinese + English queries)
  └─ Fetch content from major AI news sites
      ↓
Phase 2: Content Filtering
  ├─ Keep: Last 24-48 hours, significant announcements
  ├─ Remove: Duplicates, minor updates, old content
  └─ Split: Domestic (CN) vs International
      ↓
Phase 3: Categorization
  └─ Organize into 3 categories x 2 regions
      ↓
Phase 4: HTML Generation
  └─ Generate self-contained HTML file with card UI
```

## Phase 1: Information Gathering

### Step 1.1: Web Search (Priority Queries)

Search the web with these queries (use current date for filtering):

**Focus queries (run these first):**
1. `"Codex" OR "Claude Code" OR "Gemini CLI" AI update` (last 24 hours)
2. `"OpenAI Codex" OR "Anthropic Claude Code" OR "Google Gemini" news` (last 24 hours)

**International general queries:**
3. `AI news today artificial intelligence breakthrough` (last 24 hours)
4. `AI product launch tool release` (last 24 hours)
5. `AI startup funding industry news` (last 48 hours)

**Chinese queries:**
6. `AI 人工智能 最新消息 今天` (last 24 hours)
7. `大模型 发布 开源 最新` (last 24 hours)
8. `AI工具 产品发布 智能体 Agent` (last 24 hours)

### Step 1.2: Fetch Full Articles

For the top 15-20 most relevant results from search:
- Fetch the full article content from each URL
- Extract: title, summary, publication date, source name, **specific article URL**
- Discard results where the URL is a homepage or category page (not a specific article)

### Step 1.3: Fetch from Key Sources

Additionally, fetch content from these primary sources to ensure coverage:

**International:**
- OpenAI Blog: https://openai.com/blog
- Anthropic News: https://www.anthropic.com/news
- Google AI Blog: https://blog.google/technology/ai/

**Domestic:**
- 机器之心: https://www.jiqizhixin.com/
- 量子位: https://www.qbitai.com/

Scan the front page for articles from the last 24-48 hours. Extract specific article URLs.

> See `references/news-sources.md` for the full source database.
> See `references/search-queries.md` for additional query templates.

## Phase 2: Content Filtering

### Date Filter (CRITICAL)

**Strict date rule:** Only include news published **today** (the current date).
- Check the article's publication date — it MUST match today's date
- If the article has no clear publication date, check if the content references today's events
- Do NOT include articles from yesterday or earlier, even if they appear in today's search results
- Search engines often return older results — you MUST verify each article's actual publication date

**Exception:** If today's news yields fewer than 3 items in a category, extend to **yesterday only** (not further). Mark these items with "[昨日]" prefix in the summary.

### Content Filter

**Keep:**
- Major announcements (product launches, model releases, research breakthroughs)
- Codex / Claude Code / Gemini updates (always keep, even if minor)
- Industry developments (funding, partnerships, regulations)

**Remove:**
- Duplicate stories (same news across sources → keep most comprehensive)
- Minor updates or marketing content
- Articles NOT published today (see Date Filter above)
- Non-AI content

### Deduplication

When the same story appears in multiple sources:
- Keep the version with the most detail
- Note the source with the specific article URL
- Prefer authoritative sources (company blogs > aggregators)

### Region Classification

Classify each item as:
- **Domestic (国内)**: News about Chinese companies (Baidu, Alibaba, Tencent, ByteDance, Moonshot, Zhipu, etc.), Chinese government AI policy, Chinese AI research labs
- **International (国外)**: Everything else

## Phase 3: Categorization

Organize into 3 categories:

### 🔥 重大新闻 (Major News)
- Product launches (new AI models, services, features)
- Model releases (GPT updates, Claude features, Gemini capabilities)
- Major company announcements
- Research breakthroughs

### 🛠️ 工具产品 (Tools & Products)
- New AI tools and frameworks
- Developer tools and IDE integrations
- Open source releases
- Platform updates

### 💰 行业动态 (Industry)
- Funding rounds and investments
- Mergers and acquisitions
- AI regulations and policies
- Market trends

**Target:** At least 3 items per category per region (18 total minimum).
If a region has no news for a category, note "暂无重大更新" (No significant updates).

## Phase 4: HTML Generation

### Step 4.1: Prepare Key Takeaways

Summarize the 3 most important stories of the day as one-line takeaways.
Format: **Bold title** — brief explanation

### Step 4.2: Generate HTML

Use the HTML template from `references/output-template.html` as the base structure.

Fill in:
1. **Header**: Key Takeaways (3 items), date, stats (total items, source count), focus topics
2. **Category tabs**: 3 tabs with news cards for each category
3. **Region sections**: International (default active) and Domestic for each category
4. **News cards**: Each card contains:
   - **Title** (bold, linked to specific article URL, opens in new tab)
   - **Summary** (one sentence in Chinese)
   - **Source** (linked to specific article URL) + date

### Step 4.3: Save File

1. Create directory `./ai_news/` in the current working directory if it doesn't exist
2. Save the HTML file as `./ai_news/YYYY-MM-DD-ai-daily.html`
3. Inform the user of the file path

## Quality Standards

### CRITICAL: Link Requirements
- Every news title MUST link to the **specific article page**
- Example GOOD: `https://techcrunch.com/2026/03/06/openai-codex-update/`
- Example BAD: `https://techcrunch.com/` or `https://techcrunch.com/category/ai/`
- If you cannot find a specific article URL, mark as `#` and add note "[Link unavailable]"
- Source name in card-meta must also link to the same specific article URL

### Content Quality
- All user-facing text must be in **Chinese**
- Summaries must accurately reflect the original article (no hallucination)
- Minimum 3 different sources across the briefing
- Every item has source name + date + specific URL

### Validation Checklist
- [ ] All links point to specific article pages (not homepages)
- [ ] No duplicate stories across categories
- [ ] All items from last 24-48 hours
- [ ] HTML renders correctly (self-contained, no external deps)
- [ ] File saved to `./ai_news/YYYY-MM-DD-ai-daily.html`
- [ ] Key Takeaways present at top
- [ ] Default view shows international news

## Error Handling

| Error | Fallback |
|-------|----------|
| Website fetch fails | Skip source, continue with others. Minimum 2 sources must succeed. |
| Search returns no results | Broaden date range to 72 hours, simplify query |
| All sources fail | Inform user: "无法获取新闻源，请检查网络后重试" |
| Cannot get specific article URL | Use `#` as href, add "[Link unavailable]" note |
| Category is empty | Show "暂无重大更新" |
| File write fails | Fall back to terminal output |

## Customization

After generating the briefing, offer the user options:
- "需要聚焦某个特定话题吗？" (Focus on specific topic?)
- "需要调整时间范围吗？" (Adjust time range?)
- "需要更详细的分析吗？" (Want deeper analysis?)
