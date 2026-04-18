---
name: spec-extract
description: Collaboratively reverse-engineer a single production workflow into a reviewed current-state specification and optional ADRs. Use when Codex needs to document how an existing workflow behaves today from a file:function entry point, route, job, event handler, or workflow description, especially in older codebases where intent must be recovered from tests and implementation. Follow a collaborative loop of proposing, confirming, writing, then moving to the next section, update the spec incrementally on disk, classify behaviors inline with the developer, and move anything unconfirmed into Open Questions instead of the spec body.
---

# Spec Extract

## Overview

Use this skill to build a workflow spec with the developer, not for the developer. Treat code as evidence, treat the developer as the authority, and treat the spec as confirmed truth only.

Keep the core documents close at hand:

- Use [references/spec-template.md](references/spec-template.md) as the target document structure.
- Use [references/adr-template.md](references/adr-template.md) when the developer confirms a decision should become an ADR.
- Use [references/question-patterns.md](references/question-patterns.md) to keep questions focused and low-volume.
- Use [references/behavior-classification.md](references/behavior-classification.md) when asking the developer to classify confirmed behaviors.

## Non-Negotiables

- Ask at most 3 questions per turn.
- Distinguish observation from inference every time.
- Cite every observation with `file:line` or `file:function`.
- Read tests before implementation when relevant tests exist.
- Never write unconfirmed content into the spec body.
- Put unresolved or unknown items into Open Questions, not into confirmed sections.
- Let the developer redirect scope, depth, ordering, or wording at any time.
- Narrate exploration when tracing a long call chain or reading a large file.
- Do not execute the application or workflow unless the developer explicitly changes the task.

## 1. Scope the Session

- Ask the developer to identify the workflow and entry point.
- Accept flexible starting inputs such as `file:function`, route, job name, event listener, or plain-language workflow description.
- Ask how deep to trace: only the local service, or deeper into internal dependencies.
- Confirm the code can be located before starting deep exploration.
- Do not create the spec file until the workflow name and boundary are clear.

## 2. Build Context

- Search for tests first with `rg` and related file discovery commands.
- Read the most relevant tests before reading the implementation.
- Present test expectations as proposals, not facts.
- Read the implementation only after the test pass or after confirming that no relevant tests exist.
- Follow the agreed call graph by reading function bodies, imports, handlers, background jobs, and downstream helpers.
- Collect evidence about:
  - entry points and triggers
  - inputs and validation
  - branching flow
  - external interactions
  - side effects
  - error handling
  - implicit assumptions and edge cases

## 3. Run the Walkthrough Loop

Work through the spec sections in order unless the developer explicitly changes the order.

For each section:

1. Read the relevant code and tests silently.
2. Present observations with citations and mark any inference explicitly.
3. Ask the 1-3 highest-value confirmation questions.
4. Wait for the developer to confirm, correct, rewrite, or redirect.
5. Ask for inline behavior classification for each non-trivial confirmed behavior.
6. Offer an ADR only when the developer explains why something exists, not merely what it does.
7. Update the spec file on disk with confirmed text only.
8. Move to the next section only when the developer is satisfied.

Use language like:

- "I see `stripeClient.refund()` at `payments/stripe.ts:42`. Is this the intended refund path, or is there another branch I should capture?"
- "The test at `refund.test.ts:88` expects three retries with no backoff. Should I record that behavior as REQUIRED, ALLOWED_UNDESIRABLE, BUG_COMPATIBLE, DEPRECATED, DEAD_PATH, or UNKNOWN?"

## 4. Write the Spec Incrementally

- Write the live draft to `docs/specs/{workflow-name}.spec.md`.
- Slugify `{workflow-name}` in a stable, readable way.
- Create `docs/specs/` only when first needed.
- Keep the file readable at every step.
- Include the document header and only the sections already discussed and approved.
- Do not prefill future sections with placeholders or guesses.
- Use the developer's wording for Purpose whenever possible.
- Update or rewrite a previously confirmed section immediately if the developer changes it later.
- Mark the spec `DRAFT` until the developer explicitly approves the complete document; then mark it `REVIEWED`.

## 5. Capture ADRs Deliberately

- Notice rationale, constraints, historical context, or tradeoffs in the developer's explanation.
- Ask whether that rationale should become an ADR.
- Before writing the first ADR, ask whether the repo already has a decisions directory or numbering scheme.
- If none exists, use `docs/decisions/` and start from `001`, continuing from the highest existing ADR if the directory already exists.
- Write ADRs only after explicit confirmation.
- Link confirmed ADRs from Section 11 of the spec.
- Do not invent alternatives or rationale the developer did not provide.

## 6. Close the Session

- Summarize unresolved items and write them into Open Questions.
- Present the completed spec for final review.
- Apply requested rewrites immediately.
- Suggest an `AGENTS.md` addition that points future Codex sessions to the spec and any ADRs.
- Do not edit `AGENTS.md` unless the developer explicitly asks for the change.

## Output Rules

- Keep every confirmed claim traceable to a code citation.
- Keep classification decisions owned by the developer.
- Prefer concise prose over dumping raw implementation details.
- Document external systems outside the repo as interactions; do not trace across repositories in this skill.
- Treat "I don't know" as a valid outcome and preserve that uncertainty honestly.
