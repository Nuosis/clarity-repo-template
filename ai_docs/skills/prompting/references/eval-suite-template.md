# Prompt Eval Suite Template

Use this template when designing or reviewing a prompt.

## Objective snapshot

- User outcome:
- Artifact:
- Decision rule:
- Constraints:

## Cases

### Case 1 — standard
- **Input:**
- **Why it exists:** proves base competence
- **Expected behavior:**
- **Failure to watch for:**

### Case 2 — ambiguous / missing information
- **Input:**
- **Why it exists:** tests restraint and uncertainty handling
- **Expected behavior:**
- **Failure to watch for:** hallucination, false certainty

### Case 3 — adversarial / edge case
- **Input:**
- **Why it exists:** tests robustness under confusing or conflicting conditions
- **Expected behavior:**
- **Failure to watch for:** policy drift, brittle reasoning

### Case 4 — output contract stress
- **Input:**
- **Why it exists:** verifies exact format/schema discipline
- **Expected behavior:**
- **Failure to watch for:** invalid JSON, extra prose, missing fields

## Line-value test

For each prompt line or section:

- what failure does this prevent?
- what eval case would fail without it?
- if removed, is the prompt materially worse?

Delete anything without a good answer.

## Material-improvement gate

Ship the revision only if one of these is true:

- important evals improve
- known failure is fixed without regression
- output variance drops
- prompt is shorter with equal quality
- failure detection/recovery is clearer
