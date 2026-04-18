# ADR Template

Write an ADR only after the developer explicitly confirms that a rationale should be captured.

```markdown
# ADR-{NNN}: {Title}

> Date: {date}
> Status: ACCEPTED
> Context source: spec-extract session for {workflow name}

## Context
Describe the situation, constraint, or historical reason the developer explained.

## Decision
Describe what was decided and what the code currently does because of that decision.

## Consequences
Describe the tradeoffs, constraints on future work, and follow-on effects the developer confirmed.
```

## ADR Rules

- Ask before creating the first ADR if the repo already has an ADR directory or numbering scheme.
- Continue from the highest existing ADR number when a numbering scheme already exists.
- Keep the wording grounded in the developer's explanation.
- Do not invent alternatives considered unless the developer actually mentions them.
- Link each confirmed ADR from Section 11 of the spec.
