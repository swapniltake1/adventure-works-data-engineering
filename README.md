# Adventure Works Data Engineering Project

This repository contains an **end-to-end data engineering implementation from scratch** using Azure services and Apache Spark.  
The project ingests raw Adventure Works data, transforms it through a medallion-style architecture, serves it via Synapse, and delivers analytics to Power BI.

## 🚀 Project Goal
Build a production-style modern data platform that:
- Ingests source files from Git/HTTP using **Azure Data Factory (ADF)**.
- Stores raw and curated datasets in **Azure Data Lake Storage Gen2 (ADLS)**.
- Performs scalable transformations using **Azure Databricks + Apache Spark**.
- Exposes analytics-ready data with **Azure Synapse Analytics** (external tables/views).
- Delivers business reporting in **Power BI**.

## 🧱 Tech Stack
- **Azure Data Factory** (or Synapse pipelines) for orchestration and ingestion
- **Azure Data Lake Storage Gen2** for raw/bronze/silver/gold storage
- **Azure Databricks** for Spark-based transformation
- **Apache Spark** for distributed data processing
- **Azure Synapse Analytics** for SQL serving layer
- **Power BI** for dashboards and business reporting

## 📂 Repository Structure
```text
.
├── pipeline/                  # ADF pipeline definitions
├── dataset/                   # Dataset definitions for source/sink
├── linkedService/             # Linked service connections
├── sqlscript/                 # Synapse SQL scripts (schema, tables, views)
├── Data/                      # Sample Adventure Works CSV files
├── factory/                   # Factory definition
├── integrationRuntime/        # Integration runtime configuration
└── credential/                # Workspace identity credentials config
```

## 🔄 End-to-End Workflow (Implemented)
1. **Source configuration**
   - Store source metadata (file URL, sink folder, file name) in a control JSON.
2. **Ingestion with ADF pipeline (`GitToRawData`)**
   - `LookupGit` reads the metadata list.
   - `ForEachgit` iterates through each file entry.
   - `GitToRaw` copies CSV files from HTTP/Git source into ADLS raw zone.
3. **Data lake layering**
   - Raw/bronze layer stores ingested files.
   - Silver layer stores cleaned and standardized data.
   - Gold layer stores analytics-ready curated data.
4. **Transformations (Databricks + Spark)**
   - Clean, cast, join, and enrich domain datasets.
   - Apply business transformations for reporting consumption.
5. **Serving (Synapse SQL)**
   - Create schema and external tables over curated data.
   - Build views for BI-friendly data access.
6. **Consumption (Power BI)**
   - Connect Power BI to Synapse (or curated data endpoint).
   - Build reports and dashboards from gold views.

## 🛠️ How to Use This Repository
1. Import these artifacts into your Azure Data Factory/Synapse workspace.
2. Update linked service credentials and storage account references.
3. Upload `Data/` files (or configure Git/HTTP source as needed).
4. Trigger the `GitToRawData` pipeline.
5. Run Databricks notebooks for silver/gold transformations.
6. Execute SQL scripts in `sqlscript/` to create schema/tables/views.
7. Connect Power BI and build visual reports.
