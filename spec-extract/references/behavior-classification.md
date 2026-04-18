# Behavior Classification

Ask the developer to classify each non-trivial confirmed behavior as soon as it is understood. Do not classify behavior on the developer's behalf.

## Tags

### REQUIRED

Use when the developer says the behavior is intentional and must be preserved.

Examples:

- "Refund requests older than 90 days go to a manual queue because finance policy requires human review."
- "The workflow must emit an audit event for every successful password reset."

### ALLOWED_UNDESIRABLE

Use when the behavior works today but the developer does not want it to be the long-term state.

Examples:

- "We still retry synchronously because we never finished the background job migration."
- "We allow a legacy payload shape, but we want to remove it eventually."

### DEPRECATED

Use when the behavior still exists but is already slated for removal.

Examples:

- "This fallback endpoint remains only for the old mobile client and should disappear after the next sunset."
- "The CLI flag is still accepted for compatibility but should no longer be used."

### BUG_COMPATIBLE

Use when the behavior is known-bad but intentionally preserved for compatibility or risk management.

Examples:

- "The amount rounds incorrectly for one legacy currency, but changing it would break reconciliation."
- "The retry cap is too low, but increasing it now would change customer-visible behavior."

### DEAD_PATH

Use when the developer believes the code path is unreachable or obsolete and it remains only because nobody has removed it yet.

Examples:

- "This branch was for a provider we no longer use."
- "This handler cannot be invoked after the v2 migration."

### UNKNOWN

Use when neither the code nor the developer can confidently classify the behavior yet.

Examples:

- "I can see the branch, but I do not know who relies on it."
- "The timeout exists in code, but I do not know whether it is contractual or accidental."

## Selection Prompt

Use a compact prompt like:

`You confirmed {behavior} at {citation}. How should I classify it: REQUIRED, ALLOWED_UNDESIRABLE, DEPRECATED, BUG_COMPATIBLE, DEAD_PATH, or UNKNOWN?`

## Recording Rules

- Record only behaviors the developer has already confirmed.
- Add a short note when the classification depends on context or has a migration caveat.
- Move still-unresolved items into Open Questions even if they also appear as `UNKNOWN` in the table.
