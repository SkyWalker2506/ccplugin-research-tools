---
name: research-tools
description: "Auto-trigger for research, analysis, and PRD workflows. Routes to the correct command based on user intent."
user-invocable: false
---

# Research Tools -- Auto-Trigger Skill

This skill detects research, analysis, and PRD-related intent and routes to the appropriate command.

## Trigger Patterns

| Pattern | Routes to |
|---------|-----------|
| "research competitors", "market research", "analyze market", "web research", "find competitors" | `/web-research` |
| "analyze project", "project analysis", "deep analysis", "audit project", "code analysis" | `/project-analysis` |
| "create prd", "write prd", "plan feature", "requirements for", "spec out", "product requirements" | `/prd` |
| "convert prd", "ralph json", "create prd.json", "start ralph", "autonomous execution" | `/ralph` |

## Routing Rules

1. Match user message against trigger patterns above
2. If a clear match is found, invoke the corresponding command
3. If ambiguous, ask the user which tool they want:

```
I detected a research/analysis request. Which tool should I use?
  1) /web-research -- market research, competitors, trends
  2) /project-analysis -- deep 12-category project audit
  3) /prd -- generate a Product Requirements Document
  4) /ralph -- convert PRD to autonomous execution format
```

4. If the user explicitly names a command (e.g., "/prd"), go directly to it without asking

## Dependencies

- **fetch** MCP server: required for web-research (WebSearch, WebFetch)
- Project CLAUDE.md or README: used to understand project context
