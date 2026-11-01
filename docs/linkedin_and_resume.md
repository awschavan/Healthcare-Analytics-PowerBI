# LinkedIn, GitHub & Resume Copy

## Resume - Projects section

**Healthcare Admissions Analytics Dashboard** | Power BI, DAX, Power Query, Python | [GitHub link]
- Built a 3-page interactive Power BI report on 54,860 hospital admissions (~$1.4B billing), covering volume trends, patient demographics, clinical outcomes and insurance billing.
- Cleaned raw data in Python/pandas: removed 534 duplicates and 106 invalid negative bills, and standardised ~55K inconsistently formatted patient names and 20K+ hospital names.
- Designed a star-schema model with a date dimension, an inactive discharge-date relationship (`USERELATIONSHIP`), and 17 DAX measures including time intelligence, rates and share-of-total.
- Published the project in version-control-friendly PBIP format with a data dictionary, DAX reference and data-quality log.

*Shorter (one-line) version:*
Power BI dashboard on 55K hospital admissions - Python data cleaning, star-schema model, 17 DAX measures, 3 interactive pages.

## GitHub

- **Repository name:** `healthcare-analytics-powerbi`
- **Description:** Power BI dashboard analysing 55K hospital admissions - Python cleaning, star-schema model, DAX measures, 3 report pages
- **Topics:** `power-bi` `dax` `power-query` `data-analytics` `healthcare-analytics` `data-visualization` `pandas` `business-intelligence`
- Add the three screenshots to `images/` before publishing - recruiters look at the picture first.

## LinkedIn post (draft)

I just finished a healthcare analytics project in Power BI.

I started with a dataset of 55K hospital admissions and found real data-quality problems before any charts: inconsistent name casing and titles, 534 duplicate records, and 106 negative billing amounts. I fixed those in Python, then built a star-schema model with a date dimension and 17 DAX measures.

The report has 3 pages:
- Executive overview (admissions, billing, length of stay, monthly trend)
- Patient & clinical insights (age mix, test results, emergency share)
- Billing & insurance analysis

What I focused on: clean modelling, readable DAX, and a layout that answers questions quickly.

Code, data dictionary and DAX reference: [GitHub link]

#PowerBI #DataAnalytics #DAX #HealthcareAnalytics #DataVisualization

## LinkedIn - Featured / Projects section

Add the GitHub link, plus the `.pbix` file or screenshots as media. LinkedIn cannot display a `.pbix`, so use screenshots (or a short screen recording) as the visual.

## Interview talking points

- **Why remove negative bills instead of fixing them?** There was no way to know the correct value; excluding them (and logging it) is more defensible than guessing.
- **Why a separate date table?** Time-intelligence functions need a continuous, marked date table; it also enables the role-playing discharge-date relationship.
- **Why are YoY measures not on a headline card?** The data has partial years (2019, 2024), so a year-vs-year comparison would mislead; the measures are meant for month-level comparison.
- **Honest limitation:** the dataset is synthetic and nearly uniform, so the dashboard demonstrates technique rather than real clinical findings.
