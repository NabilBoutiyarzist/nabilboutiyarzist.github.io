---
title: Automated File Control, Integrated into Google Sheets
publishDate: 2028-10-02 00:00:00
img: /assets/stock-4.png
img_alt: Soft pink and baby blue water ripples together in a subtle texture.
description: |
  I developed an automated file control, directly integrated into Google Sheets, to facilitate the integration into Salesforce.
tags:
  - Python
  - Pandas
  - Data 
---

### Project Overview & Objectives 

The goal of this project was to facilitate the integration of Google Sheets files into Salesforce. To import an `.xlsx` file into Salesforce, it must comply with the format specified by Salesforce objects. However, the files we needed to integrate contained many formatting errors, and we had hundreds of files to process.

The integration partner responsible for Salesforce configuration spent approximately **five hours per file** correcting errors before importing them.

The objective was to identify **errors in each file** to help users correct them more easily. **Automatic correction was not possible**, as some values were missing and could not be guessed. To address this issue, I developed a script that generates a **report listing all detected errors**. These reports were **directly integrated into Google Sheets**. 

---

### Technologies Used  
- **Python** (Pandas for data processing, FPDF for PDF generation)  
- **Google Cloud Platform (GCP)** (Cloud Run for deployment)  
- **Docker** (Containerization of the application)  
- **Flask API** (To handle file processing)  
- **Google Apps Script** (To integrate the solution into Google Sheets)  

---

### How It Works  

The **control script** was built in Python using **Pandas** for data validation and **FPDF** to generate reports in PDF format. To ensure **scalability and maintainability**, the script was developed using **Object-Oriented Programming** principles.  

The application was then **containerized with Docker** and deployed on **Google Cloud Platform using Cloud Run**.  

Additionally, I integrated **Google Apps Script** into each Google Sheets file to:  
1. **Create a button** that allows users to launch the file validation process.  
2. **Export the Google Sheet as an `.xlsx` file**.  
3. **Send the exported file to the endpoint created on Cloud Run**.  
4. **Receive the generated report** and display a **popup** with a link to the report (which is stored in the user’s Google Drive root folder).  

---

### Example of Results  
<img src="/assets/controlling_file.gif" alt="Architecture">


