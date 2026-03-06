# AI 每日新闻速报

聚合国内外 AI 最新资讯，自动生成精美的自包含 HTML 新闻简报。

## 功能特点

- **中英双语覆盖** — 同时收录国内和国际 AI 新闻
- **3 大分类** — 重大新闻 / 工具产品 / 行业动态
- **地区切换** — 国外（默认显示）/ 国内 一键切换
- **重点关注** — 优先收录 Codex、Claude Code、Gemini 相关内容
- **严格日期过滤** — 只收录当天新闻（不足时扩展到昨天并标注 [昨日]）
- **自包含 HTML** — 无外部依赖，内联 CSS + JS，打开即用
- **精确链接** — 每条新闻都链接到具体文章页面，绝不链接到首页

## 安装

已验证支持 Claude Code 和 Codex。理论上兼容所有支持 `npx skills` 的 AI 编码助手。

```bash
npx skills add yinan-yinan/ai-daily-news-cn
```

## 使用方式

安装后，对 AI 助手说以下任意触发语：

- "今天的AI资讯" / "每日AI新闻" / "AI日报" / "AI有什么新动态"
- "AI news" / "AI daily" / "what's new in AI"

Skill 会自动搜索今日 AI 新闻、分类整理，并生成 HTML 文件保存到 `./ai_news/YYYY-MM-DD-ai-daily.html`。

## 输出效果

生成一个自包含的 HTML 文件，包含：

- 今日要点（头部展示 3 条关键新闻）
- 分类 Tab 导航（重大新闻 / 工具产品 / 行业动态）
- 国外 / 国内地区切换
- 卡片式新闻条目（标题 + 摘要 + 来源链接 + 日期）

## 工作流程

```
第 1 阶段：信息收集
  ├─ 中英文关键词搜索（带日期过滤）
  └─ 抓取主要 AI 新闻站点内容
      ↓
第 2 阶段：内容过滤
  ├─ 严格日期验证（必须是今天发布的文章）
  ├─ 去重（同一新闻保留最详细版本）
  └─ 分类：国内 / 国外
      ↓
第 3 阶段：分类整理
  └─ 按 3 大类 × 2 地区 组织内容
      ↓
第 4 阶段：生成 HTML
  └─ 填充模板，保存为 ./ai_news/YYYY-MM-DD-ai-daily.html
```

## 新闻来源

### 国际来源
| 来源 | 侧重 |
|------|------|
| OpenAI Blog | Codex、GPT 官方公告 |
| Anthropic News | Claude Code、AI 安全 |
| Google AI Blog | Gemini、研究成果 |
| TechCrunch AI | 创业、融资、产品 |
| VentureBeat AI | 行业深度分析 |
| The Verge AI | 消费级 AI、产品评测 |

### 国内来源
| 来源 | 侧重 |
|------|------|
| 机器之心 | 技术深度、研究解读 |
| 量子位 | 行业快讯、模型发布 |
| 36氪 AI | 创业、融资、商业 |
| InfoQ 中文 | 开发者技术文章 |
| CSDN AI | 开发者社区资讯 |
| 新智元 | 行业趋势分析 |
| AI 科技评论（雷锋网） | 产品分析、研究解读 |

## 文件结构

```
ai-daily-news-cn/
├── SKILL.md                  # 核心技能定义
├── README.md                 # 本文件
├── LICENSE                   # MIT 许可证
└── references/
    ├── news-sources.md       # 新闻源数据库（中英文）
    ├── search-queries.md     # 搜索查询模板
    └── output-template.html  # HTML 输出模板
```

## 兼容性

本 Skill 采用 **agent-agnostic** 设计，不使用任何特定 agent 的工具名（如 `mcp__*`），所有操作均使用通用描述（如"搜索网页"、"抓取 URL 内容"），因此任何 AI 编码助手都能执行。

| AI 助手 | 状态 |
|---------|------|
| Claude Code | ✅ 已验证 |
| Codex | ✅ 已验证 |
| 其他（Gemini CLI、Cursor 等） | 🔲 理论兼容，未测试 |

## 许可证

MIT
