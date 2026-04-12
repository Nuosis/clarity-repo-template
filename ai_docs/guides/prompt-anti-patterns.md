# Prompt Anti-Patterns

This guide is for killing prompt bloat and fake sophistication.

## 1. Writing the prompt before defining the objective

**Bad smell:** the prompt is polished, but no one can say what success is.

**Why it hurts:** the model may produce impressive-looking output that solves the wrong problem.

**Fix:** state the objective, artifact, decision rule, and constraints first.

## 2. Ignoring the pain of being wrong

**Bad smell:** instructions focus on style while the real business risk is misclassification, hallucination, or bad automation output.

**Why it hurts:** the prompt optimizes for vibes instead of failure prevention.

**Fix:** identify the highest-cost failure and encode defenses against that specific pain.

## 3. Cargo-cult roleplay

**Bad smell:** “You are a world-class, elite, expert, genius…”

**Why it hurts:** token cost goes up; signal usually does not.

**Fix:** include role framing only when it changes perspective, domain assumptions, or output behavior.

## 4. Un-testable instructions

**Bad smell:** “be insightful,” “think deeply,” “use best judgment,” “be comprehensive.”

**Why it hurts:** these lines sound useful but are hard to verify and easy to ignore.

**Fix:** replace vague aspirations with observable requirements.

## 5. Stuffing every possible rule into one prompt

**Bad smell:** the prompt contains every lesson ever learned, regardless of whether it applies to this task.

**Why it hurts:** important instructions get diluted; maintenance becomes impossible.

**Fix:** keep the prompt task-specific and prove each line is needed with evals or ablation.

## 6. No explicit output contract

**Bad smell:** output format is implied, loosely described, or buried in prose.

**Why it hurts:** downstream consumers break; reviewers waste time interpreting answers.

**Fix:** specify the exact structure, allowed values, and what to do when information is missing.

## 7. Only testing happy paths

**Bad smell:** prompt “works” on clean examples but fails on ambiguity, conflict, or incomplete inputs.

**Why it hurts:** real-world inputs are messier than demos.

**Fix:** include ambiguous, adversarial, missing-data, and format-stress cases in the eval suite.

## 8. Mistaking longer for safer

**Bad smell:** every failure adds three paragraphs.

**Why it hurts:** prompts grow, clarity drops, and new contradictions appear.

**Fix:** patch the smallest instruction that fixes the observed failure, then re-run the full eval suite.

## 9. Changing prompts without a “materially better” test

**Bad smell:** revisions are accepted because they feel cleaner or more sophisticated.

**Why it hurts:** teams accumulate churn, not quality.

**Fix:** keep a simple gate: the new version must improve important evals, reduce variance, shorten the prompt without regressions, or make failures easier to detect.

## 10. Never checking whether each line matters

**Bad smell:** nobody knows which lines are critical versus decorative.

**Why it hurts:** the prompt becomes folklore instead of an engineered artifact.

**Fix:** run line-removal tests. If deleting a line changes nothing important, remove it.

## 11. Hiding policy in examples only

**Bad smell:** critical behavior is shown in examples but never stated in the rules.

**Why it hurts:** the model may imitate examples inconsistently; maintainers miss the real contract.

**Fix:** keep essential policy in explicit instructions, then use examples to reinforce edge cases.

## 12. Overfitting to one eval case

**Bad smell:** a prompt revision solves the latest failure but quietly breaks previous cases.

**Why it hurts:** quality whack-a-mole.

**Fix:** maintain a stable regression suite and rerun all of it after every change.

## Quick review checklist

Before approving a prompt, ask:

- Is the objective explicit?
- Is the highest-cost failure explicit?
- Is the output contract explicit?
- Does the eval suite reflect real failure modes?
- Can we justify every line?
- Is this revision materially better, or just different?

If any answer is no, the prompt is not done.
