This project showcases an end-to-end Azure-based data engineering solution integrating various tools for ETL, data modeling, and reporting.

##  Tools & Tech Stack
- **Azure Data Lake Gen2** (Bronze, Silver, Gold zones)
- **Azure Data Factory** for orchestrating ETL pipelines with watermarking
- **Azure Databricks** using PySpark for transformation and dimensional modeling (SCD1)
- **Delta Lake** for scalable data storage and merging
- **Power BI** with DirectQuery for real-time reporting
- **GitHub** for version control

##  Architecture Layers
- **Bronze Layer**: Raw parquet files ingested from GitHub and stored in ADLS
- **Silver Layer**: Cleaned, enriched, and transformed data with new columns (e.g., Year, RevPerUnit)
- **Gold Layer**: Dimensional modeling (Fact and Dim tables) with surrogate keys and merge logic (UPSERT)

## Features
- Incremental loading using Lookup + Stored Procedure in ADF
- Surrogate key generation using `monotonically_increasing_id()`
- SCD Type-1 implementation using DeltaTable merge
- Unified schema managed in Unity Catalog
- Power BI dashboards for business insights (KPIs like Revenue, Units Sold)

## Dashboards
- Units Sold per Dealer/Branch
- Revenue per Product/Model
- Time series by Year and Month

## 📸 Screenshots
All screenshots are included in the `pipeline_screenshots/` directory.
"""

# Recreate dataflow_details.txt content
dataflow_details = """# Data Engineering Pipeline Flow - Azure

1. **Raw Ingestion (Bronze Layer)**
   - Source: GitHub repository
   - Format: Parquet
   - Storage: Azure Data Lake Gen2 - Bronze Container

2. **Silver Layer (Data Transformation)**
   - Notebook: `silver_notebook`
   - Actions:
     - Derive new columns like `model_category`, `Year`, and `RevPerUnit`
     - Write cleaned dataset to Silver zone in ADLS

3. **Gold Layer (Modeling and Dimensional Load)**
   - Notebooks: `gold_dim_date`, `gold_dim_dealer`, `gold_fact_sales`, etc.
   - Actions:
     - Load DIM tables with surrogate keys
     - Apply merge logic to update or insert using Delta Lake UPSERT (SCD1)
     - Fact table joins all DIMs to form star schema

4. **Incremental Load Logic**
   - ADF pipeline with Lookup → Copy Data → Stored Proc (Watermark update)
   - Supports re-runs without duplicate load

5. **Power BI**
   - Connected to Gold layer using DirectQuery
   - Visualized trends by Dealer, Branch, Model, and Year

6. **Unity Catalog**
   - All tables managed under `cars_catalog` → `gold` schema
   - Ensures governed data access and metadata tracking
"""
