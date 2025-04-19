---
title: Salesforce Data Integration to Google Cloud Platform
publishDate: 2025-03-02 00:00:00
img: /assets/stock-1.png
img_alt: Salesforce Data Integration to Google Cloud Platform
description: |
  I integrated the Salesforce Data into the cloud, in order to build a visualization tool
tags:
  - Data Engineering 
  - Data Analysis
---

### Project Objective 

The goal of this project was to integrate Salesforce data into Google Cloud Platform in order to create a Power BI dashboard. This dashboard enables managers to engage with their teams using key performance indicators.  

### Technologies Used  
- **SQL** : Data extraction, transformation in BigQuery  
- **Python** : Backend application with Flask to handle API calls and process data  
- **Terraform** : Infrastructure as Code (IaC) for GCP resources  
- **DBT** : Data transformation and modeling in BigQuery  
- **GIT** : Version control for code and infrastructure  
- **GCP** : BigQuery, Cloud Storage, Cloud Functions, Cloud Run  
- **Docker** : Containerization for data processing and automation  

### Salesforce Configuration  
In order to use the Salesforce API, several configurations have been established. After these configurations were completed, I was able to obtain the necessary information to interact with the API. These elements were securely stored.  

### Backend Development with Flask
To interact with the API, I developed a Flask application that interacts with:  
- The **Salesforce API**  
- **Google Cloud Platform**  
- **Securely stored secrets**  

On Google Cloud Platform, an internal tool was used to streamline the management of GCP integrations.  

I implemented an **incremental data ingestion** process, ensuring that only new or updated records are retrieved. To achieve this, the application first fetches the stored data from BigQuery before querying Salesforce.  

Additionally, the application retrieves secrets via API calls.  

### Cloud Deployment on GCP 
On **Google Cloud Platform**, the following processes were implemented:  
- **Data retrieval**: Initiates the extraction of data.  
- **Flask application deployment**: Exposes the API for interaction.  
- **Incremental refresh management**: Sends the last refresh date to the API to ensure incremental updates.  

To manage the infrastructure, **Terraform** was used, with **Cloudcraft** facilitating the integration of Terraform code.  

For data transformation aligned with business needs, **dbt (Data Build Tool)** was utilized.  

Additionally, **Datadog** was implemented to monitor both API calls and GCP resources, ensuring system reliability.  

### Dashboard  
A **Power BI dashboard** was developed to provide visibility into key performance indicators, enabling better monitoring and decision-making.  
Using of **DAX, Power Query**  

### Architecture  
<img src="/assets/archi.png" alt="Architecture">


