# IRISH PRISON STATISTICS DATASET  
## Methodology and Coversheet

**Dataset:** `FF_Irish_Prison_Stats_Jan_2014_Jan_2026.xlsx`  
**Compiled by:** `@fiannafact`  
**Date:** March 2026  
**Coverage:** January 2014 to January 2026 (13 annual snapshots)

---

## What is this dataset?

This is a structured, machine-readable longitudinal dataset tracking the Irish prison system across four dimensions:

- population
- offence profile
- nationality breakdown
- sentence length

It was built by programmatically extracting data from 13 individual PDF reports published by the Irish Prison Service (IPS), cleaning and normalising the output, and compiling it into this workbook.

---

## Data source

All data originates from the **Irish Prison Service Monthly Information Notes**.

Published at:  
`https://www.irishprisons.ie/information-centre/statistics-information/`

These are official government PDF reports issued monthly by the IPS. Each report is typically 8 to 12 pages and contains standardised tables covering prison population counts, offence classifications, nationality profiles, and sentence length distributions.

The reports are publicly accessible and are the same primary source used by government bodies, journalists, and researchers when citing Irish prison statistics.

See the **Data_Sources** tab for the direct PDF link for each of the 13 reports used.

---

## Why January?

Rather than processing every monthly report across 13 years, approximately 156 PDFs, this dataset uses only the **January** report from each year.

### Rationale

**Consistency**  
January reports provide a fixed annual anchor point, making year-on-year comparisons clean and unambiguous.

**Representativeness**  
The January snapshot captures the standing population, meaning every prisoner physically in custody or on temporary release at a single point in time.

**Feasibility**  
The IPS changed the formatting of these PDF reports multiple times over the 13-year period. Using one report per year allowed manual verification of each extraction.

**Precedent**  
This is the same general approach used in longitudinal prison analysis by bodies such as the CSO and ESRI, relying on annual point-in-time snapshots.

---

## Extraction methodology

**Tools used**

- Python 3
- `pdfplumber` for PDF text extraction
- `pandas` for data manipulation
- regular expressions for pattern matching

### Process

1. The 13 January reports from 2014 to 2026 were downloaded from the IPS website.
2. Each PDF was opened using `pdfplumber` and full text was extracted page by page.
3. Four separate parsing functions were written:

#### Population parser
Extracted per-prison counts for:
- In Custody
- Temporary Release
- Remand / Trial

#### Offence parser
- keyword-matched offence groups
- mapped abbreviated IPS labels to full CSO classification names

#### Nationality parser
Extracted:
- Female
- Male
- Total

for each nationality group.

#### Sentence length parser
Extracted sentence duration categories for male prisoners.

4. Fallback logic was included to handle report-format changes across years, including:
   - older `Sentence Profile` headers versus modern `Sentence length by Age` headers
   - nationality group naming variations
5. Extracted data was compiled into separate sheets within this workbook.

---

## Dataset structure

### Sheet 1: `Methodology`
This coversheet containing methodology, sources, and limitations.

### Sheet 2: `Legend`
Notes and definitions for column names and categories.

### Sheet 3: `Prison_Population`
Per-prison population snapshot for each January.  
**Rows:** 362

### Sheet 4: `Prisoners_By_Offence_Group`
Offence profile of the sentenced population.  
**Rows:** 182

### Sheet 5: `Prisoners_By_Nationality`
Nationality breakdown with Female, Male, and Total counts.  
**Rows:** 111

### Sheet 6: `Prisoners_By_Sentence_Length`
Male sentence duration distribution.  
**Rows:** 65

### Sheet 7: `Data_Sources`
Direct PDF links for all 13 source reports.

---

## Known limitations

### Single-month snapshot
This dataset does not capture intra-year fluctuations or monthly flow data.

### Male-only sentence data
Older reports from 2014 to 2017 only published male sentence breakdowns.

### PDF parsing tolerances
Minor discrepancies of plus or minus 1 to 2 prisoners may exist due to PDF artefacts.

### Offence group mapping
Some offence groups were normalised from abbreviated IPS labels to full CSO classification names.

---

## Citation

**Irish Prison Service**, *Monthly Information Notes* (January editions, 2014 to 2026).  
Data extracted and compiled by `@fiannafact`.  
Source PDFs listed in the `Data_Sources` tab.
