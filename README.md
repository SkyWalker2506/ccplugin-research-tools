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
| `/project-analysis` | Deep 12-category project audit with parallel background agents |
| `/prd` | Generate a Product Requirements Document for a new feature |
| `/ralph` | Convert PRD markdown to `prd.json` for autonomous execution |

## MCP Dependency

This plugin requires the **fetch** MCP server for web research capabilities. The `.mcp.json` file configures it automatically:

```json
{
  "mcpServers": {
    "fetch": {
      "command": "npx",
      "args": ["mcp-fetch-server"]
    }
  }
}
```

## Auto-Trigger

The `skills/research-tools/SKILL.md` skill detects research, analysis, and PRD-related intent and routes to the correct command automatically. You can also invoke commands directly by name.

## Structure

```
ccplugin-research-tools/
  .claude-plugin/
    plugin.json          # Plugin manifest
  commands/
    web-research.md      # Market research agent
    project-analysis.md  # 12-category deep analysis
    prd.md               # PRD generator
    ralph.md             # PRD-to-JSON converter
  skills/
    research-tools/
      SKILL.md           # Auto-trigger routing
  .mcp.json              # MCP server configuration
  README.md
```

## License

MIT

## Part of

- [claude-config](https://github.com/SkyWalker2506/claude-config) — Multi-Agent OS for Claude Code (110 agents, local-first routing)
- [Plugin Marketplace](https://github.com/SkyWalker2506/claude-marketplace) — Browse & install all 14 plugins
