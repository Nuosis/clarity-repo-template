---
name: prompting
description: Create, review, and improve prompts for task-specific LLM work. Use when Claire needs to draft a new prompt, evaluate an existing prompt, trim prompt bloat, design a prompt eval suite, or decide whether a prompt revision is materially better than the current version.
---

# Prompting

Use this skill to produce lean, testable prompts instead of verbose prompt theater.

## Core rule

Start from the job, not the wording.

Always establish:

1. **Objective** — what must become true
2. **Pain if wrong** — what costly failure must be prevented
3. **Output contract** — exact artifact/schema expected
4. **Eval suite** — cases that prove the prompt works
5. **Improvement gate** — how you decide a revision is materially better

If any of those are missing, do not over-polish the prompt yet.

## Default workflow

### 1. Frame the objective

Write four bullets:

- User outcome
- Artifact to produce
- Decision rule for success
- Constraints / must-not-do items

### 2. Name the pain

Identify the highest-cost failure and at least one plausible but wrong output.

Ask:

- What would cause pain if this were wrong?
- What bad answer might still look convincing?
- What downstream system or human would be harmed?

### 3. Draft the minimum viable prompt

Include only instructions that change behavior:

- essential role framing, if it matters
- task instructions
- output contract
- uncertainty/refusal handling
- critical constraints

Do **not** add generic filler like “be thoughtful” unless the requirement can be observed in outputs.

### 4. Build the eval suite

Create a compact but representative suite. At minimum include:

- one standard case
- one ambiguous or missing-information case
- one edge or adversarial case
- one strict formatting case

For each case, define:

- why it exists
- expected behavior
- failure to watch for

If useful, read `references/eval-suite-template.md`.

### 5. Run line-value review

For every instruction or section, ask:

- Does this prevent a real failure?
- Does this improve reliability in a way we can observe?
- Would removing it materially worsen eval performance?

Delete lines that do not earn their keep.

### 6. Decide whether the revision is materially better

Use this gate:

Keep the change only if it does at least one of these:

- fixes a known failure without causing a new one
- improves pass rate on an important eval case or slice
- reduces variance across repeated runs
- shortens the prompt without regressions
- makes failures easier to detect or recover from

If the new version is only different, prefer the shorter one.

## Output pattern

When asked to create or review a prompt, structure your response like this unless the user wants a different format:

### Objective
- User outcome:
- Artifact:
- Decision rule:
- Constraints:

### Pain if wrong
- Highest-cost failure:
- Plausible but wrong output:
- Downstream damage:

### Prompt
```text
[proposed prompt]
```

### Eval suite
- Case:
  - Why it exists:
  - Expected behavior:
  - Failure to watch for:

### Material-improvement check
- Current weakness:
- What changed:
- Why this is materially better:
- Risk introduced:

## Anti-bloat rules

- Prefer the smallest prompt that can pass the eval suite.
- Never add a line you cannot justify.
- Never accept a revision just because it sounds smarter.
- Do not confuse style improvements with behavioral improvements.
- If the prompt keeps growing, run ablation before adding more.

## References

Read only if needed:

- `references/eval-suite-template.md` — compact template for prompt evals
- `references/review-checklist.md` — fast review checklist for existing prompts
