# eDiscovery Data Processing & Quality Control Simulation (SQL Server / SSMS)

## Overview
This project simulates an eDiscovery Data Specialist workflow aligned to LAW/Relativity-style operations: large-volume data loads, load file validation, quality control (QC), and production-ready exports. The focus is on accuracy, repeatability, and documentation—key requirements in government and regulated environments.

## Objectives
- Load large volumes of “document metadata” into SQL Server (SSMS)
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

## Notes on Tool Equivalence
This simulation uses SQL Server to replicate core functions performed in tools like LAW/Relativity (loading, QC, validation, and export verification). The emphasis is on consistent processing logic and documented QC procedures.

## Sample Results (Add screenshots)
Add screenshots here after running:
- Batch record counts
- QC issue summary by type
- Production export counts and sample rows

## Author
Sanny Danfawada — Dallas, TX  
GitHub: https://github.com/MohSan083
