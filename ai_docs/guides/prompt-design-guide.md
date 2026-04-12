# Prompt Design Guide

Good prompts are not long prompts. They are precise, testable instructions tied to a real job.

## 1. Start with the objective

Write the objective before writing the prompt.

Use this format:

- **User outcome:** what must become true
- **Artifact:** what the model must produce
- **Decision rule:** how success is judged
- **Constraints:** what must not happen

If you cannot state those four items cleanly, the prompt is not ready.

### Example

- **User outcome:** triage inbound leads into the right follow-up lane
- **Artifact:** one JSON object per lead
- **Decision rule:** routing matches policy and reasons are traceable
- **Constraints:** no invented facts, no prose outside schema

## 2. Identify the pain if this is wrong

Before drafting instructions, answer:

- What failure would create the most pain?
- What wrong answer would look superficially acceptable?
- What downstream step would break if this output drifted?

This step prevents vague “quality” language and forces the prompt to defend against actual business damage.

### Common pain categories

- **Wrong decision:** the model chooses the wrong path, label, or recommendation
- **Wrong format:** automation breaks because output cannot be parsed
- **Wrong evidence:** rationale sounds good but is unsupported
- **Wrong scope:** the model answers with extras, omissions, or policy drift
- **Wrong confidence:** uncertain cases are stated as certain

Turn the highest-cost pain into explicit instructions and eval cases.

## 3. Define the contract

Specify the minimum contract the model must satisfy.

Include only what changes behavior:

- role or perspective, if it matters
- exact task
- required inputs
- output schema or structure
- refusal / uncertainty handling
- hard constraints

Avoid generic filler like “be thoughtful,” “be accurate,” or “use best practices” unless you can test it.

## 4. Make every line earn its keep

Every instruction should survive this test:

1. Does this line change model behavior in an important way?
2. Can we observe whether it helped?
3. Would removing it create a real failure risk?

If the answer is no, delete it.

### Fast line audit

For each line in the prompt, label it:

- **Critical:** prevents a costly failure
- **Helpful:** improves consistency or format
- **Decorative:** sounds nice but adds no measurable value

Delete decorative lines. Challenge helpful lines. Keep critical lines.

## 5. Build the eval suite before polishing

Do not declare a prompt “good” because it reads well. A prompt is good if it survives representative tests.

Your eval suite should cover:

- **happy path:** ordinary inputs
- **edge cases:** ambiguous, incomplete, or conflicting inputs
- **adversarial cases:** inputs that tempt the model to hallucinate or overreach
- **format compliance:** strict schema/output checks
- **policy cases:** where refusal, escalation, or uncertainty is required

### Minimum eval table

| Case | Why it exists | Expected behavior | Failure to watch for |
|---|---|---|---|
| clean standard input | proves base competence | correct output in correct format | unnecessary verbosity |
| ambiguous input | tests uncertainty handling | ask/flag/escalate correctly | false certainty |
| missing key fact | tests restraint | do not invent | hallucinated field |
| conflicting evidence | tests reasoning discipline | note conflict and resolve per policy | cherry-picking |
| formatting stress | tests automation reliability | exact schema only | extra prose / invalid JSON |

## 6. Validate that every line is needed

Run ablation, not just execution.

Simple process:

1. Run the baseline eval suite.
2. Remove one instruction or section.
3. Run the same eval suite.
4. Keep the line only if removal causes a meaningful regression.

This is the fastest way to catch prompt bloat.

### What counts as meaningful regression

- a case flips from correct to incorrect
- output format becomes less reliable
- ambiguity handling worsens
- rationale becomes less grounded
- variance increases across repeated runs

If nothing materially worsens, the line probably does not deserve to stay.

## 7. Check whether the change is materially better

Do not accept prompt changes because they feel cleaner. Accept them because they improve outcomes.

Use a simple improvement gate:

### Material improvement gate

A prompt revision is worth keeping only if at least one is true:

- it fixes a known failure without causing a new one
- it improves pass rate on an important eval slice
- it reduces output variance on the same task
- it shortens the prompt without lowering quality
- it makes failures easier to detect or recover from

If the change is neutral, prefer the shorter prompt.

## 8. Preferred prompt workflow

1. Write objective and pain statement.
2. Draft the smallest prompt that could work.
3. Build evals that reflect real failures.
4. Run the prompt.
5. Fix the specific failure, not the entire prompt.
6. Re-run the full eval suite.
7. Do a line-value audit.
8. Keep only materially better revisions.

## 9. Prompt skeleton

```md
## Objective
- User outcome:
- Artifact:
- Decision rule:
- Constraints:

## Pain if wrong
- Highest-cost failure:
- Plausible but wrong output:
- Downstream breakage:

## Instructions
[smallest set of instructions that changes behavior]

## Output contract
[exact schema / structure]

## Edge handling
- missing information:
- conflicting information:
- out-of-scope requests:

## Eval suite
- case 1:
- case 2:
- case 3:
- case 4:

## Improvement gate
- what must improve to justify this revision?
```

## 10. A final rule

If you cannot explain why a line exists, it should not be in the prompt.
