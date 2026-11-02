# UK Tavi examples

The UK part of [Graffiti Tavi testing](../README.md). 301 sets of UK company accounts filed at Companies House, each written as a Tavi file: the format of XBRL
International's [Project Tavi 1.0](https://www.xbrl.org/Specification/tavi/PWD-2026-09-01/tavi-PWD-2026-09-01.html)
(Public Working Draft, 1 September 2026). Published examples of Tavi so far are US SEC filings; these are UK ones,
under the UK's own taxonomies (FRC FRS 105, FRS 102, FRS 101 and IFRS), from micro-entities to large companies.
There are also 6 examples of a filing's facts placed on a PDF of the same accounts.

Made by S-Tech Analytics with [Graffiti](https://stechanalytics.com), an Inline XBRL viewer, version 2.0.87
(commit `f079f91c6`), on 2026-11-02. Every file was written by the same code the viewer's Data tab runs when you
download a Tavi file, so these are what a Graffiti user gets.

**The draft is a draft.** Tavi will change before it is final, and these files will be regenerated when it does.
Don't build anything that needs them to stay as they are.

## What is in each folder

`filings/<stem>/`, one per filing (the stem is the bulk data file's name: `Prod224_<yymm>_<company number>_<period end>`):

| File | What it is |
|---|---|
| `<stem>.html` | The accounts as filed (Inline XBRL), from Companies House's free bulk accounts data |
| `<stem>.tavi.json` | Tavi **module**: the facts, the statements' structure (groups, presentation and calculation networks, cubes), importing the FRC taxonomy for the concepts |
| `<stem>.compiled.tavi.json` | Tavi **compiled**: the same, with the concepts, data types, dimensions, members and labels the facts use written in, no imports |
| `<stem>.tavi.gaps.json` | What the Tavi file could not carry, and why (what the draft cannot express, what Graffiti does not write yet) |
| `<stem>.tavi.validation.json` | Graffiti's Tavi validator on both forms: each finding under the draft's own error code |

`pdf/<stem>/`: a filing, the same accounts printed to PDF by Chromium, and the filing's facts placed on the PDF's
pages by page and box (`xbrl:pdfImageLocatorType`), as Graffiti's Open > Place on a PDF does: module and compiled, and
the validator's findings. The PDFs carry no accessibility tags, so there are no page + MCID locators.

`index.csv`: one row per filing: company number and name, period, framework, size, whether its numbers use
dimensions, taxonomy entry point, fact counts, validator error counts, the paths of its files, the bulk data file it
came from and its Companies House filing history page. `pdf-index.csv`: the same for the PDF examples.

## What was chosen, and how

From the Companies House monthly and daily accounts bulk data of October 2025 to October 2026 (period ends 2021 to
2026, HTML filings under 3 MB), sampled at random with a fixed seed across period-end year and size, then classified
from what each filing itself reports:

- **Framework**: its `bus:AccountingStandardsDimension` member (Micro-entities is FRS 105; SmallEntities, which is
  Section 1A, MediumEntities and FRS102 are FRS 102; FRS101; FullIFRS is IFRS), else its taxonomy entry point.
- **Size**: the regime the filing declares (micro-entity, small, medium entity), or small when it reports the small
  companies regime; otherwise medium or large by the Companies Act 2006 thresholds (as from April 2025) on its
  turnover, balance sheet total and employees.
- **Dimensions**: whether any of its numbers sit in a context with a dimension.

Then quotas per framework and size, filled in turn across period-end years and with and without dimensional numbers,
one filing per company. FRS 101 and IFRS filings are few in the bulk data, so those groups hold what there was.

| Framework | micro | small | medium | large | Total |
|---|---:|---:|---:|---:|---:|
| FRS 101 |  |  | 20 | 25 | 45 |
| FRS 102 |  | 80 | 50 | 50 | 180 |
| FRS 105 | 65 |  |  |  | 65 |
| IFRS |  |  | 7 | 4 | 11 |

By period-end year:

| Framework | 2021 | 2022 | 2023 | 2024 | 2025 | 2026 | Total |
|---|---:|---:|---:|---:|---:|---:|---:|
| FRS 101 |  |  |  | 17 | 17 | 11 | 45 |
| FRS 102 | 13 | 13 | 22 | 41 | 47 | 44 | 180 |
| FRS 105 | 12 | 12 | 11 | 10 | 10 | 10 | 65 |
| IFRS |  |  |  | 3 | 6 | 2 | 11 |

With and without dimensional numbers:

| Framework | with | without | Total |
|---|---:|---:|---:|
| FRS 101 | 45 |  | 45 |
| FRS 102 | 132 | 48 | 180 |
| FRS 105 | 32 | 33 | 65 |
| IFRS | 10 | 1 | 11 |

Taxonomy entry points: `FRS-101-2023-01-01.xsd` 25, `FRS-101-2024-01-01.xsd` 1, `FRS-101-2025-01-01.xsd` 19, `FRS-102-2023-01-01.xsd` 102, `FRS-102-2024-01-01.xsd` 31, `FRS-102-2025-01-01.xsd` 103, `FRS-102-2026-01-01.xsd` 7, `IFRS-2022-01-01.xsd` 1, `IFRS-2023-01-01.xsd` 4, `IFRS-2024-01-01.xsd` 2, `IFRS-2025-01-01.xsd` 4, `char-2025-01-01.xsd` 1, `char-2026-01-01.xsd` 1.

## Validation

Every file was checked by Graffiti's Tavi validator, which covers 76 of the draft's 178 error codes plus calculation
consistency (Calculations 1.1 interval arithmetic, under the `oimtce` codes of Herm Fischer's Arelle prototype).
Files with an Error: 11 (`oimce:invalidUnitStringRepresentation` in 1 file, `oimce:invalidURI` in 10 files, `oimte:invalidJSONStructure` in 10 files). The FRC taxonomies publish no calculation linkbase, so
there are no calculation networks to check (0 Warnings, 0 Reviews).

All of them are the filing's own: the entity identifier's scheme and value swapped (`scheme="12040435"` with
`http://www.companieshouse.gov.uk/` as the company number), which Companies House accepted, and one unit measure
`employeeNumber` with no prefix, so in the XHTML namespace. The facts are written as filed.

A sample was also loaded in Herm Fischer's Arelle prototype (the XbrlModel plugin, tag `da2026-final`); see
`ARELLE.md`.

## Opening them in Graffiti

In Graffiti, Open and choose a `.tavi.json` file on its own: it opens as a report built from the model, with its
statements, facts, Data, Review and the Tavi validation view. Choose the `.tavi.json` together with its `.html` (or,
in `pdf/`, its `.pdf`) and the facts are shown on the document, each where its anchor points.

## Known gaps

- **Most Companies House filings give their tags no `id`**, and the draft locates an HTML element only by its id
  (14.3.11), so a fact from such a filing has no anchor in the document: 5,754 of 58,757 facts are
  anchored, and 176 filings have none. Each gaps file lists them. The PDF examples are placed by
  page and box, so they do not have this gap.
- **References**: FRC taxonomies give their references FRC's own roles (Companies Act, FRS paragraphs), which the
  draft's reference types (A.7) do not include, so the compiled files carry no references.
- Each number's display format, scale and sign as tagged are not carried: the draft forbids them beside a value
  (8.4.1). The anchor still points at the printed figure.
- Footnotes no fact links to, links other than footnotes and the tags of a second Inline XBRL target would be left
  out (8.11.1); this set has 0 such items.
- The module form imports the FRC taxonomy by its URL; a Tavi processor needs the taxonomy (or Arelle's legacy loader)
  to resolve it.

## Licence

The accounts are Companies House data, from its
[Free Accounts Data Product](https://download.companieshouse.gov.uk/en_accountsdata.html). Contains public sector
information licensed under the
[Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/). See
`LICENCE.md`.
