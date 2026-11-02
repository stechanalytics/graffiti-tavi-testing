# Arelle on the Herm, SEC and ESEF parts

Every Tavi file of `herm/`, `sec/` and `esef/` (26 filings, compiled and module), loaded in Herm Fischer's Arelle
prototype (the XbrlModel plugin, tag `da2026-final`) on 2 November 2026 with
`arelleCmdLine.py --plugins XbrlModel --internetConnectivity online -f <file> --validate`. The UK part's sample is in
`uk/ARELLE.md`. Besides Arelle's `[info]` lines and its two notes on every run (`arelle:oimNamespaceStatusDate`,
reading the PWD namespace as the year 2026, and `arelle:oimModelVectorSearchDisabled`):

**Compiled: 25 of 26 raise nothing.** Ondas's 10-K raises 5 `oimte:factUnitDatatypeMismatch` on
`us-gaap:DerivativeFloorPrice`, an `srt-types:perUnitItemType` fact in `iso4217:USD/compsci:item`, a unit the filing
declares; Arelle's model gives the per-unit type no unit signature.

**Module: each raises `oimte:taxonomyNotFound` and every concept missing** (`oime:missingConceptDimension`,
`oimte:invalidQNameReference`, `oimte:invalidDomainClass`). A module imports the filing's own extension taxonomy by
the name the filing gives it (`msft-20250630.xsd`, `http://www.loreal.com/20251231/loreal-2025-12-31.xsd`), and that
schema is in the filing's zip or report package, not beside the bare Tavi file, so Arelle cannot load the taxonomy.
The SEC filings' `.xbr` packages carry the schema with the module; ESEF report packages are not in this repository.
