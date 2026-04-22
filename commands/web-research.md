# /web-research

Web research agent -- competitors, user reviews, market trends, UX patterns, monetization strategies.

## Usage

| Command | Behavior |
|---------|----------|
| `/web-research` | General market research for the current project |
| `/web-research competitors` | Competitor analysis |
| `/web-research ux` | UX patterns, onboarding, gamification |
| `/web-research trends` | Market trends and growth |
| `/web-research monetization` | Monetization strategies |
| `/web-research reviews` | User reviews (App Store, Reddit, forums) |
| `/web-research ai` | AI/LLM integration landscape |
| `/web-research growth` | ASO, viral loops, retention |
| `/web-research pedagogy` | Learning science, SRS |
| `/web-research accessibility` | WCAG, a11y patterns |
| `/web-research localization` | Multi-language, RTL support |
| Any topic | Focused research on that topic |

## Execution

**Model:** Opus -- background agent, single deep-dive pass.

Launch a background agent with this prompt:

```
You are a market research expert. Research the ecosystem around the current project.

Read the project's CLAUDE.md (or README) to understand the project name, domain, and existing features.

FOCUS: [user-provided focus, or "General market research" if none]

## STEPS

### 1. COMPETITOR ANALYSIS (WebSearch + WebFetch)
Find the top competitors in the project's domain.

For each:
- Key features and differentiators
- User count / rating
- Monetization model
- Features they have that the project lacks

### 2. USER REVIEWS (WebSearch)
Search terms:
- "[project domain] app review 2025/2026"
- "best [project domain] app reddit"
- "[competitor1] vs [competitor2] vs [competitor3]"
- "[project domain] app complaints"
- "[project domain] app feature request"

Collect:
- Most frequent complaints
- Most requested features
- What makes users happy
- Retention / churn reasons

### 3. MARKET TRENDS (WebSearch)
- Market size and growth
- Mobile / web app trends
- AI integration trends
- Gamification trends
- Subscription vs one-time purchase trends

### 4. UX BEST PRACTICES (WebSearch)
- Onboarding best practices
- Gamification patterns that work
- Retention strategies
- Feedback collection UX
- Tutorial / coach marks patterns

### 5. OPPORTUNITIES FOR THE PROJECT
Apply findings to the project:
- Lessons from competitors
- Feature gaps from user needs
- Quick wins (low effort, high impact)
- Strategic investments (high effort, high impact)

### 6. WRITE REPORT

## Competitor Analysis Summary
| App | Rating | Users | Monetization | Missing in Project |
(table)

## User Insights
- Top 5 complaints
- Top 5 requested features
- Retention factors

## Market Trends
- Key trends
- Opportunities for the project

## UX Recommendations
- Onboarding
- Gamification
- Retention

## Task Suggestions
| # | Title | Description | Priority | Effort | Source |
(table -- source: which competitor/trend/user need)

## Priority Order
1. Quick win -- reason
2. Strategic -- reason
...

## RULES
- Use WebSearch and WebFetch for current data
- Provide concrete, actionable recommendations
- Cite the source for each recommendation (competitor, trend, user review)
- Suggest tasks in Jira-ready format (title, description, priority, effort)
- Do NOT write code or edit files
- Max 30 tool calls
```

## Output

When the agent completes, show the report and offer 3 options:

```
What next?
  1) Create Jira tasks (approved items go to WAITING FOR APPROVAL)
  2) Save as notes (append to docs/recommendations.md)
  3) Nothing (report is informational only)
```

## MCP Dependency & Error Handling

This command requires the **fetch** MCP server. If WebSearch or WebFetch calls fail, check:

```
MCP unavailable — /web-research requires the fetch MCP server.

Remediation:
  1. Ensure .mcp.json is present at project root (run: ls .mcp.json)
  2. Restart Claude Code to reload MCP servers
  3. Verify uvx is installed: uvx --version
  4. Manually install: uvx mcp-server-fetch

If MCP is unavailable, fall back to providing general guidance based on training data,
clearly noting that live web data was not fetched.
```
