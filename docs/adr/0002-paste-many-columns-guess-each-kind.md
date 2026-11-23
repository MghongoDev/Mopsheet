---
status: accepted
---

# Paste many columns and guess each column's kind

The box accepts one or more tab-separated columns, which is what a spreadsheet puts on the clipboard. For each column, Mopsheet guesses the column kind (phone, county or amount) from what most of its rows look like. It shows the guess above the column, and the visitor can change it. The guide described a single column. We widened it so the sample can show all three cleaners at once, and so a visitor can paste a whole sheet in one go.

## Considered options

- **One column, with the kind picked by three buttons.** This is simpler, but it adds a step before the first Clean and shows only one cleaner per sample.
- **Guess each row on its own.** We rejected this. A cell like `0712000001` could be a phone or an amount, and guessing row by row would mix kinds within one column.

## Consequences

- The sample is 8 rows by 3 columns, so the `sample_filled` arm shows every cleaner.
- Rows are compared as whole lines (all columns together) when deciding whether a Clean counts as on own data. See [ADR 0001](0001-own-data-needs-a-new-row.md).
- If most rows don't fit any kind, the guess can be wrong. The visitor fixes it with the column kind control.
