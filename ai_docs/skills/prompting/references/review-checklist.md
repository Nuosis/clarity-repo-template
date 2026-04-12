# Prompt Review Checklist

Use this when reviewing an existing prompt.

## Ask in order

1. Is the objective explicit?
2. Is the highest-cost failure explicit?
3. Is the output contract explicit?
4. Does the prompt say what to do with ambiguity or missing information?
5. Does the eval suite cover normal, edge, and formatting cases?
6. Can each line be justified by a real failure mode or measurable gain?
7. Is the latest revision materially better, or just different?

## Common fixes

- delete decorative roleplay
- replace vague quality language with observable requirements
- tighten output schema
- add an ambiguity-handling rule
- add missing regression cases
- remove lines that fail the line-value test
