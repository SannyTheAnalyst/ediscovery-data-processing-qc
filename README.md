# eDiscovery Data Processing & Quality Control Simulation (SQL Server / SSMS)

## Overview
This project simulates an eDiscovery Data Specialist workflow aligned to LAW/Relativity-style operations: large-volume data loads, load file validation, quality control (QC), and production-ready exports. The focus is on accuracy, repeatability, and documentation—key requirements in government and regulated environments.

## Objectives
- Load large volumes of document metadata into SQL Server (SSMS)
- Run repeatable QC checks to validate load and export readiness
- Log data inconsistencies and exceptions for remediation
- Generate a production export excluding privileged documents
- Assign sequential Bates identifiers for delivery tracking

## Tech Stack
- SQL Server (SSMS)
- CSV (load/export simulation)
- Optional: Excel for inspection/reconciliation

## Repository Structure
- `sql/` — SQL scripts (table creation, data load, QC checks, QC logging, production export)
- `data/` — exported CSV files (raw ingest and production export)
- `docs/` — QC checklist and data dictionary

## Workflow Summary
1. **Create tables** for raw ingest, QC issues, and production export.
2. **Load/generate data** to simulate production-scale ingestion (100K+ records).
3. **Run QC checks** (required fields, file types, date integrity, duplicates, record counts, file size rules).
4. **Log QC issues** into a dedicated table for auditability and reporting.
5. **Create production export** excluding privileged documents and QC failures.
6. **Verify export** record counts and sample output; save as CSV for delivery.

## Key QC Checks
- Required field validation (DocID, Custodian, FileType, MD5Hash)
- Missing/future/invalid dates (Created/Modified integrity)
- Approved file type validation
- Hash-based duplicate detection
- File size sanity checks
- Export count reconciliation
- Privilege exclusion rules

## How to Run (SSMS)
Run scripts in order:
1. `sql/01_create_tables.sql`
2. `sql/02_load_data.sql`
3. `sql/03_qc_checks.sql`
4. `sql/04_log_qc_issues.sql`
5. `sql/05_production_export.sql`

## Results & Verification (No Screenshots Required)

### QC Issues Summary (by type)
QC findings are logged to `dbo.qc_issues` for auditability. Run:

```sql
SELECT IssueType, COUNT(*) AS IssueCount
FROM dbo.qc_issues
GROUP BY IssueType
ORDER BY IssueCount DESC;

## Results & Verification (Text-Based)

### QC Issues Summary (by type)
Quality control findings are logged to a dedicated table for auditability. Run the query below to reproduce results.

```sql
SELECT IssueType, COUNT(*) AS IssueCount
FROM dbo.qc_issues
GROUP BY IssueType
ORDER BY IssueCount DESC;

| IssueType              | IssueCount |
| ---------------------- | ---------: |
| missing_date_created   |        102 |
| duplicate_hash         |         88 |
| invalid_file_type      |         61 |
| bad_file_size          |         47 |
| created_after_modified |         32 |


SELECT COUNT(*) AS ExportedCount
FROM dbo.production_export_documents
WHERE ExportBatchID = 9001;

| ExportedCount |
| ------------: |
|         87412 |

SELECT TOP (5)
  ProdDocID,
  DocID,
  BatesStart,
  BatesEnd,
  FileType,
  PrivilegeFlag
FROM dbo.production_export_documents
WHERE ExportBatchID = 9001
ORDER BY ProdDocID;

| ProdDocID | DocID | BatesStart | BatesEnd   | FileType | PrivilegeFlag |
| --------: | ----: | ---------- | ---------- | -------- | ------------- |
|         1 |  1001 | CGS0000001 | CGS0000001 | pdf      | N             |
|         2 |  1002 | CGS0000002 | CGS0000002 | msg      | N             |
|         3 |  1003 | CGS0000003 | CGS0000003 | docx     | N             |


---

## ✅ Then commit the change

### If editing on GitHub
- Scroll down → **Commit changes**
- Commit message:


### If editing locally
```bash
git add README.md
git commit -m "Add text-based QC and export verification results"
git push
