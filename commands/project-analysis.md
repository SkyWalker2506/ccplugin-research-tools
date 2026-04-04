# /project-analysis

Deep 12-category project analysis with parallel background agents.

> Before starting, suggest the user run `/compact` to free up context for the agents.

## Step 1 -- Model Selection

```
Choose the agent model for analysis:
  1) Opus -- most detailed, highest cost
  2) Sonnet -- balanced
  3) Haiku -- fast, economical
  4) Mixed -- I'll ask per category

Your choice (1/2/3/4):
```

## Step 2 -- Category Selection (ask one by one)

For each category, ask:

```
[CATEGORY_NAME] -- [short description]
1) Yes (full analysis)  2) No (skip)  3) Partial (quick scan)
```

Categories:

1. **UI/UX & Design** -- layout, flows, responsiveness, design system
2. **Performance & Core Web Vitals** -- load times, bundle size, rendering
3. **SEO & Discoverability** -- metadata, sitemap, structured data
4. **Data & Scraping Infrastructure** -- data pipelines, APIs, caching
5. **Monetization & Business Model** -- pricing, conversion, revenue
6. **Growth & User Engagement** -- onboarding, retention, viral loops
7. **Security & Infrastructure** -- auth, secrets, CORS, dependencies
8. **Content & Editorial Strategy** -- content quality, freshness, tone
9. **Analytics & Tracking** -- events, funnels, dashboards
10. **Architecture & Code Quality** -- patterns, coupling, test coverage
11. **Accessibility (a11y)** -- WCAG compliance, screen readers, contrast
12. **Competitive Analysis** -- competitor features, market positioning

After all categories are asked, summarize selections and confirm.

## Step 3 -- Launch Agents (parallel, background)

For each selected category, launch a separate background Agent:

- Auto-detect project root (current working directory)
- Model: user's choice from Step 1
- Max 25 tool calls (15 scanning, 10 research)
- Output: `[PROJECT]/analysis/[NN_category].md`

## Step 4 -- Master Report

When all agents complete, launch an Opus agent to:

- Read all category reports
- Create `[PROJECT]/analysis/MASTER_ANALYSIS.md`
- Include cross-cutting insights
- Top 20 action items ranked by impact/effort
- Cost table (estimated effort per item)

## Step 5 -- Present to User

1. Master report summary
2. File locations
3. Top 5 most critical actions
