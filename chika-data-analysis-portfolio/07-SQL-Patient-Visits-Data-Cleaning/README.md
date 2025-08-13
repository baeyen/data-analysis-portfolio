# 07 — SQL Data Cleaning: Patient Visits
*From noisy hospital logs to analysis-ready truth.*

---

## Overview
This project cleans a messy **patient visits** dataset in **SQL Server**.  
The raw table had duplicates, mixed casing, missing charges, and inconsistent status values.  
Using SQL-only transforms, I produced a reliable table for reporting and downstream analytics.

---

## What I cleaned
- **Duplicates:** removed repeated visits (same PatientID + VisitDate)  
- **Text standardization:** proper-case **Department** and **Doctor** names  
- **Statuses:** normalized to `Checked-In`, `Discharged`, or `Unknown`  
- **Charges:** coerced text to numeric; non-numeric → `NULL`  
- **Export:** saved a clean Excel workbook for easy review

---

## Project structure

```

/07-SQL-Patient-Visits-Data-Cleaning/
├─ README.md                     # this file
├─ workbooks/
│  ├─ PatientVisits\_Dirty.xlsx   # raw export
│  └─ patients vists cleaned.xlsx# cleaned export (final)
├─ docs/
│  ├─ SQL\_Data\_Cleaning\_Project\_Summary\_Celestine.docx
│  └─ Portfolio Summary.docx
└─ outputs/
└─ screenshots/
├─ IMG-20250726-WA0005.jpg # invalid timelines / date fixes
├─ IMG-20250726-WA0006.jpg # duplicate check
├─ IMG-20250726-WA0007.jpg # department / text standardization
├─ IMG-20250726-WA0008.jpg # type casting & conversions
├─ IMG-20250726-WA0009.jpg # charges cleaning
└─ IMG-20250726-WA0010.jpg # final cleaned table preview

````

*(Folder names match the rest of my portfolio: `workbooks/`, `docs/`, `outputs/screenshots/`.)*

---

## Core SQL (simplified)

Create a clean table from the raw feed:

```sql
-- Build cleaned table
SELECT
    PatientID,
    Name,
    DOB,
    VisitDate,
    -- Proper-case text fields
    CONCAT(UPPER(LEFT(Department,1)),
           LOWER(SUBSTRING(Department,2,LEN(Department)))) AS Department,
    CONCAT(UPPER(LEFT(Doctor,1)),
           LOWER(SUBSTRING(Doctor,2,LEN(Doctor))))         AS Doctor,
    -- Normalize status values
    CASE
        WHEN Status IS NULL OR LTRIM(RTRIM(Status)) = '' THEN 'Unknown'
        WHEN LOWER(Status) = 'discharged'  THEN 'Discharged'
        WHEN LOWER(Status) = 'checked-in'  THEN 'Checked-In'
        ELSE Status
    END AS Status,
    -- Cast Charges to numeric, keep impossible values as NULL
    CASE
        WHEN TRY_CAST(Charges AS FLOAT) IS NULL THEN NULL
        ELSE CAST(Charges AS FLOAT)
    END AS CleanedCharges
INTO dbo.PatientVisitsCleaned
FROM dbo.patientVisitsRaw;
````

Quick validation checks:

```sql
-- 1) Missing charges after cleaning
SELECT COUNT(*) AS missingCharges
FROM dbo.PatientVisitsCleaned
WHERE CleanedCharges IS NULL;

-- 2) Status distribution
SELECT Status, COUNT(*) AS Visits
FROM dbo.PatientVisitsCleaned
GROUP BY Status
ORDER BY Visits DESC;

-- 3) Any residual duplicates?
SELECT PatientID, VisitDate, COUNT(*) AS DuplicateCount
FROM dbo.PatientVisitsCleaned
GROUP BY PatientID, VisitDate
HAVING COUNT(*) > 1;
```

---

## Results (from my run)

* **Missing charges:** 18 rows flagged for follow-up
* **Unknown statuses:** 172 rows (captured for data quality reporting)
* **Residual duplicates:** 0 rows after de-duplication

Screenshots in `outputs/screenshots/` shows each step and result.

---

## Tools

* SQL Server Management Studio (SSMS)
* Excel (before/after exports)
* Windows Snipping Tool (evidence screenshots)
* Word (concise project summary)

---

## Why it matters

* Clean data shortens analysis time and prevents bad decisions.
* This workflow is repeatable for new arrivals of the same feed.
* The cleaned table is ready for dashboards, forecasting, and audit.
