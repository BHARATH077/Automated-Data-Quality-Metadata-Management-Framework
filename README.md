# Automated-Data-Quality-Metadata-Management-Framework

## Step1: Automated Data Quality & Metadata Management Framework 

## 🎯 Objective
Set up the base structure and generate synthetic data for testing the data quality validation framework.

## ✅ Tasks Completed
- Created a folder structure:
- Generated 3 example datasets:
- `customers.csv` – user signup data
- `orders.csv` – order transactions (contains intentional data errors)
- `products.csv` – product catalog

- Built a **metadata catalog** (`data/metadata/catalog.csv`) to track:
- Table name
- File path
- Record count
- Last updated timestamp


# Step2: Automated Data Quality & Metadata Management Framework

## 🎯 Objective
Implement **schema validation** to ensure incoming datasets match expected structures.

## ✅ Tasks Completed
1. Defined **expected schemas** (column names + data types) for:
   - customers
   - orders
   - products
2. Wrote a Python-based **schema validation function**:
   - Checks for missing/extra columns.
   - Detects datatype mismatches.
   - Returns validation status (PASS / FAIL).
3. Generated a **schema validation report**:
   - `data/metadata/reports/schema_validation_report.csv`
4. Updated the **metadata catalog** with validation results.


# Step3: Automated Data Quality & Metadata Management Framework 

## 🎯 Objective
Add **data quality validation** to ensure data integrity and detect errors before ingestion.

## ✅ Tasks Completed
- Implemented validation checks for:
  1. **Null Values** – Detect missing or incomplete records.
  2. **Duplicates** – Identify repeated rows in datasets.
  3. **Referential Integrity** – Ensure relationships between datasets (e.g., `orders.customer_id` exists in `customers.customer_id`).
  4. **Negative Values** – Flag invalid numeric entries (e.g., negative order amounts).

- Created a **data quality report** summarizing pass/fail results for each check.
- Updated **metadata catalog** with a `data_quality_status` column.


# Step4: Automated Data Quality & Metadata Management Framework 

## 🎯 Objective
Create an automated **Metadata Management Framework** that tracks schema, record counts, data quality status, and versions for all ingested tables.

## ✅ Tasks Completed

### 1. Schema Extraction
- Extracted data types for all columns in each dataset.
- Stored schema as JSON for easy retrieval.

### 2. Metadata Versioning
- Generated a unique **schema hash** using MD5 for change detection.
- Added timestamp-based **versioning** (`YYYYMMDD_HHMMSS` format).
- Saved historical snapshots.

### 3. Data Quality Integration
- Merged data quality results (`PASS` / `FAIL`) from the Day 3 validation framework.
- Updated current catalog with the latest data quality status.

## 💡 Key Learning
This metadata catalog enables:
- **Auditing**: You can trace schema evolution over time.  
- **Quality Control**: Quickly see which tables failed checks.  
- **Lineage**: Know exactly when and where each table was last updated.


# Step5: Automated Data Quality & Metadata Management Framework 

## 🎯 Objective
Simulate an **Airflow-like orchestration framework** in Python to automate the end-to-end data workflow.

## ✅ Tasks Completed

### 1. DAG Definition
- Created a **Directed Acyclic Graph (DAG)** with the following tasks:
  1. `ingest_data`
  2. `validate_data`
  3. `update_metadata`
- Established dependencies:
ingest_data → validate_data → update_metadata

### 2. DAG Execution Engine
- Sequentially executes each task using **topological sort**.
- Tracks:
- `start_time`
- `end_time`
- `duration_sec`
- `status`
- Automatically halts the pipeline on failure.

### 3. Run Logging
- Stores each DAG run’s results in: data/orchestration/pipeline_runs.csv

## 💡 Key Learning
- Built an **end-to-end automated data pipeline** using only free Python tools.  
- Demonstrated orchestration, logging, and task dependencies — similar to Apache Airflow.  
- Can easily scale by adding more tasks or conditional branches.


# Automated Data Quality & Metadata Management Framework - Day 6

## 🎯 Objective
Implement monitoring, alerts, and dashboarding to visualize and track pipeline performance.

## ✅ Tasks Completed

### 1. Monitoring
- Loaded DAG execution logs (`data/orchestration/pipeline_runs.csv`)  
- Calculated summary metrics:
  - Total DAG runs  
  - Total failed tasks  
  - Total successful tasks  

### 2. Alerts
- Simulated alerting system:
  - Printed warning messages for any task with status `FAIL` or `FAIL_WITH_WARNINGS`  
  - Can be extended to email or Slack notifications

### 3. Dashboard Visualizations (Plotly)
1. **Task Execution Status & Duration** – bar chart of each task duration by status.  
2. **DAG Execution Timeline** – Gantt-like timeline chart of task start/end times.  
3. **Data Quality Status per Table** – bar chart of record counts colored by `dq_status`.

## 💡 Key Learning
- Built **observability** for automated data pipelines.
- Can monitor pipeline health, spot failures, and quickly respond.
- Provides interactive dashboards for **stakeholders and engineers**.

