# Data Dictionary

Source: `data/raw/healthcare_dataset.csv` (55,500 rows, 15 columns - a synthetic healthcare dataset; no real patients).
Model tables are built from `data/processed/` by `scripts/clean_data.py`.

## Fact_Admissions (one row = one hospital admission)

| Column | Type | Description |
|---|---|---|
| Admission ID | Whole number | Surrogate key added during cleaning |
| Patient Name | Text | Cleaned name (title case, honorifics/suffixes removed) |
| Age | Whole number | Age in years at admission |
| Age Group | Text | 0-17, 18-34, 35-49, 50-64, 65+ (derived) |
| Age Group Order | Whole number | Hidden sort key for Age Group |
| Gender | Text | Male / Female |
| Blood Type | Text | A+, A-, B+, B-, AB+, AB-, O+, O- |
| Medical Condition | Text | Arthritis, Asthma, Cancer, Diabetes, Hypertension, Obesity |
| Admission Date | Date | Date admitted (active relationship to Dim_Date) |
| Discharge Date | Date | Date discharged (inactive relationship to Dim_Date) |
| Length of Stay | Whole number | Discharge Date - Admission Date, in days (derived) |
| Admission Type | Text | Elective / Urgent / Emergency |
| Doctor | Text | Attending doctor (cleaned) |
| Hospital | Text | Hospital name (cleaned) |
| Insurance Provider | Text | Aetna, Blue Cross, Cigna, Medicare, UnitedHealthcare |
| Billing Amount | Decimal | Billed amount in USD |
| Room Number | Whole number | Room 101-500 |
| Medication | Text | Aspirin, Ibuprofen, Lipitor, Paracetamol, Penicillin |
| Test Results | Text | Normal / Abnormal / Inconclusive |

## Dim_Date (one row per calendar day, 2019-05-01 to 2024-06-30)

Date (key, marked as date table), Year, Quarter, Month Number, Month Name, Month Year, Month Year Sort, Day Name, Day of Week Number, Is Weekend.

## Relationships

| From | To | Cardinality | Active |
|---|---|---|---|
| Fact_Admissions[Admission Date] | Dim_Date[Date] | Many-to-one | Yes |
| Fact_Admissions[Discharge Date] | Dim_Date[Date] | Many-to-one | No (used by `Total Discharges` via `USERELATIONSHIP`) |
