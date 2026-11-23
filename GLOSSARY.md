# Mopsheet

Mopsheet tidies messy Kenyan spreadsheet columns in the browser. It also carries one experiment on how the paste box first looks.

## Cleaning

**Cleaner**:
A rule that turns one kind of messy cell into its standard form: phones, counties or amounts.
_Avoid_: Parser, formatter, normaliser

**Column kind**:
The kind of data a pasted column holds: phone, county or amount. It decides which cleaner runs on the column.
_Avoid_: Column type, field type

**Needs a look**:
The state of a cell that a cleaner will not change because it cannot be sure of the right answer. The cell keeps its original text.
_Avoid_: Error, invalid, failed, flagged

**Clean**:
The visitor's act of pressing the Clean button to run the cleaners over the box.
_Avoid_: Run, process, convert

## Experiment

**Visitor**:
One browser that opens the page, known by an ID it keeps between visits.
_Avoid_: User, customer

**Arm**:
One of the two versions of the page that a visitor can see: control or `sample_filled`.
_Avoid_: Variant, bucket, group, cohort

**Sample**:
The 8 invented messy rows that fill the box in the `sample_filled` arm.
_Avoid_: Example, demo data, placeholder

**Own data**:
Rows a visitor pressed Clean on that are not sample rows. A Clean counts as on own data when at least one non-empty row is not a sample row.
_Avoid_: Real data, user data, custom input
