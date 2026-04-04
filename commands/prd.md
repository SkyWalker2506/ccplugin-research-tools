# /prd

Generate a Product Requirements Document for a new feature.

Do NOT implement anything. Only create the PRD.

## Flow

1. Receive feature description from the user
2. Ask 3-5 clarifying questions (with lettered options for quick "1A, 2C" answers)
3. Generate structured PRD
4. Save to `tasks/prd-[feature-name].md`

## Questions Format

```
1. Primary goal?
   A. Option one
   B. Option two
   C. Other: [specify]
```

## PRD Structure

### 1. Introduction/Overview
Brief description and the problem it solves.

### 2. Goals
Specific, measurable objectives.

### 3. User Stories
Each story small enough for one focused session:

```markdown
### US-001: [Title]
**Description:** As a [user], I want [feature] so that [benefit].

**Acceptance Criteria:**
- [ ] Specific verifiable criterion
- [ ] Typecheck/lint passes
- [ ] [UI stories] Verify in browser
```

Criteria must be verifiable. "Works correctly" = bad. "Button shows confirmation dialog" = good.

### 4. Functional Requirements
`FR-1: The system must...` -- explicit, numbered.

### 5. Non-Goals (Out of Scope)

### 6. Technical Considerations (Optional)

### 7. Success Metrics

### 8. Open Questions

## Output

- Format: Markdown
- Location: `tasks/prd-[feature-name].md`
