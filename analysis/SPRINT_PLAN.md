# Sprint Plan — ccplugin-research-tools

**Generated:** 2026-04-22  
**Source:** analysis/MASTER_ANALYSIS.md  
**Total Sprints:** 3

---

## Summary

| Sprint | Focus | Tasks | SP | Status |
|--------|-------|-------|----|--------|
| 1 | Critical Fixes & Infrastructure | 5 | 7 | Planned |
| 2 | DX Improvements | 5 | 9 | Planned |
| 3 | Documentation & Quality | 5 | 8 | Planned |

**Total:** 15 tasks, 24 SP

---

## Sprint 1 — Critical Fixes & Infrastructure (SP: 7)

**Goal:** Fix broken install experience and remove interactive friction in automated contexts.

| Task | Title | Priority | Effort | SP | Labels | depends_on | wave |
|------|-------|----------|--------|----|--------|------------|------|
| RT-S1-01 | Add `.mcp.json` at repo root with fetch MCP config | P0 | S | 1 | infrastructure | — | W1 |
| RT-S1-02 | Add `mkdir -p tasks/` guard in /prd before saving output | P0 | S | 1 | bug | — | W1 |
| RT-S1-03 | Add `--all` flag to /project-analysis skipping 12-question flow | P0 | M | 2 | dx, feature | — | W1 |
| RT-S1-04 | Add MCP unavailability error messages with remediation steps | P1 | S | 1 | ux, dx | RT-S1-01 | W2 |
| RT-S1-05 | Fix `/prd` output path — ensure consistent save to `analysis/` | P1 | M | 2 | bug, arch | RT-S1-02 | W2 |

**Verify:** `ls /Users/musabkara/Projects/ccplugin-research-tools/.mcp.json` → exists; grep for `mkdir` in prd.md; grep for `--all` in project-analysis.md

---

## Sprint 2 — DX Improvements (SP: 9)

**Goal:** Reduce repetition, unify output conventions, add power-user flags.

| Task | Title | Priority | Effort | SP | Labels | depends_on | wave |
|------|-------|----------|--------|----|--------|------------|------|
| RT-S2-01 | Extract shared constants block (model, max tool calls) to each command header | P1 | S | 1 | refactor | — | W1 |
| RT-S2-02 | Add `--quick` flag to /web-research for 5-minute rapid scan | P1 | M | 2 | feature, dx | — | W1 |
| RT-S2-03 | Add project context injection to /web-research (read CLAUDE.md/README first) | P2 | M | 2 | feature | RT-S2-01 | W2 |
| RT-S2-04 | Cache web-research results to `analysis/web-research-cache.md` | P2 | M | 2 | performance | RT-S2-03 | W2 |
| RT-S2-05 | Improve SKILL.md trigger patterns — add synonym groups, example phrasings | P2 | S | 2 | quality | — | W1 |

**Verify:** grep `--quick` in web-research.md; grep `CLAUDE.md\|README` in web-research.md; SKILL.md has expanded trigger table

---

## Sprint 3 — Documentation & Quality (SP: 8)

**Goal:** Complete documentation and add output validation.

| Task | Title | Priority | Effort | SP | Labels | depends_on | wave |
|------|-------|----------|--------|----|--------|------------|------|
| RT-S3-01 | Add end-to-end workflow guide to README (web-research → analysis → prd → ralph) | P1 | M | 2 | docs | — | W1 |
| RT-S3-02 | Add JSON schema validation block to /ralph for prd.json output | P1 | M | 2 | quality | — | W1 |
| RT-S3-03 | Add troubleshooting section to README (MCP, model, path errors) | P2 | S | 1 | docs | — | W1 |
| RT-S3-04 | Add example outputs to web-research.md and project-analysis.md | P3 | M | 2 | docs | RT-S3-01 | W2 |
| RT-S3-05 | Add confidence scoring guidance to SKILL.md routing rules | P3 | S | 1 | quality | — | W1 |

**Verify:** README has "Workflow" section; ralph.md has schema block; README has "Troubleshooting" section

---

## Risk Assessment

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| `.mcp.json` format not matching Claude Code spec | Medium | High | Test against claude-config reference |
| `--all` flag breaks existing /project-analysis UX | Low | Medium | Keep interactive as default, `--all` is opt-in |
| Cache file growing unbounded | Low | Low | Add 30-day TTL note in cache logic |

---

## Dependencies

- Sprint 2 tasks RT-S2-03, RT-S2-04 depend on Sprint 1 RT-S1-01 (MCP config)
- Sprint 3 tasks can run independently of Sprint 2
