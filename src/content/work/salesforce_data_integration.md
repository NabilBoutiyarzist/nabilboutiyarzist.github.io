---
title: Salesforce Data Integration to Google Cloud Platform
publishDate: 2026-01-01 00:00:00
img: /assets/stock-1.png
img_alt: Salesforce Data Integration to Google Cloud Platform
description: |
  Managers needed real-time KPIs, but Salesforce data required manual exports to reach BI tools. I built an automated pipeline into Google Cloud Platform to feed a live Power BI dashboard.
tags:
  - Data Engineering 
  - Data Analysis
---

### The Problem
Managers needed real-time visibility on their team's KPIs, but the source of truth (Salesforce) wasn't accessible for BI without manual exports. I built a pipeline to sync Salesforce data into Google Cloud Platform automatically, so KPIs stay current without anyone touching a spreadsheet.

Here's the exposition architecture: how data flows from Salesforce to BigQuery, then out to Power BI.

<img src="/assets/archi.png" alt="Data exposure architecture: Salesforce to GCP (BigQuery) to Power BI">

### The Data
Salesforce CRM records, synced **every morning**, **tens of thousands of rows per run**, through an incremental ingestion process: the app checks what's already stored in BigQuery before querying Salesforce again, so only new or updated records are pulled.

### Why This Stack
- **Flask** as a thin API layer between Salesforce, GCP and secret storage. Enough for an orchestrated data sync, no need for a heavier framework.
- **BigQuery** as the analytical store: serverless, scales with data volume, plugs directly into Power BI.
- **DBT** to model raw Salesforce exports into business-ready tables. Same logic as any ELT project: keep transformation logic versioned and testable instead of buried in application code.
- **Terraform** to provision GCP resources as code, so the infrastructure is reproducible and reviewable like any other code change.
- **Docker** to containerize the processing and automation jobs. A consistent environment between local development and Cloud Run.
- **Datadog** to monitor API calls and GCP resources. Once data feeds a decision-making dashboard, a silent failure is the real risk.

### The Real Challenge
The trickiest part wasn't the extraction itself, it was making the refresh **incremental without missing or duplicating records**. The application uses the last successful refresh date as a checkpoint and checks BigQuery before querying Salesforce again, instead of re-pulling the entire dataset on every run.

### Result
A Power BI dashboard (DAX + Power Query) gives managers real-time visibility on their team's KPIs, fed by an automated pipeline instead of manual exports. [À COMPLÉTER : métrique concrète, ex. gain de temps vs. process manuel, nombre d'utilisateurs actifs du dashboard, ou volume de données synchronisé]


