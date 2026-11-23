# Experiment: does a filled box make visitors clean their own data?

Fixed on 2026-11-23, before any visitor data exists. The commit time of this file is the proof. Nothing below changes once the experiment starts.

## Hypothesis

A paste box that already holds a messy sample raises the share of visitors who clean their own data. Visitors see the expected input before they type, so they know what to paste.

## Arms

| Arm | Flag value | What the visitor sees |
|---|---|---|
| Control | `control` | An empty box with a neutral placeholder. |
| Variation | `sample_filled` | The box holds the sample: 8 invented messy rows in three columns (phone, county, amount). |

Flagsmith serves the arms through the flag `sample_first` in the project `Mopsheet`. The split is 50/50. Each visitor keeps one ID in the browser, so they stay in one arm.

## Metrics

| Metric | Role | Fires when |
|---|---|---|
| `clean_own_data` | Primary. The decision rests on this one. | The visitor presses Clean and at least one non-empty row in the box is not a sample row. |
| `clean_run` | Secondary. Reported, never used to decide. | The visitor presses Clean on a box that is not empty. |

Both metrics count whether the event happened at least once per visitor. Higher is better.

The sample arm wins `clean_run` by default, since pressing Clean on a filled box takes one click. That is why it cannot decide the result.

The "own data" rule is stricter than "the text differs from the sample". Under the looser rule, a visitor who deletes one sample row and presses Clean would count as cleaning their own data. Under this rule they need to add at least one row of their own. See [ADR 0001](docs/adr/0001-own-data-needs-a-new-row.md).

Rows are compared after trimming spaces at both ends and squeezing runs of spaces to one. Empty rows are ignored. In the control arm there is no sample, so any Clean press on a box that is not empty counts.

## Sample size

The baseline is unknown. Suppose 25% of control visitors clean their own data and we want to detect a rise to 35%. The standard two-proportion formula, at 5% significance (two-sided) and 80% power, gives about 330 visitors per arm, or roughly 700 in all. This is a planning figure only.

Flagsmith reports a win probability and a credible interval. These still work at smaller counts, but the interval comes out wider.

## Decision rule

On the morning of Sunday, 2026-11-29 (Nairobi time), refresh the results and read `clean_own_data`.

- If the win probability of `sample_filled` is 90% or higher, roll out `sample_filled` to everyone through the same flag.
- Otherwise keep `control`. Call the result inconclusive and state how many visitors a clear answer would need.

## Looking at the data before Sunday

Before Sunday, check only two things, once a day:

- exposures per day
- how close the split is to 50/50

A large skew means a bug, not luck. Do not stop early because the numbers look good, since early stops inflate false wins.

## If traffic is low

If fewer than 200 visitors have been exposed by Saturday noon, report the result as it stands. Give the interval and the number of visitors a clear answer needs.

Simulated visitors run only in the `development` environment. They never count toward this result, and we never present them as real.

## The sample data

Every row in the sample and in [`fixtures/messy-rows.tsv`](fixtures/messy-rows.tsv) is invented. Phone numbers follow the pattern `07XX 000 0NN` (zero blocks with a two-digit counter) so that they are unlikely to belong to anyone. Any match with a real line is chance.

The sample is the first 8 data rows of that file.

## What leaves the browser

Only three things leave the browser:

- the visitor ID
- the flag request
- the event names

Pasted text never does. We check this in the browser's network tab before launch.
