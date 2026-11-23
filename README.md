# Mopsheet

Mopsheet tidies messy Kenyan spreadsheet columns:

- Phone numbers become `+254` followed by nine digits.
- County names get their official spelling.
- KES amounts become plain numbers.

It runs in the browser. Pasted text never leaves your machine.

Mopsheet is our entry for Track 01 ("Test Something Real") of the Toggle Wars hackathon. It carries one Flagsmith experiment: does a paste box that already holds a messy sample make more visitors clean their own data than an empty box does? [EXPERIMENT.md](EXPERIMENT.md) holds the hypothesis, metrics and decision rule, fixed before launch.

## Status

There is no app code yet. Hackathon rule 04 says the main coding work starts at kickoff, on 2026-11-26 at 08:00 IST (05:30 Nairobi time). The repo holds the experiment plan, the glossary, the design decisions and the invented test data. Setup steps, the live URL and the results will be added as the work lands.

## How it will work

1. You paste one or more columns from a spreadsheet.
2. Mopsheet guesses each column's kind (phone, county or amount) and shows the guess. You can change it.
3. You press Clean. Each cell becomes its standard form.
4. Mopsheet doesn't guess at a cell it can't be sure of. It marks the cell "needs a look" and leaves the text as it was.
5. You press Copy and paste the result back into your sheet.

## Layout

| Path | What it holds |
|---|---|
| [EXPERIMENT.md](EXPERIMENT.md) | The experiment, fixed before launch. |
| [GLOSSARY.md](GLOSSARY.md) | The words this project uses and the ones it avoids. |
| [docs/adr/](docs/adr/) | Decisions that are hard to reverse. |
| [fixtures/messy-rows.tsv](fixtures/messy-rows.tsv) | 30 invented messy rows. The first 8 are the sample, and the tests read them. |
| [docs/agents/](docs/agents/) | How coding agents find the issue tracker, the labels and the domain docs. |

The docs will follow four parts, each added once it has real content:

- `docs/tutorials/`: a first run, start to finish.
- `docs/how-to/`: single tasks, such as deploying or running the experiment.
- `docs/reference/`: the cleaners' rules, the flag, the events and the configuration.
- `docs/explanation/`: why the project works the way it does.

## Decisions

- [0001: Own data needs at least one row that is not in the sample](docs/adr/0001-own-data-needs-a-new-row.md)
- [0002: Paste many columns and guess each column's kind](docs/adr/0002-paste-many-columns-guess-each-kind.md)

## Issue tracker

Work is tracked in [GitHub Issues](https://github.com/MghongoDev/Mopsheet/issues). The triage labels are listed in [docs/agents/triage-labels.md](docs/agents/triage-labels.md).

## Cost

Mopsheet runs on free tiers: Flagsmith Cloud's free plan and Vercel's free hosting.
