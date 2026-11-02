# Arelle on a sample

Ten files, one per framework and size group plus a charity and a PDF example, loaded in Herm Fischer's Arelle
prototype (the XbrlModel plugin, tag `da2026-final`) on 1 November 2026 (after Graffiti's fixes from this set), with
`arelleCmdLine.py --plugins XbrlModel --internetConnectivity online -f <file> --validate`. Besides Arelle's
`[info]` lines and its two notes on every run (`arelle:oimNamespaceStatusDate`, reading the PWD namespace as the year
2026, and `arelle:oimModelVectorSearchDisabled`):

| Filing | Framework, size | Compiled | Module |
|---|---|---|---|
| 13773218, 2024 | FRS 105, micro | 1 `factUnitDatatypeMismatch` | the same, and 338 `invalidJSONStructure` |
| 05647013, 2022 | FRS 102, small | none | 362 `invalidJSONStructure` |
| 00806618, 2025 | FRS 102, medium | 1 `factMissingUnitDimension` | the same, and 338 `invalidJSONStructure` |
| 02704138, 2026 | FRS 102, large | 1 `factMissingUnitDimension` | the same, and 338 `invalidJSONStructure` |
| 04987690, 2024 | FRS 101, medium | 1 `factMissingUnitDimension` | the same, and 338 `invalidJSONStructure` |
| 01268846, 2024 | FRS 101, large | 2 `factUnitDatatypeMismatch` | the same, and 338 `invalidJSONStructure` |
| 06040998, 2024 | IFRS, large | 3 `factMissingUnitDimension` | the same, 338 `invalidJSONStructure` and 7 `invalidFactDimensionMember` |
| 05660595, 2025 | IFRS, medium | 1 `factUnitDatatypeMismatch` | the same, and 338 `invalidJSONStructure` |
| 05368398, 2025 | FRS 102 charity, small | none | Arelle's model of both FRC taxonomies, imported whole: 703 `invalidJSONStructure`, 8,079 `duplicateLabelObject`, 487 `invalidDomainNetworkObject`, 974 `invalidDomainRelationshipTarget`, 2 `invalidCubeDimensionDomainName`, 4 `missingCoreDomainNameFromCubeDimension` |
| SC177933 on its PDF, 2026 | FRS 102 | none | 362 `invalidJSONStructure` |

What they are:

- **The filings' own units.** `factMissingUnitDimension` and `factUnitDatatypeMismatch` are `ParValueShare` (money per
  share) filed in plain GBP, and once employees filed in GBP. The facts are as filed.
- **Arelle reading the FRC taxonomy** (module form only, which imports it): `invalidJSONStructure` is the taxonomy's
  own non-ASCII member names (`curr:SãoToméPríncipeDobra`), which Arelle's legacy loader turns into names its JSON
  schema rejects, and `invalidFactDimensionMember` is the FRC's `bus:Consolidated` domain used as a member.
- **The charity's module** names two entry points (FRS 102 and the charities taxonomy) and imports each whole, as
  the draft's import rules leave no other way to say which defines what. Arelle then builds and checks its own model of
  both taxonomies: their shared labels count twice (`duplicateLabelObject`), and the cubes, domain networks and
  domains it makes from the FRC's hypercubes (named `FRS-102:group_..._Cube`, Arelle's names) carry
  `bus:CompanyDefault` and `bus:Consolidated` as domain items. None names an object of the Tavi file.

No finding concerns the structure Graffiti writes (groups, networks, cubes, labels) or a name it does not carry.
