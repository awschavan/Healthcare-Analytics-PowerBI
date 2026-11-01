# Healthcare Admissions Analytics | Power BI

An end-to-end Power BI project analysing **54,860 hospital admissions (May 2019 - May 2024)**: data cleaning in Python, a star-schema semantic model, 17 DAX measures and a 3-page interactive report.

![Executive Overview](executive_overview.png)

## Business questions answered

- How many patients are admitted, and how does volume trend month by month?
- Which medical conditions, insurers and admission types drive volume and billing?
- What do the patient mix (age, gender, blood type, medication) and clinical outcomes (test results, emergency share) look like?
- How do average bill, billing per patient-day and length of stay vary across conditions and insurance providers?

## Report pages

| Page | What it shows |
|---|---|
| **Executive Overview** | KPI cards (admissions, billing, avg bill, avg length of stay), monthly admission trend, admission-type split, condition and insurer breakdowns |
| **Patient Insights** | Age-group distribution, test-result mix by condition, medication and blood-type breakdowns, abnormal-result rate, emergency share |
| **Billing & Insurance** | Total billing by insurer, avg bill by condition, billing by year, insurer x admission-type matrix, billing per patient-day |

All pages are cross-filterable with Year / Gender / Condition / Insurance / Admission Type slicers.

## Headline numbers (after cleaning)

| Metric | Value |
|---|---|
| Admissions | 54,860 |
| Total billing | ~$1.40B |
| Avg bill per admission | ~$25,595 |
| Avg length of stay | 15.5 days |
| Abnormal test-result rate | 33.5% |
| Emergency admissions | 32.9% |

> **Note on the data:** this is a synthetic dataset, and most categories are almost evenly distributed (e.g. each condition is ~16-17% of admissions; average bill differs by only a few percent across insurers). The project's value is in the **pipeline, model and dashboard design**, not in real-world clinical conclusions. The 65+ age group is the largest partly because its bucket spans 25 years vs ~15 for the others. 2019 and 2024 are partial years.

## Data model

```
Dim_Date (1) ──────< Fact_Admissions (*)   [Admission Date]   active
Dim_Date (1) - - - -< Fact_Admissions (*)   [Discharge Date]   inactive, used via USERELATIONSHIP
```

- **Fact_Admissions** - one row per admission, with derived `Length of Stay`, `Age Group`
- **Dim_Date** - marked as date table; `Month Year` sorted chronologically, `Month Name` by month number
- Auto date/time is disabled; implicit measures are discouraged (all numbers come from explicit DAX measures)
- Measures are organised in display folders: Volume, Billing, Clinical, Time Intelligence - see [`docs/dax_measures.md`](docs/dax_measures.md)

## Data cleaning (`scripts/clean_data.py`)

| Issue found in raw data | Rows | Fix |
|---|---:|---|
| Random casing + honorifics/suffixes in patient names (`MS. nAtalIE gAMble`) | 55,467 | Title case, removed Mr./Mrs./Ms./Dr. and MD/DDS/PhD/Jr. |
| Doctor names with the same problems | 2,216 | Same |
| Hospital names with stray commas / dangling "and" | 20,682 | Normalised |
| Exact duplicate records | 534 | Removed |
| Negative billing amounts | 106 | Removed (invalid) |
| Discharge before admission | 0 | Checked - none |

Full log: [`docs/data_quality_log.md`](docs/data_quality_log.md) · Column definitions: [`docs/data_dictionary.md`](docs/data_dictionary.md)

## How to open the project

**Requirements:** [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free, Windows).

1. Download or clone this repository.
2. Double-click **`Healthcare_Analytics.pbip`**. *(If Desktop says the project format is a preview feature: File > Options and settings > Options > Preview features > enable "Power BI Project (.pbip) save option", then reopen.)*
3. **Point the model at your local data folder** (one-time step):
   `Home > Transform data > Edit parameters` → set **DataFolder** to the full path of `data\processed`, e.g. `C:\Users\you\Downloads\healthcare-analytics-powerbi\data\processed` → **OK** → **Apply changes**.
4. Wait for the refresh to finish - all visuals will populate.
5. *(Optional)* `View > Themes > Browse for themes` → `theme/healthcare_theme.json` for the teal/navy palette.
6. `File > Save as` to create a single **`.pbix`** file if you want to share it as one file.

### Re-running the cleaning

```bash
pip install pandas
python scripts/clean_data.py
```

## Repository structure

```
Healthcare_Analytics.pbip              <- open this
Healthcare_Analytics.SemanticModel/    <- data model, relationships, DAX (model.bim)
Healthcare_Analytics.Report/           <- report pages & visuals (PBIR format)
data/raw/                              <- original dataset
data/processed/                        <- cleaned fact + date dimension (loaded by Power BI)
scripts/clean_data.py                  <- cleaning pipeline
docs/                                  <- data dictionary, DAX reference, data-quality log
theme/healthcare_theme.json            <- optional report theme
images/                                <- dashboard screenshots
```

## Skills demonstrated

Power BI · Power Query (M) · DAX (CALCULATE, USERELATIONSHIP, SAMEPERIODLASTYEAR, ALLSELECTED) · Data modelling (star schema, role-playing dates) · Data cleaning (Python / pandas) · Dashboard design · Version-controlled BI (PBIP/PBIR)

## Author

**Your Name** · [LinkedIn](https://www.linkedin.com/in/swapnil-chavan-7b413124a/) · [GitHub](https://github.com/awschavan)
