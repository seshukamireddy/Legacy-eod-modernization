# Project: Legacy EOD Modernization to Azure Lakehouse

## Objective
Rebuild enterprise End-of-Day (EOD) batch pipelines using Azure ADF + ADLS Gen2 + Azure Databricks + Delta Lake + Databricks SQL. 
This project transitions a legacy shell/SQL Server architecture into a scalable, decoupled cloud-native platform.

## Ingestion Types
1. **SFTP Batch Files:** Delimited & Fixed-width datasets, kicked off via storage-based event triggers (`.go` marker file arrival).
2. **REST API Ingestion:** Token-based authentication extracting nested JSON data, landing it into the raw storage layer.

## Key Controls & Guardrails
* **Header/Trailer Validation:** Confirm record counts match trailer values before processing.
* **Business Date Validation:** Ensure file dates align with the expected batch processing window.
* **Rejects/Quarantine & Audit Metrics:** Route corrupted or malformed records to a dedicated isolation layer while logging metadata metrics.
* **Idempotency:** Prevent duplicate processing of identical data batches if a pipeline is re-run.
* **Strict EOD Gating:** Implement notification warnings at T-30 minutes and execute a hard fail if critical files are missing past the deadline.

## Serving Layer
* Downstream flat-file extractions.
* Databricks SQL tables and optimized views for business intelligence tools.

## Success Criteria
An end-to-end operational pipeline execution that seamlessly populates the Bronze, Silver, and Gold layers while maintaining comprehensive execution audit logs.
