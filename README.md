# Graffiti Tavi testing

Test files for XBRL International's [Project Tavi 1.0](https://www.xbrl.org/Specification/tavi/PWD-2026-09-01/tavi-PWD-2026-09-01.html)
(Public Working Draft, 1 September 2026): real filings from the UK, the US and Europe, each written as a Tavi file
in both of the draft's forms, with what the file could not carry and what a validator found in it. Published examples
of Tavi so far are US SEC filings; this set adds UK and European ones, and Herm Fischer's demonstration filings for
comparison with his Arelle prototype.

Made by S-Tech Analytics with [Graffiti](https://stechanalytics.com), an Inline XBRL viewer, version 2.0.87
(commit `f079f91c6`), on 2026-11-02. Every Tavi file was written by the same code the viewer's Data tab runs when you
download one, so these are what a Graffiti user gets.

**The draft is a draft.** Tavi will change before it is final, and these files will be regenerated when it does.

## The parts

| Folder | What | Filings |
|---|---|---:|
| [`uk/`](uk/README.md) | Companies House accounts: FRS 105, FRS 102, FRS 101 and IFRS, micro to large, 2021 to 2026, and 6 placed on a PDF of the same accounts | 301 |
| [`herm/`](herm/COMPARISON.md) | The five filings of Herm Fischer's Tavi demonstration (Apple and Microsoft 10-Ks, Chevron's Form SD, L'Oréal, Wickes) and Apple's 10-K on Apple's tagged PDF, compared with his output | 6 |
| `sec/` | SEC 10-Ks, one per SIC division (two from Manufacturing), from small to large | 10 |
| `esef/` | ESEF annual reports, one from each of ten countries | 10 |
| [`uk-pdf-tagging/`](uk-pdf-tagging/README.md) | 50 Companies House accounts printed to PDF and tagged blind by Graffiti, with every tag compared with the filed ones (no Tavi files: the tags and the comparison as CSV) | 50 |

`index.csv` lists every filing in the Tavi parts (`uk-pdf-tagging/` has its own CSVs); each part has its own `index.csv` with its files and source.

## What is in each filing's folder

| File | What it is |
|---|---|
| `<name>.tavi.json` | Tavi **module**: the facts, each anchored to its element in the filing (`xbrl:htmlElementId`), the statements' structure (groups, presentation and calculation networks, cubes), importing the filing's taxonomy |
| `<name>.compiled.tavi.json` | Tavi **compiled**: the same, with the concepts, data types, dimensions, members, labels and references the facts use written in, and no imports |
| `<name>.xbr` | A report package (Report Packages 1.0) holding the module and the filing as filed, as Graffiti downloads it (SEC filings) |
| `<name>.tavi.gaps.json` | What the Tavi file could not carry, and why |
| `<name>.tavi.validation.json` | Graffiti's Tavi validator on both forms, each finding under the draft's own error code |
| the filing | as filed (UK, SEC); ESEF filings are linked, not copied (see `LICENCE.md`) |

## How they were made, and how they were checked

Each part's filings were chosen by a stated rule, written in its README or below, with a fixed seed; the scripts are
`graffiti-ml/ch_bulk/tavi_examples.py` (choosing) and `graffiti-ai/src/scripts/tavi_uk_examples.mjs` and
`tavi_more_examples.mjs` (writing) in Graffiti's repository.

- **SEC**: 10-Ks for fiscal years ending in 2025 with a primary document under 6 MB, one per SIC division
  (Manufacturing twice), each taken at a set quantile of its division's tagged figures so the ten range in size.
- **ESEF**: the ten countries with the most filings at filings.xbrl.org other than the UK; in each, the filings of the
  latest period-end year to 2025 that filings.xbrl.org found no error in, taken at a quantile of their tagged figures
  that rises with the country's place, with a report package under 15 MB.

Every file was checked by Graffiti's Tavi validator (76 of the draft's 178 error codes, plus calculation consistency
by Calculations 1.1 interval arithmetic) and a sample was loaded in Herm Fischer's Arelle prototype (tag
`da2026-final`): see `ARELLE.md` and `uk/ARELLE.md`.

## Known issues

- Graffiti's validator finds Errors in 11 UK filings, every one the filing's own (an entity scheme and company number
  written the wrong way round, a unit with no prefix); the Tavi files keep them as filed. `uk/README.md` has the detail.
- A module file imports the filing's own extension taxonomy by the name the filing gives it, which is in the filing's
  zip or report package, not beside the Tavi file: a Tavi processor loading a bare module of an SEC or ESEF filing
  cannot find its concepts. The SEC filings' `.xbr` packages carry it; the compiled files need nothing.
- Most Companies House filings give their tags no id, and the draft locates an HTML element only by its id, so most UK
  facts have no anchor (each gaps file lists them).
- The validator does not yet check per-share units, and covers 76 of the draft's 178 error codes.

## Opening them in Graffiti

Open a `.tavi.json` file on its own and it opens as a report built from the model. Open it together with its filing
(or PDF) and the facts are shown in the document, each where its anchor points.

## Licence

See `LICENCE.md`: the filings are public records under their sources' terms, which differ by part.
