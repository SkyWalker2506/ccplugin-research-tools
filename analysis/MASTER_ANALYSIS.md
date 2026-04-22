# Master Analysis — ccplugin-research-tools

**Date:** 2026-04-22  
**Forge Run:** 1  
**Analyst:** Sonnet 4.6 (Jarvis)

---

## Executive Summary

`ccplugin-research-tools` is a Claude Code plugin bundling 4 research/analysis commands: `/web-research`, `/project-analysis`, `/prd`, and `/ralph`. The plugin is structurally sound but has several quality, DX, and completeness gaps that limit its adoption and reliability.

**Overall Score: 6.5/10**

---

## 1. Architecture & Code Quality

**Score: 6/10**

### Findings
- Commands are markdown-only (no code execution), relying entirely on Claude agents for logic — appropriate for this plugin type
- No shared configuration or constants file — each command duplicates settings (e.g., `Max 25 tool calls` appears in multiple places)
- No error handling protocols defined for when MCP tools (fetch, atlassian) are unavailable
- `web-research` command hardcodes research topics that may not apply to all projects
- `project-analysis` has interactive mode (12 categories, one-by-one questions) that creates friction — no `--quick` or `--all` shortcut

### Gaps
- No `plugin.json` manifest validation — format was changed multiple times per git log
- No `.mcp.json` at root (referenced in README but absent)
- Ralph command output format (`prd.json`) not validated against a schema

---

## 2. Documentation & DX

**Score: 7/10**

### Findings
- README is clear and well-structured
- Command docs include usage tables and examples
- Missing: quick-start guide showing a complete workflow (web-research → project-analysis → prd → ralph)
- No troubleshooting section for common MCP failures
- `SKILL.md` auto-trigger lacks confidence scoring — will conflict with other research-adjacent plugins

---

## 3. Completeness & Feature Gaps

**Score: 6/10**

### Findings
- `/project-analysis` asks 12 interactive questions — should support `--all` flag to select all categories automatically
- `/web-research` has no caching — repeated calls for the same project waste context
- `/prd` saves to `tasks/prd-[feature-name].md` but `tasks/` dir may not exist — no mkdir guard
- `/ralph` produces `prd.json` but provides no validation of the output JSON
- No unified output format — each command writes to different directories (`analysis/`, `tasks/`, project root)
- Missing: `--dry-run` flag across commands for previewing without side effects

---

## 4. Security & Infrastructure

**Score: 8/10**

### Findings
- No code execution — attack surface minimal
- Fetch MCP dependency is external; no fallback if MCP unavailable
- No secrets used — clean

---

## 5. Integration & Compatibility

**Score: 6/10**

### Findings
- Tight coupling to claude-config ecosystem (references `~/Projects/claude-config/`)
- No instructions for standalone use without full claude-config setup
- `plugin.json` format has been fixed multiple times — suggests unstable schema
- MCP dependency (fetch) must be pre-installed; no auto-install path
- SKILL.md trigger patterns use exact string matching — fragile for diverse phrasing

---

## Top 20 Action Items (ranked by impact/effort)

| # | Title | Category | Priority | Effort | Impact |
|---|-------|----------|----------|--------|--------|
| 1 | Add `--all` flag to /project-analysis to skip 12-question interactive flow | DX | P0 | S | High |
| 2 | Add `.mcp.json` file at repo root (referenced in README but missing) | Infrastructure | P0 | S | High |
| 3 | Add `mkdir -p tasks/` guard in /prd before saving output | Bug Fix | P0 | S | High |
| 4 | Create end-to-end workflow guide in README (web-research → analysis → prd → ralph) | Docs | P1 | M | High |
| 5 | Add JSON schema validation for ralph's `prd.json` output | Quality | P1 | M | High |
| 6 | Unified output directory (`analysis/`) across all commands | Architecture | P1 | M | High |
| 7 | Add MCP unavailability fallback messages with remediation steps | UX | P1 | S | Medium |
| 8 | Extract shared constants (model, max tool calls) to reusable block | Refactor | P1 | S | Medium |
| 9 | Add `--quick` flag to /web-research for rapid 5-minute scan | Feature | P1 | M | Medium |
| 10 | Improve SKILL.md trigger patterns with fuzzy/semantic matching guidance | Quality | P2 | S | Medium |
| 11 | Add troubleshooting section to README | Docs | P2 | S | Medium |
| 12 | Add `--dry-run` flag for /prd and /sprint-plan | Feature | P2 | M | Medium |
| 13 | Add project-specific context injection to /web-research (read CLAUDE.md first) | Feature | P2 | M | Medium |
| 14 | Cache web-research results to `analysis/web-research-cache.md` | Performance | P2 | M | Medium |
| 15 | Add confidence scoring to SKILL.md auto-trigger routing | Quality | P2 | S | Low |
| 16 | Create standalone setup guide (without full claude-config) | Docs | P2 | M | Low |
| 17 | Add acceptance criteria template to /prd US generation | Quality | P3 | S | Low |
| 18 | Add `--format json` output option to /project-analysis | Feature | P3 | M | Low |
| 19 | Version pin MCP dependencies in `.mcp.json` | Infrastructure | P3 | S | Low |
| 20 | Add example outputs to each command's documentation | Docs | P3 | M | Low |

---

## Cross-Cutting Insights

1. **Interactive friction is the #1 pain point** — /project-analysis requires 12+ answers before starting; a `--all` flag would make it usable in automated contexts (like forge itself)
2. **Missing infrastructure files** — `.mcp.json` is documented but absent; this breaks new installs
3. **Scattered output dirs** — `analysis/`, `tasks/`, root — a unified convention would make the plugin more predictable
4. **Standalone story is weak** — tight coupling to claude-config makes standalone adoption difficult

---

## Recommended Sprint Structure

- **Sprint 1:** P0 bug fixes + missing infrastructure (`.mcp.json`, `--all` flag, `tasks/` guard)
- **Sprint 2:** DX improvements (unified output, shared constants, MCP fallbacks)
- **Sprint 3:** Documentation + quality (README workflow guide, JSON schema, SKILL.md improvements)
