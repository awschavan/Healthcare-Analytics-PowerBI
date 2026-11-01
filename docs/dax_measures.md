# DAX Measures

All measures live in the `Fact_Admissions` table, grouped by display folder.

> **Time-intelligence note:** the data covers 2019-05-08 to 2024-05-07, so **2019 and 2024 are partial years**. The YoY measures are most reliable at month level (e.g. the *Admissions by Month* axis) rather than comparing a full year against a partial one.

## Volume

### Total Admissions
Number of patient admissions in the current filter context.
```dax
Total Admissions =
    COUNTROWS ( Fact_Admissions )
```

### Total Discharges
Admissions counted by discharge date (uses the inactive relationship).
```dax
Total Discharges =
    CALCULATE ( [Total Admissions], USERELATIONSHIP ( Fact_Admissions[Discharge Date], Dim_Date[Date] ) )
```

### Total Patient Days
Sum of length of stay in days.
```dax
Total Patient Days =
    SUM ( Fact_Admissions[Length of Stay] )
```

### Admissions % of Total
Share of admissions within the currently selected slicers.
```dax
Admissions % of Total =
    DIVIDE ( [Total Admissions], CALCULATE ( [Total Admissions], ALLSELECTED () ) )
```

## Billing

### Total Billing
Total billed amount.
```dax
Total Billing =
    SUM ( Fact_Admissions[Billing Amount] )
```

### Avg Billing per Admission
Average bill per admission.
```dax
Avg Billing per Admission =
    DIVIDE ( [Total Billing], [Total Admissions] )
```

### Avg Billing per Day
Average billing per patient day.
```dax
Avg Billing per Day =
    DIVIDE ( [Total Billing], [Total Patient Days] )
```

## Clinical

### Avg Length of Stay
Average length of stay in days.
```dax
Avg Length of Stay =
    AVERAGE ( Fact_Admissions[Length of Stay] )
```

### Avg Patient Age
Average patient age in years.
```dax
Avg Patient Age =
    AVERAGE ( Fact_Admissions[Age] )
```

### Abnormal Results
Admissions with an abnormal test result.
```dax
Abnormal Results =
    CALCULATE ( [Total Admissions], Fact_Admissions[Test Results] = "Abnormal" )
```

### Abnormal Result Rate
Share of admissions with an abnormal test result.
```dax
Abnormal Result Rate =
    DIVIDE ( [Abnormal Results], [Total Admissions] )
```

### Emergency Admissions
Admissions of type Emergency.
```dax
Emergency Admissions =
    CALCULATE ( [Total Admissions], Fact_Admissions[Admission Type] = "Emergency" )
```

### Emergency Admission %
Share of admissions that are emergencies.
```dax
Emergency Admission % =
    DIVIDE ( [Emergency Admissions], [Total Admissions] )
```

## Time Intelligence

### Admissions PY
Admissions in the same period last year. Note: 2019 and 2024 are partial years.
```dax
Admissions PY =
    CALCULATE ( [Total Admissions], SAMEPERIODLASTYEAR ( Dim_Date[Date] ) )
```

### Admissions YoY %
Year-over-year change in admissions. Best read at month level.
```dax
Admissions YoY % =
    DIVIDE ( [Total Admissions] - [Admissions PY], [Admissions PY] )
```

### Billing PY
Billing in the same period last year.
```dax
Billing PY =
    CALCULATE ( [Total Billing], SAMEPERIODLASTYEAR ( Dim_Date[Date] ) )
```

### Billing YoY %
Year-over-year change in billing. Best read at month level.
```dax
Billing YoY % =
    DIVIDE ( [Total Billing] - [Billing PY], [Billing PY] )
```
