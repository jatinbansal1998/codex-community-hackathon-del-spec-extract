# Question Patterns

Use these patterns to keep the walkthrough collaborative, explicit, and low-volume.

Ask no more than 3 questions in a single turn.

## Scope Agreement

- "What workflow should I trace, and what is the best entry point to start from?"
- "How deep should I go from that entry point: only this service, or should I follow internal dependencies too?"
- "What should stay out of scope for this session?"

## Test Framing

- "The tests in `{file}` suggest the workflow does X, Y, and Z. Does that match your understanding, or should I treat one of those as incidental behavior?"
- "I found implementation code but no obvious tests for this branch. Is that expected, or should I keep searching under another name?"

## Observation vs. Confirmation

- "I see `{observation}` at `{citation}`. Is that the intended behavior, or is there context I should add?"
- "I can confirm `{observation}` from code, but I am inferring `{inference}`. Should I include that interpretation, or keep it as an open question?"
- "This branch appears reachable from `{citation}`, but I have not yet found a caller that hits it. Should I keep tracing, or mark it as uncertain for now?"

## Section-Specific Prompts

### Purpose

- "In one to three sentences, how would you describe the purpose of this workflow in your own words?"

### Inputs

- "I see these inputs being read at `{citation}`. Which of them are part of the real contract versus incidental implementation detail?"

### Flow

- "After `{step}`, I see two branches at `{citation}`. Should both be documented in the main flow, or is one effectively exceptional?"

### External Interactions

- "This code calls `{service}` at `{citation}`. What should I say this interaction accomplishes?"

### Side Effects

- "This appears to emit `{effect}` at `{citation}`. Should I record it as a side effect every time, or only under certain conditions?"

### Error Handling

- "I see `{error path}` at `{citation}`. Is this a deliberate fallback, or more of a legacy behavior we still carry?"

### Edge Cases

- "The code assumes `{assumption}` at `{citation}`. Should I record that as an intentional constraint, or as an implicit risk?"

## Inline Classification

- "You confirmed `{behavior}` at `{citation}`. How should I classify it: REQUIRED, ALLOWED_UNDESIRABLE, DEPRECATED, BUG_COMPATIBLE, DEAD_PATH, or UNKNOWN?"
- "Is this behavior something we must preserve, something tolerated for now, or something we believe should go away?"

## ADR Offer

- "That sounds like rationale rather than just behavior. Should I capture it as an ADR?"
- "Do you want me to turn that constraint into an ADR so future changes preserve the why, not just the what?"

## Open Questions

- "You were unsure about `{topic}`. Should I leave it in Open Questions for now, or do you want me to keep tracing before we move on?"
- "This point is still unresolved between code and recollection. Should I record the uncertainty explicitly and continue?"

## Final Review

- "Please read the current draft and tell me what to rewrite first."
- "Should I mark this spec as REVIEWED, or keep it as DRAFT for another pass?"
- "Do you want a suggested `AGENTS.md` snippet that points future work to this spec and these ADRs?"
