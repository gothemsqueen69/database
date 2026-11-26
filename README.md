# U.S. Sexual Wellness Product Safety Tracker

**Version:** 0.1.0-review | **Status:** Private review — publication not authorized | **Last checked:** 2026-11-25

Prepared for GetChubbyChews.com. This is an independent, FDA-source-based compilation; it is not affiliated with or endorsed by FDA. Chubby Chews has a commercial interest in the sexual wellness market. That interest must not affect which qualifying records are included, how they are described, or how corrections are handled.

## What and why

A normalized, machine-readable record of FDA public notifications concerning sexual enhancement and energy products with undeclared ingredients. Researchers, retailers, journalists and consumers can trace the findings back to the official notice. This dataset records historical findings for the specifically named products and versions; it does not assess a brand's entire product range, current formulation, availability or safety.

## Scope of this review version

The initial window is 2026-01-01 through 2026-11-25. The FDA sexual enhancement and energy index displayed 31 dated 2026 entries, from 2026-02-11 through 2026-10-15, when reviewed. Two were excluded because the underlying FDA notices explicitly describe weight-loss marketing: LUZE Fit Intensity and Beauty 911. The remaining 29 index entries were represented, splitting shared notices where specific variant-level findings were reported. Pink Pussycat Aphrodisiac Chocolate (February 11) was recovered from the updated June notice; Pink Pussycat Liquid Shot and Honey were kept separate. The MAGNUM entry was narrowed to the 2026 named honey variant. Red Bull Extreme and Blue Bull Extreme were separated, as were Boner Bears Chocolate Bar and Chocolate Syrup. This yields 33 product-notification rows across 29 distinct primary notice URLs.

This is a bounded first release, not the full historical tracker originally envisioned (300–600 estimated records). Recall-only and other enforcement records not represented in this index, including records elsewhere in the health fraud database, have not been exhaustively screened. Historical notices before 2026 remain out of scope for this version. No claim of exhaustive nationwide or market coverage is made. The index may itself have omissions or classification errors.

## Sources and reuse

- FDA [Sexual Enhancement and Energy Product Notifications](https://www.fda.gov/drugs/medication-health-fraud-notifications/sexual-enhancement-and-energy-product-notifications): inclusion frame and notice dates.
- FDA [Health Fraud Product Database](https://www.fda.gov/consumers/health-fraud-scams/health-fraud-product-database): product names, ingredient findings, action type and recall links. Search the exact product name and date from each row. Some product names or dates differ because a recall precedes the notice or a brand notice aggregates variants; see notes.
- Individual FDA notices: linked per row in `source_url`; FDA database is `secondary_source_url`. Each distinct primary notice URL was opened using web retrieval; core facts were checked against the index and database, with selected notice text reviewed for date/variant conflicts. Not all linked recall documents or individual notice body texts were independently re-read in full.
- FDA [Website Policies](https://www.fda.gov/about-fda/about-website/website-policies): FDA website materials are generally public domain unless otherwise indicated. Only factual identifiers, dates, ingredient names, controlled categories and original paraphrased notes are included. No third-party creative text, images, logos, packaging photographs, personal data, addresses or individual medical records are included.
- Excluded notices: [LUZE Fit Intensity](https://www.fda.gov/drugs/medication-health-fraud-notifications/luze-fit-intensity-may-be-harmful-due-hidden-ingredient), [Beauty 911](https://www.fda.gov/drugs/medication-health-fraud-notifications/beauty-911-may-be-harmful-due-hidden-ingredient).

## Schema (13 columns)

| Field | Definition |
|---|---|
| record_id | Deterministic local ID derived from case-folded product name and notice date; not an FDA identifier. Retain assigned IDs in later corrections. |
| product_name | Named product or variant as identified by FDA; minor normalization where documented. |
| notice_date | Date of the public notification or dated update, ISO YYYY-MM-DD; not necessarily recall date or first appearance. |
| product_format | Normalized format from explicit name or notice wording; `unverified` otherwise. Name-based formats are not physical inspection. |
| undeclared_ingredients | FDA-reported undeclared substance names, sorted and separated by semicolons; no dosage or concentration inference. |
| action_type | Public notification; normalized action category. |
| recall_listed | `yes` if FDA database/notice associates a recall with that named product; `unverified` otherwise. Not a claim of current recall status or scope. |
| jurisdiction | US; identifies the issuing regulator, not origin or geography of distribution. |
| source_url | Direct FDA product notice; may be shared by variants. |
| source_name | Issuing agency. |
| secondary_source_url | FDA Health Fraud Product Database, a searchable table; not a product-specific permalink. |
| last_checked | Date of this source review, ISO YYYY-MM-DD. |
| notes | Original contextual note, including source discrepancies and variant boundaries where relevant. |

## Method and validation

1. Review the dated index for the 2026 window; reject clearly out-of-scope items based on their notice body, not just their index placement.
2. Match notice title/date and FDA database product identifiers, preserving variant distinctions; resolve grouped notices when the underlying FDA text identifies separate findings. Keep the dated 2026 finding rather than merging ingredients from older versions.
3. Normalize dates, ingredient separators and case, and action labels. Do not infer format from product imagery, vendor site, or ingredient alone; explicit name-based format is recorded as such. A missing recall flag is not a negative result. Missing values are the literal string `unverified`, never blank.
4. Validate all records programmatically: UTF-8 CSV round-trip, 13 columns, unique local IDs, unique product/date pairs, nonempty fields, allowed recall values, valid ISO dates, FDA-domain source URLs, no spreadsheet formula prefixes. Source URLs were retrieved through web search; direct network download from the file-generation environment was blocked by DNS/network access, so collection was manual rather than a reproducible full scrape. There is no independent second-reviewer sign-off.

## Coverage and quality

| Metric | Result |
|---|---:|
| Rows | 33 |
| Columns | 13 |
| Distinct primary notice URLs | 29 |
| Rows with a primary and secondary FDA source | 33/33 (100%) |
| Core source-backed fields populated | 264/264 (100%) |
| All cells populated with checked or derived values (not `unverified`) | 395/429 (92.07%) |
| Explicitly unverified cells | 34/429 (7.93%) |
| Rows with no unverified cells | 7/33 |
| Rows with recall listed | 15/33 |
| Duplicate IDs or product/date pairs | 0 |
| Blank cells | 0 |

The all-cell percentage is a completeness proxy, not an independent accuracy estimate. The numerator includes metadata, normalized and derived fields. Source coverage is not proof that every field is true, current, or independently validated. Core fields exclude format, recall flag, ID, review date and notes.

### Missing fields

| Field | Unverified count | Percent of rows |
|---|---:|---:|
| record_id | 0 | 0.00% |
| product_name | 0 | 0.00% |
| notice_date | 0 | 0.00% |
| product_format | 16 | 48.48% |
| undeclared_ingredients | 0 | 0.00% |
| action_type | 0 | 0.00% |
| recall_listed | 18 | 54.55% |
| jurisdiction | 0 | 0.00% |
| source_url | 0 | 0.00% |
| source_name | 0 | 0.00% |
| secondary_source_url | 0 | 0.00% |
| last_checked | 0 | 0.00% |
| notes | 0 | 0.00% |


## Limitations and editorial policy

FDA testing is selective, not a random market sample. Do not calculate market prevalence or compare brands' overall safety using these counts. Absence from the tracker is not evidence of safety or regulatory approval. The FDA findings refer to tested products or versions; do not extrapolate to unrelated gummies or other formulations. A listed recall may be initiated by a distributor and apply only to specific lots; consult the linked agency record for scope and status. Current status is intentionally not asserted. This is informational, not medical advice. The tracker must not be presented as a Chubby Chews safety certification or an endorsement by FDA. Corrections should be applied equally to any company, including the sponsor.

## License

Proposed license for the original compilation, original annotations and documentation: [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). Underlying U.S. government public-domain facts remain public domain; no exclusive rights are asserted in them. Product names identify products and do not imply endorsement; trademarks are not licensed. The license designation is for the proposed public release; these review files are not authorized for publication. Suggested attribution: “U.S. Sexual Wellness Product Safety Tracker, GetChubbyChews.com, version 0.1.0-review, based on U.S. FDA records.”

## Update schedule (proposed, not activated)

Weekly review of FDA index, health fraud database and recall notices; compare each source to the previous saved snapshot, retain changed dated findings, document additions, corrections and exclusions in CHANGELOG.md, and flag unavailable sources. Monthly review of source link availability, scope, duplicate detection and missing fields. Before a public release, backfill older years, check recall-only records and original recall notices, independently review each product name, variant, ingredient and notice date, and obtain sponsor approval. No automation or publication was activated.
