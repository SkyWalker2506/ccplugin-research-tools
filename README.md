# research-tools — Claude Code Plugin

by [Musab Kara](https://linkedin.com/in/musab-kara-85580612a) · [GitHub](https://github.com/SkyWalker2506)

Claude Code plugin that bundles research and analysis functionality into four commands.

## Install

```bash
claude plugin install research-tools@musabkara-claude-marketplace
```

## Commands

| Command | Description |
|---------|-------------|
| `/web-research [focus]` | Market research -- competitors, user reviews, trends, UX patterns, monetization |
| `/web-research --quick [focus]` | Rapid 5-minute scan — top competitors + key insights only |
| `/project-analysis` | Deep 12-category project audit with parallel background agents |
| `/project-analysis --all` | Non-interactive mode — runs all 12 categories automatically |
| `/project-analysis --quick` | Quick scan — Security, Architecture, Performance only |
| `/prd` | Generate a Product Requirements Document for a new feature |
| `/ralph` | Convert PRD markdown to `prd.json` for autonomous execution |

## Workflow

The four commands are designed to work together in a sequential pipeline:

```
Step 1: /web-research          → market context, competitor gaps, user needs
         ↓
Step 2: /project-analysis --all → 12-category technical + product audit
         ↓
Step 3: /prd [feature]         → structured PRD from findings
         ↓
Step 4: /ralph                 → prd.json for autonomous implementation
```

### Example

```bash
# 1. Research the market
/web-research competitors

# 2. Audit your project
/project-analysis --all

# 3. Plan a feature based on findings
/prd "User onboarding redesign"

# 4. Convert for autonomous execution
/ralph
```

## MCP Dependency

This plugin requires the **fetch** MCP server for web research capabilities. The `.mcp.json` file configures it automatically when you install the plugin.

## Auto-Trigger

The `skills/research-tools/SKILL.md` skill detects research, analysis, and PRD-related intent and routes to the correct command automatically.

## Troubleshooting

| Issue | Fix |
|-------|-----|
| `/web-research` fails with MCP error | Restart Claude Code to reload MCP servers; verify `uvx` is installed |
| `uvx` not found | Install with `pip install uv` or `brew install uv` |
| `/prd` fails to save | Ensure you have write permission in the project directory |
| `tasks/` directory missing | Not needed — `/prd` creates it automatically |
| `/project-analysis --all` hangs | Try `/project-analysis --quick` for a faster scan |

## License

MIT

## Part of

- [claude-config](https://github.com/SkyWalker2506/claude-config) — Multi-Agent OS for Claude Code (134 agents, local-first routing)
- [Plugin Marketplace](https://github.com/SkyWalker2506/claude-marketplace) — Browse & install all 18 plugins
- [ClaudeHQ](https://github.com/SkyWalker2506/ClaudeHQ) — Claude ecosystem HQ
