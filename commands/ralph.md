# /ralph

Convert a PRD markdown file to `prd.json` for Ralph autonomous execution.

## Output Format

```json
{
  "project": "[Project Name]",
  "branchName": "ralph/[feature-kebab-case]",
  "description": "[Feature description]",
  "userStories": [
    {
      "id": "US-001",
      "title": "[Title]",
      "description": "As a [user], I want [feature] so that [benefit]",
      "acceptanceCriteria": ["Criterion 1", "Typecheck passes"],
      "priority": 1,
      "passes": false,
      "notes": ""
    }
  ]
}
```

## Story Size Rule

Each story must be completable in ONE iteration (one context window).

Right-sized: add a DB column, add a UI component, update server action.
Too big: "build entire dashboard" -- split into schema, queries, UI, filters.

## Story Order: Dependencies First

1. Schema / database (migrations)
2. Backend logic
3. UI components
4. Dashboard / summary views

## Acceptance Criteria

Must be verifiable. Always include `"Typecheck passes"`. UI stories add `"Verify in browser"`.

Bad: "Works correctly". Good: "Filter dropdown has options: All, Active, Completed".

## Conversion Rules

1. Each user story maps to one JSON entry
2. IDs: sequential US-001, US-002...
3. Priority: dependency order
4. All stories: `passes: false`, empty `notes`
5. branchName: `ralph/[feature-kebab-case]`

## Running Ralph

After creating `prd.json`, run from the project directory:

```bash
ralph.sh [max_iterations]
```

Default: 10 iterations. Each iteration spawns a fresh Claude Code instance.

## Archive

If `prd.json` already exists with a different `branchName`, archive first:
- Copy current `prd.json` + `progress.txt` to `archive/YYYY-MM-DD-feature/`
- `ralph.sh` handles this automatically

## Output Validation

After generating `prd.json`, validate the output against this schema before finishing:

### Required Fields Check
```
project        → string, non-empty
branchName     → string, matches pattern "ralph/[a-z0-9-]+"
description    → string, non-empty
userStories    → array, length >= 1
```

### Per-Story Check
```
id             → string, matches "US-NNN"
title          → string, non-empty, max 80 chars
description    → string, contains "As a", "I want", "so that"
acceptanceCriteria → array, length >= 2, includes "Typecheck passes"
priority       → integer >= 1
passes         → boolean, must be false
notes          → string (can be empty)
```

### Self-Correction
If any field fails validation, fix it before saving the file. Do not output an invalid `prd.json`. Show a brief validation summary at the end:

```
prd.json validated:
  ✓ 7 user stories
  ✓ All required fields present
  ✓ All acceptance criteria include "Typecheck passes"
  ✓ branchName: ralph/user-onboarding-redesign
```
