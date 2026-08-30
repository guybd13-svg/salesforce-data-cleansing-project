# Data Migration & Cleansing Project | Salesforce Data Loader

## Overview
This project demonstrates an end-to-end data cleansing and migration workflow: taking a raw, "dirty" leads dataset, cleaning it using Excel, and migrating the cleaned data into Salesforce as Lead records.

## Objective
Simulate a real-world scenario where a messy customer/leads dataset needs to be cleaned, validated, and imported into a CRM system — a common task for Data Analysts and Salesforce Administrators.

## Dataset
The raw dataset (`dirty_leads_dataset.csv`) contained ~978 records with intentionally introduced data quality issues:
- Duplicate records (exact and near-duplicates with formatting variations)
- Missing values (Email, Phone, City, Company)
- Inconsistent formatting (mixed case in City/Status fields, extra whitespace in names)
- Inconsistent phone number formats (with/without country code, dashes, spaces)
- Corrupted/invalid records (malformed dates, invalid email formats)

## Data Cleaning Process
Performed in Microsoft Excel:

1. **Standardized text formatting** — used `PROPER()` and `UPPER()` functions to normalize City and Status fields
2. **Removed extra whitespace** — used `TRIM()` to clean First Name / Last Name fields
3. **Fixed phone number formatting** — restored missing leading zeros and standardized format across all records
4. **Removed duplicate records** — used Excel's Remove Duplicates feature, matched primarily on Email
5. **Removed corrupted records** — manually identified and removed rows with unusable data (invalid emails, malformed dates)
6. **Filled required fields** — populated blank Company fields (required for Salesforce Lead object) with "Unknown"

### Results

| Metric | Count |
|---|---|
| Original records | 977 |
| Duplicates removed | 89 |
| Corrupted records removed | 2 |
| **Final clean dataset** | **888** |

## Salesforce Migration
The cleaned dataset was migrated into a Salesforce Developer Org as Lead records using:
- **Salesforce Data Import Wizard** (initial import)
- **Workbench** (REST API-based insert, used to troubleshoot and complete the migration)

<img width="1440" height="900" alt="צילום מסך 2026-08-30 ב-19 07 21" src="https://github.com/user-attachments/assets/e0b765a3-3e25-4a92-b3c2-a8af015fda53" />

### Challenges encountered & solved
- Salesforce's Bulk API was not enabled by default on Workbench — resolved by switching to standard REST API inserts
- Salesforce's built-in Duplicate Management Rules blocked re-imports of records that had already loaded successfully in a prior (seemingly stuck) import attempt
- Required field validation (`Company`) caught remaining blank values that needed to be filled before import

## Tools & Skills Used
- Microsoft Excel (formulas, data cleaning, Remove Duplicates)
- Salesforce (Lead object, Data Import Wizard, Duplicate Management)
- Workbench (SOQL queries, REST API data operations)
- Data quality assessment & documentation

## Files in this Repository
- `dirty_leads_dataset.csv` — original raw dataset
- `clean_leads_dataset.csv` — final cleaned dataset (887 records)
- `README.md` — this file

## Author
Guy Ben Dahan
