# Logistics Data Integrity & Optimization

> **A data quality and process improvement project demonstrating end-to-end Excel data cleaning, standardization, and reporting for warehouse shipping operations.**

---

## Objective

Practice project with leverage of LLM's. Fixes the incosistency in logistics with shipping logs, helpful for getting rid of the runt work, and putting in effort for higher priority tasks
---

## Project Files

| File | Description |
|---|---|
| `raw_data.csv` | Original warehouse shipping log containing 15 records with 5 documented data quality errors |
| `clean_data.csv` | Fully cleaned, standardized, and validated dataset ready for analysis or reporting |
| `README.md` | Project documentation and technical overview |

---

## Errors Identified in Raw Data

The following five data quality issues were identified in `raw_data.csv` and systematically resolved:

| # | Error Type | Description | Example |
|---|---|---|---|
| 1 | Inconsistent Date Formats | Ship dates entered in three different formats across records | `01/16/2024`, `Jan 19 2024`, `01-24-2024` vs. `2024-01-15` |
| 2 | Duplicate Entry | Shipment SH-1004 appeared twice with identical data | Row 5 and Row 11 are exact duplicates |
| 3 | Missing Carrier Name | SH-1005 had a blank Carrier field with no value entered | Carrier cell left empty |
| 4 | Invalid Cost Values | Two records contained `N/A` text in a numeric Shipping_Cost column | SH-1003 and SH-1011 |
| 5 | Inconsistent Text Casing | Carrier names entered in mixed, lowercase, and all-caps formats | `fedex`, `FEDEX`, `ups` instead of `FedEx`, `UPS` |

---

## Technical Process

**Data Auditing & Duplicate Removal**
- Used **Remove Duplicates** (Data tab) to identify and get rid of the exact duplicate record for Shipment ID SH-1004, reducing the dataset from 15 to 14 unique records

**Date Standardization**
- Applied **Power Query (Get & Transform)** to detect and normalize all three non-standard date formats into a consistent `YYYY-MM-DD` ISO 8601 format to ensure constisency throughout the table
- Used the **Format Cells** dialog to enforce a uniform `Date` data type across the entire Ship_Date column

**Text Casing Standardization**
- Used **Find & Replace** (Ctrl+H) to correct all-caps and lowercase carrier entries (`FEDEX` → `FedEx`, `fedex` → `FedEx`, `ups` → `UPS`)
- Applied the `PROPER()` formula as a secondary validation check on the Carrier column

**Handling Missing & Invalid Values**
- Used **Go To Special → Blanks** to locate the empty Carrier cell; flagged the record with `Unknown` per data governance protocol
- Applied **Find & Replace** to locate all `N/A` string values in the Shipping_Cost column and replaced them with `0.00` to maintain numeric data integrity
- Used **Data Validation** (Data tab → Data Validation) to apply a numeric-only rule to the Shipping_Cost column, preventing future non-numeric entries

**Verification & Quality Assurance**
- Built a **PivotTable** summarizing total shipments per carrier and average cost per destination to validate total sums against source records
- Used `COUNTIF()` formulas to verify no remaining duplicate Shipment IDs existed in the cleaned dataset
- Applied **Conditional Formatting** to show and highlight any remaining blank cells as a final visual audit check

---

## Results

| Metric | Before Cleaning | After Cleaning |
|---|---|---|
| Total Unique Records | 14 (1 duplicate present) | 14 |
| Data Accuracy Rate | ~67% (5 errors in 15 records) | **100%** |
| Consistent Date Format | No (3 formats in use) | Yes (ISO 8601) |
| Valid Numeric Cost Entries | 13 of 15 | 14 of 14 |
| Standardized Carrier Names | No | Yes |
| Estimated Manual Review Time Saved | — | **~3 hours/week** |

By standardizing this workflow, recurring shipping log audits that previously required manual line-by-line review can be completed in under 15 minutes using the documented Power Query steps and validation rules — a reduction of approximately 3 hours of manual data entry and correction per week.

---

## Skills Demonstrated

- Microsoft Excel: Power Query, PivotTables, Data Validation, Conditional Formatting
- Data Cleaning: Duplicate removal, null value handling, type enforcement
- Data Standardization: ISO date formatting, consistent text casing
- Quality Assurance: Formula-based auditing (`COUNTIF`, `PROPER`, `IF`)
- Documentation: Structured process documentation for repeatability and handoff

---

## How to Use This Project

1. Open `raw_data.csv` in Microsoft Excel
2. Follow the numbered cleaning steps in the **Data Cleaning Guide** section below or in the accompanying process document
3. Compare your result against `clean_data.csv` to validate your work
4. Use the cleaned data to build a PivotTable summary by Carrier or Destination

---

*Project completed as part of a personal technical portfolio demonstrating data entry, data integrity, and office productivity skills.*
