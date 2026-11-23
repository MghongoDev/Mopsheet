---
status: accepted
---

# Own data needs at least one row that is not in the sample

The primary metric `clean_own_data` fires only when the box holds at least one non-empty row that is not a sample row. The guide's rule was looser: fire whenever the text differs from the sample once whitespace is ignored. Under that rule, a visitor in the `sample_filled` arm who deletes one sample row and presses Clean would count as cleaning their own data. That would hand the sample arm the same easy win that rules out `clean_run`. We chose the stricter rule because it counts only visitors who brought data of their own.

## Consequences

- Once the experiment starts, Flagsmith locks the flag and we cannot change the rule. A change would mean a new experiment.
- A visitor who edits a sample row counts, because the edited row is no longer a sample row. We accept this. Editing a row means typing their own value.
- In the control arm the box starts empty, so the two rules agree there.
