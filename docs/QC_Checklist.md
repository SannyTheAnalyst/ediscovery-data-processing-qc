\# QC Checklist — Load \& Export Validation



\## Purpose

Ensure accuracy and completeness of data loads and production exports for eDiscovery-style processing workflows.



\## Pre-Load Checks

\- Confirm expected source format (CSV / delimited load file)

\- Confirm required columns exist:

&nbsp; - DocID, Custodian, FileName, FileType, Path, DateCreated, DateModified, FileSizeKB, MD5Hash, PrivilegeFlag, ConfidentialFlag, LoadBatchID

\- Confirm approved FileType list:

&nbsp; - pdf, msg, docx, xlsx, pptx, jpg, png, txt

\- Confirm encryption/transfer method (if applicable) and receipt of all batches



\## Post-Load QC (Raw Ingest)

\- Record count reconciliation:

&nbsp; - Source rows = rows loaded by LoadBatchID

\- Required field validation:

&nbsp; - DocID not null; Custodian not blank; FileType valid; MD5Hash populated

\- Date integrity:

&nbsp; - DateCreated not null (unless documented exception)

&nbsp; - DateCreated <= DateModified

&nbsp; - No future DateCreated

\- File size sanity:

&nbsp; - FileSizeKB > 0

\- Duplicate detection:

&nbsp; - Duplicates by MD5Hash within batch and across batches

\- Privilege/confidential flags:

&nbsp; - Flag distribution reviewed; privileged items identified



\## Export QC (Production Readiness)

\- Export eligibility rules applied:

&nbsp; - Exclude PrivilegeFlag = 'Y' unless specifically requested

&nbsp; - Exclude records with QC issues

\- Record count reconciliation:

&nbsp; - Eligible record count = export record count

\- Bates numbering:

&nbsp; - Sequential, no gaps within ExportBatchID

&nbsp; - BatesStart/BatesEnd format verified

\- Spot-check samples:

&nbsp; - FileType, dates, sizes, hashes present

&nbsp; - Path and filename populated

\- Documentation:

&nbsp; - QC issues summary captured (counts by IssueType)

&nbsp; - Export verification results saved



