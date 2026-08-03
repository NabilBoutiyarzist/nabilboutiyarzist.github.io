---
title: From DBT Transformation to Streamlit Visualization
publishDate: 2025-12-01 00:00:00
img: /assets/dbt_streamlit.png
img_alt: From DBT Transformation to Streamlit Visualization
description: |
  Raw retail exports, no shared keys, no reliable KPIs. I built an end-to-end ELT pipeline with DBT and DuckDB into a Star Schema, visualized through an interactive Streamlit dashboard.
tags:
  - DBT
  - DuckDB
  - Streamlit
  - SQL
  - Data Engineering
---

🚀 **Live Dashboard:** [https://nabilboutiyarzist-end-to-end-project.streamlit.app/](https://nabilboutiyarzist-end-to-end-project.streamlit.app/)

### The Problem
Raw retail data rarely comes ready to analyze. Orders, products and stores lived in separate exports, didn't share consistent keys (e.g. `ARTEAN` vs `product_code`), and used inconsistent types. Before any KPI can be trusted, that mess has to be modeled properly. I built a complete ELT pipeline to turn disconnected retail exports into a single, reliable source for business KPIs.

<img src="/assets/dashboard.png" alt="Streamlit Dashboard">

### The Data
Tens of thousands of rows of structured, tabular retail data (order headers, order lines, products, stores), ingested and modeled entirely with SQL inside DuckDB.

### Why This Stack
- **DuckDB** instead of a full data warehouse: an in-process OLAP engine, zero infrastructure to manage, fast enough for this data volume. The right tool when you don't need a cluster.
- **DBT** to make the transformation logic testable, versioned and readable as SQL, instead of scattered ad-hoc scripts. Important once staging, intermediate and marts layers start depending on each other.
- **Streamlit** for the visualization layer: the fastest way to turn a Python/SQL backend into a shareable, interactive dashboard without building a separate frontend.

### How It's Built
Three DBT layers:
1. **Staging (Bronze):** raw ingestion, `TRY_CAST` type harmonization, column standardization.
2. **Intermediate (Silver):** join order headers with order lines to rebuild the full sales context, compute enriched metrics (gross revenue incl. VAT, tax amounts, order status).
3. **Marts (Gold):** Star Schema, a central `fact_sales` table surrounded by `dim_product`, `dim_store`, `dim_date`, built for fast analytical queries.

<img src="/assets/MLD.drawio.png" alt="Logical Data Model">
<img src="/assets/lineage_graph.png" alt="DBT Lineage">

### The Real Challenge
Inconsistent keys and naming across source files (`ARTEAN` vs `product_code`) meant the join logic couldn't be assumed. It had to be reverse-engineered from the data itself. I mapped the relationships in a Logical Data Model *before* writing a single DBT model, to avoid discovering schema conflicts halfway through the transformation layer.

### Result
A live Streamlit dashboard reading directly from the modeled DuckDB tables, no manual refresh, no spreadsheet juggling. Stakeholders can track Gross Revenue, VAT and Top Products in real time.

🚀 **Try it live:** [https://nabilboutiyarzist-end-to-end-project.streamlit.app/](https://nabilboutiyarzist-end-to-end-project.streamlit.app/)