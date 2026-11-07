# Licence and sources

The filings in this repository are public records, published by the bodies below under their own terms. The Tavi,
gaps, validation and index files were made from them by S-Tech Analytics with Graffiti. Nothing here is endorsed by
any of those bodies or by the companies whose filings these are.

## `uk/` and `uk-pdf-tagging/`: Companies House

The company accounts are from Companies House's Free Accounts Data Product
(https://download.companieshouse.gov.uk/en_accountsdata.html).

Contains public sector information licensed under the Open Government Licence v3.0:
https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/

S-Tech Analytics' files made from them are offered on the same terms, under the Open Government Licence v3.0.

## `sec/` and the SEC filings in `herm/`: the US Securities and Exchange Commission

The 10-Ks and Chevron's Form SD are from EDGAR (https://www.sec.gov/edgar), each linked in its part's `index.csv`. The
SEC says: "Information presented on www.sec.gov is considered public information and may be copied or further
distributed by users of the web site without the SEC's permission" (https://www.sec.gov/privacy). The filings are the
companies' own documents; no further licence is given or implied.

## `esef/` and the ESEF filings in `herm/`: filings.xbrl.org

The ESEF annual reports are from XBRL International's filings.xbrl.org, which collects them from each country's
officially appointed mechanism; filings.xbrl.org states no licence for reuse, and the reports are the companies' own
documents. So the reports themselves (their report packages, and the `.xbr` packages that would hold them) are not
in this repository: each is linked from `index.csv`. The Tavi files hold the facts these companies tagged and
published, including tagged text, so that a Tavi tool can be tested on them.

## Taxonomies

The compiled Tavi files carry the labels, documentation and references of the taxonomy concepts their facts use: the
FRC's UK taxonomies, the IFRS Foundation's IFRS Accounting Taxonomy (through the ESEF and FRC IFRS taxonomies) and
FASB's US GAAP Financial Reporting Taxonomy. Those remain their owners' and are under their own terms
(https://www.ifrs.org/legal/terms-and-conditions/ for the IFRS Taxonomy; FASB's for US GAAP).

## Apple's PDF

`herm/aapl-10k-2025-pdf/` places Apple's 10-K facts on Apple's own PDF of its 10-K. The PDF is Apple's document and is
not in this repository; the Tavi file names it as `aapl-20250927.pdf`.
