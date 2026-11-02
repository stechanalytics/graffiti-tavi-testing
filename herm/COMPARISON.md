# Graffiti against Herm Fischer's Arelle prototype

The five filings of Herm Fischer's Tavi demonstration (Data Amplified 2026, his Arelle fork at tag `da2026-final`),
written by Graffiti 2.0.87 (commit `f079f91c6`). His numbers are from his report-mode models (and, for Apple, his
model aligned to Apple's PDF) as run on 1 November 2026; his files are not in this repository. "Located" is a fact with
any locator (an element id, element pointer, PDF page and box or MCID).

| Filing | Facts, his / ours | Located, his / ours | Calculation inconsistencies, his / ours | Our validator, Errors (module / compiled) |
|---|---|---|---|---|
| Apple Inc. | 1,131 / 1,131 | 1,123 / 1,109 | 0 / 0 | 0 / 0 |
| Microsoft Corporation | 1,829 / 1,829 | 1,826 / 1,800 | 21 / 21 | 0 / 0 |
| Chevron Corporation (Form SD) (XBRL 2.1 instance) | 1,183 / 1,183 | 0 / 0 | 0 / 0 | 0 / 0 |
| L'Oréal | 684 / 684 | 684 / 684 | 6 / 6 | 0 / 0 |
| Wickes Group plc | 414 / 414 | 414 / 414 | 0 / 0 | 0 / 0 |
| Apple Inc. on its PDF | 1,131 / 1,131 | 1,123 / 1,106 (1,106 by MCID) | n/a / n/a | 0 / 0 |

Notes:

- Our facts are the default Inline XBRL target's, as Arelle's: Wickes also tags 26 Companies House facts under a
  second target (`UKFRS`), a separate report, so ours and his both have 414.
- His located facts include those he locates by `xbrl:htmlElementPointer` (Apple 14, Microsoft 26): tags with no
  id, located by his proposal, which the draft does not have; ours locate by element id only. On Apple's PDF his 1,123
  are 1,106 on the PDF (850 by MCID, 256 by page and box), those 14 pointers and 3 element ids.
- An XBRL 2.1 instance (Chevron's Form SD) has no document, so neither file locates its facts.
- Calculations are Calculations 1.1 interval arithmetic (`oimtce` codes) on both sides; ours shows some as Review
  where another network balances the same total. The detail is in each `.tavi.validation.json`.
- Apple's PDF is Apple's own accessibility-tagged PDF of its 10-K: we place a fact by page and box, and by MCID too
  where the PDF's tags allow, as he does. The PDF itself is not in this repository (Apple's document); the Tavi file
  names it as `aapl-20250927.pdf`.
