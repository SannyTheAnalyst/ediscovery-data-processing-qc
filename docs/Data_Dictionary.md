\# Data Dictionary — eDiscovery Document Metadata



\## raw\_ingest\_documents

\- DocID (BIGINT): Unique document identifier (within batch key)

\- LoadBatchID (INT): Ingest batch identifier

\- Custodian (NVARCHAR): Owner/source of document

\- FileName (NVARCHAR): Document file name

\- FileType (NVARCHAR): Extension/type (pdf, msg, docx, etc.)

\- Path (NVARCHAR): Source path (simulated JEFS / file share path)

\- DateCreated (DATETIME2): Document created date

\- DateModified (DATETIME2): Document modified date

\- FileSizeKB (INT): Size in KB

\- MD5Hash (CHAR(32)): Hash identifier for deduplication

\- PrivilegeFlag (CHAR(1)): Y/N privilege indicator

\- ConfidentialFlag (CHAR(1)): Y/N confidentiality indicator

\- IngestedAt (DATETIME2): Ingest timestamp



\## qc\_issues

\- IssueID (BIGINT): Identity key

\- DocID (BIGINT): Document identifier

\- LoadBatchID (INT): Batch identifier

\- IssueType (NVARCHAR): Category of issue

\- IssueDetail (NVARCHAR): Human-readable detail

\- DetectedAt (DATETIME2): Detection timestamp



\## production\_export\_documents

\- ProdDocID (BIGINT): Identity key for export table

\- ExportBatchID (INT): Export batch identifier

\- DocID (BIGINT): Original document identifier

\- LoadBatchID (INT): Original load batch

\- BatesStart/BatesEnd (VARCHAR): Sequential Bates identifiers

\- ExportedAt (DATETIME2): Export timestamp

\- Plus: mirrored metadata fields for delivery



