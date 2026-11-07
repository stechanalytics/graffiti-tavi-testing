# Tagging a PDF of accounts automatically: 50 UK filings

The files behind the blog post "Tagging a PDF of accounts automatically, into Tavi". Fifty sets of UK company accounts
filed at Companies House as Inline XBRL were printed to PDF, each PDF was tagged blind by Graffiti and saved as Tavi,
and Graffiti's tags were compared with the tags the companies filed. Everything needed to repeat the comparison, or to
score another tool on the same PDFs, is here.

## What we found

- Graffiti found **95%** of the figures the companies tagged and printed (3,049 of 3,204).
- Of the 3,126 filed facts paired with a Graffiti figure, **96%** had the same concept as the company chose, and
  **74%** matched every part of the tag: concept, period, dimensions, sign and scale.
- For text (company name and number, the required statements, accounting policies), it found **84%** of what the
  companies tagged (1,498 of 1,791).
- Of the 155 misses, 66 are in fixed-asset notes (in one filing a table continued on a new page without its column
  headings, and most of its class figures were missed), 52 have no row label (mostly totals at the foot of a note) and 25
  are dashes printed for nil.

Many concept disagreements are not plain errors: in some, both tags fit and one is more specific (VAT payable against
other taxation); in others, both give the same value in a small company's accounts but mean slightly different things.
On dimensions, the largest miss is current against within one year, which filers tag one way, the other, or both.

## What is here

| File | What it is |
|---|---|
| `filed/<name>.html` | The accounts as filed (Inline XBRL), from Companies House's free accounts data for 8 October 2026 |
| `pdf/<name>.pdf` | The same accounts printed to PDF by Chromium (A4, backgrounds on), with a text layer and no accessibility tags |
| `tavi/<name>/<name>.tavi.json` | Graffiti's tags as a Tavi file, **module** form: each fact anchored to the PDF by page and box, importing the FRC taxonomy |
| `tavi/<name>/<name>.compiled.tavi.json` | The same, **compiled**: the concepts, dimensions, members and labels used written in, no imports |
| `tavi/<name>/<name>.xbr` | A report package (Report Packages 1.0) holding the module Tavi file and its PDF, as Graffiti's Data tab downloads it |
| `graffiti-figures.csv` | Every figure Graffiti tagged on the PDFs: row label, printed text, concept, period, dimensions, sign, scale |
| `graffiti-text.csv` | Every text fact Graffiti tagged on the PDFs |
| `comparison.csv` | Every numeric fact the companies filed, with the Graffiti figure paired with it (if any) and which fields agree |

The Tavi files are what a Graffiti user downloads, taken from the same tagging the CSVs record. One filing
(`SC177933`) has no compiled file: its compiled download did not finish, a Graffiti bug we are fixing.

`comparison.csv` columns: the filing, row label and value; the filed and Graffiti concept, period, dimensions and sign
side by side; `found` (Graffiti tagged the figure at all); `concept_same`, `period_same`, `dimensions_same`,
`sign_same`, `scale_same` and `all_same`; `paired_by` (`label` when the row labels agreed, `value` when only the value
did); and `hidden_in_filing` for facts the filing tags but does not print. The 95% counts the printed ones only; the
3,126 paired facts include 77 hidden ones whose value is also printed.

## How it was done

- **The filings.** 50 from Companies House's accounts data for 8 October 2026: 30 laid out as tables and 20 as
  positioned text, each with 30 or more tagged figures. Some of the companies are also in the model's training data,
  from a year earlier.
- **The PDFs.** Each filing printed by Chromium. These prints have a clean text layer; scanned PDFs will do worse.
- **The tagging.** Each PDF opened in Graffiti 2.0.87 (commit `136bb9180`, run on 7 November 2026), which tagged it with
  no access to the filing, then saved its Tavi files from the Data tab. The figures are read in the browser; only the
  rows of labels and figures go to Graffiti's model.
- **The scoring.** Each Graffiti figure was paired, one to one, with a filed fact of the same printed value,
  preferring the same row label. "Same concept" means the same concept name; dimensions are compared as a set.

## Scoring your own tool

Tag the PDFs in `pdf/`, then pair your figures with the filed facts in `filed/` (or with the `filed_*` columns of
`comparison.csv`). If you get different results, or a different way of pairing, I would like to hear about it.

## Licence

The accounts are Companies House public records under the Open Government Licence v3.0; see `../LICENCE.md`.
