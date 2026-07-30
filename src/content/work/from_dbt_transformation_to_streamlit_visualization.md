---
title: From DBT Transformation to Streamlit Visualization
publishDate: 2025-12-01 00:00:00
img: /assets/dbt_streamlit.png
img_alt: From DBT Transformation to Streamlit Visualization
description: |
  I built an end-to-end ELT pipeline using DBT and DuckDB to transform raw retail data into a Star Schema, visualized via an interactive Streamlit dashboard.
tags:
  - DBT
  - DuckDB
  - Streamlit
  - SQL
  - Data Engineering
---

🚀 **Live Dashboard:** [https://nabilboutiyarzist-end-to-end-project.streamlit.app/](https://nabilboutiyarzist-end-to-end-project.streamlit.app/)

### Project Overview & Objectives

The goal of this project was to build a robust **End-to-End Data Pipeline** for a retail business. Starting from raw, disjointed datasets (orders, products, stores), the objective was to provide a clear view of business performance through a **dynamic dashboard**.

The main challenge lay in the **data quality and modeling**: unclear relationships between files (e.g., inconsistent naming conventions like `ARTEAN` vs `product_code`) and raw data requiring type harmonization.

To solve this, I designed a complete **ELT (Extract, Load, Transform)** process. I structured the data modeling to ensure reliability and scalability, resulting in a **Star Schema** optimized for analytics. The final output is an interactive application allowing stakeholders to monitor KPIs such as Gross Revenue, VAT, and Top Products in real-time.

---

### Technologies Used
- **DBT (Data Build Tool)** (For data transformation and testing)
- **DuckDB** (High-performance in-process SQL OLAP database)
- **Streamlit** (Python framework for data visualization)
- **SQL** (Core logic for data modeling)
- **Python** (Environment management and application deployment)

---

### How It Works

The pipeline follows modern Data Engineering best practices, structured in three key layers using **DBT**:

1.  **Staging Layer (Bronze):** Raw data ingestion with type harmonization (using `TRY_CAST` for robustness), cleaning, and column standardization.
2.  **Intermediate Layer (Silver):** Complex logic implementation. I joined Order Headers with Order Lines to reconstruct the full sales context and calculated enriched metrics (Gross Revenue incl. VAT, tax amounts, and order statuses).
3.  **Marts Layer (Gold):** Final modeling into a **Star Schema**. This includes a central `fact_sales` table surrounded by dimensional tables (`dim_product`, `dim_store`, `dim_date`), optimized for analytical queries.

**Methodology:**
Before coding, I established a **Logical Data Model (LDM)** to map out relationships and resolve schema ambiguities. The visualization layer, built with **Streamlit**, connects directly to the processed DuckDB files to render KPIs and charts without latency.

---

### Example of Results

🚀 **Live Dashboard:** [https://nabilboutiyarzist-end-to-end-project.streamlit.app/](https://nabilboutiyarzist-end-to-end-project.streamlit.app/)

**Logical Data Model**
<img src="/assets/MLD.drawio.png" alt="Logical Data Model"> 

**Logical Data Lineage:**
<img src="/assets/lineage_graph.png" alt="DBT Lineage">

**Final Dashboard Interface:**
<img src="/assets/dashboard.png" alt="Streamlit Dashboard">