# 🛒 End-to-End Azure Data Engineering Project – Retail (ADF + ADLS + Databricks + Power BI)

> End-to-end Azure data engineering project for a **Retail client**, built using  
> **Azure Data Factory, Azure Data Lake Storage Gen2, Azure SQL Database, Azure Databricks, and Power BI**.

---

## 📌 Business Requirement

We are working for a **Retail client** who wants an **end-to-end data pipeline and analytics solution**.

**Data Sources:**

- **Azure SQL Database**
  - `Transactions` data  
  - `Stores` data  
  - `Products` data  
- **API (JSON via HTTP / GitHub)**
  - `Customers` data

**High-level requirements:**

- Ingest data from **multiple sources** into a **central data lake** (ADLS Gen2).
- Apply **Medallion Architecture**:
  - **Bronze** – Raw data  
  - **Silver** – Cleaned & joined data  
  - **Gold** – Aggregated, business-ready data  
- Use **Azure Data Factory (ADF)** to perform ETL and land data into **ADLS**.
- Use **Azure Databricks (PySpark)** to:
  - Mount ADLS
  - Read Bronze data
  - Clean & transform into Silver
  - Aggregate & prepare Gold layer
- Use **Power BI** for reporting on **Gold layer** data.

---

## 🧰 Tech Stack & Tools

- **Cloud**: Microsoft Azure
- **Data Ingestion / Orchestration**: Azure Data Factory
- **Storage**: Azure Data Lake Storage Gen2 (ADLS)
- **Source Database**: Azure SQL Database
- **Compute / Transformation**: Azure Databricks (PySpark)
- **Visualization**: Power BI Desktop / Power BI Service
- **API Source**: HTTP endpoint (JSON hosted on GitHub)

---

## 🏗️ Architecture Overview (Medallion)

**Medallion Architecture (3 layers of refinement):**

- **Bronze Layer**
  - Raw data from **Azure SQL** and **API**
  - Stored as **Parquet** in ADLS
  - Minimal or no transformation
- **Silver Layer**
  - Data **cleaning & standardization**
  - Type casting, removing duplicates, handling nulls (as needed)
  - Joining **Transactions + Products + Stores + Customers**
  - Stored as **Delta tables** in ADLS
- **Gold Layer**
  - **Business-level aggregations**, e.g.:
    - Total sales amount
    - Total quantity sold
    - Number of transactions
    - Average transaction value
  - Grouped by attributes like:
    - Transaction date
    - Product
    - Store
    - Category
  - Stored as **Delta tables** in ADLS for Power BI consumption

---

## 📂 Suggested Project Structure (GitHub Repo)

```text
azure-retail-de-project/
├── README.md
├── sql/
│   └── retail_tables_and_seed_data.sql      # CREATE TABLE + INSERT scripts
├── adf/
│   └── pipelines/
│       └── pl_retail_bronze_ingestion.json  # ADF pipeline definition (optional export)
├── databricks/
│   ├── bronze_to_silver.ipynb               # Notebook for cleaning & joining
│   └── silver_to_gold.ipynb                 # Notebook for aggregations
├── powerbi/
│   └── Retail_Sales_Report.pbix             # Power BI report file
└── api/
    └── customers.json                       # JSON file hosted on GitHub as raw URL


