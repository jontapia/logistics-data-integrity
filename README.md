# Logistics Data Integrity & Optimization

> **A data quality and process improvement practice project displaying the end-to-end Excel data cleaning, standardization, and reporting for warehouse shipping logs and operations.**

---

## Objective

Practice project with leverage of LLM's. Fixes the incosistency in logistics with shipping logs, helpful for getting rid of the runt work, and putting in effort for higher priority tasks Furthermore, used AI to help brainstorm the logic for these formulas provided, personally checked the output to ensure the data was 100% accurate
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

How I Fixed It
Duplicates

Used Excel's Remove Duplicates tool to catch and remove the duplicate SH-1004 record, bringing the dataset down from 15 to 14 unique entries.
Date Standardization

Ran Power Query to detect and normalize all three non-standard date formats into a consistent YYYY-MM-DD (ISO 8601) format, then enforced a uniform Date type across the entire Ship_Date column.
Text Casing

Used Find & Replace to correct carrier names entered in all-caps or lowercase, then ran PROPER() as a secondary check to catch anything that slipped through.
Missing & Invalid Values

Used Go To Special → Blanks to find the empty Carrier cell and flagged it as Unknown following data governance protocol. Replaced all N/A strings in Shipping_Cost with 0.00 to keep the column numeric, then applied Data Validation to prevent the same issue from coming back.
Verification

Built a PivotTable to summarize shipments per carrier and average cost per destination, then used COUNTIF() to confirm no duplicate Shipment IDs remained. Applied Conditional Formatting as a final visual sweep for any leftover blanks.
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
