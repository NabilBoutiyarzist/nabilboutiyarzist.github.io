---
title: Automated File Control, Integrated into Google Sheets
publishDate: 2025-01-02 00:00:00
img: /assets/stock-4.png
img_alt: Soft pink and baby blue water ripples together in a subtle texture.
description: |
  An integration partner spent hours fixing Excel files by hand before every Salesforce import. I built an automated control tool, directly inside Google Sheets, to catch formatting errors in seconds.
tags:
  - Python
  - Pandas
  - Data 
---

### The Problem
Before every Salesforce import, someone had to manually check each `.xlsx` file line by line. Missing fields, wrong formats, broken references: the integration partner spent **around five hours per file** fixing errors by hand, across hundreds of files. That doesn't scale.

Here's the solution in action, a button inside Google Sheets that triggers the check and returns a report in seconds:

<img src="/assets/controlling_file.gif" alt="Automated control in action: button in Google Sheets triggers validation and returns a report">

### The Data
Each file is a Google Sheet exported to `.xlsx`, expected to match a specific Salesforce object schema. Volume: hundreds of files, filled in manually by different people, so formatting drifted (missing values, wrong types, inconsistent columns). Automatic correction wasn't an option here: some missing values simply can't be guessed. So the focus shifted to **detection, not guessing**: surface every error clearly and let the person filling the sheet fix it themselves.

### Why This Stack
- **Python + Pandas** for the validation logic: the ruleset (required fields, formats, cross-references) maps naturally to DataFrame operations.
- **FPDF** to turn validation results into a readable PDF report instead of raw logs. End users aren't developers, so the output had to be self-explanatory.
- **Object-Oriented Programming** to keep the rule engine maintainable: adding a new check should be an isolated change, not a rewrite.
- **Docker + Cloud Run**: the validation logic runs as a stateless service, no server to maintain, scales to zero between usage spikes. A good match for a "one file, one request" usage pattern.
- **Google Apps Script** as the front door: instead of asking non-technical users to leave Google Sheets, I added a button directly inside the sheet they already use. Export `.xlsx`, send it to the Cloud Run endpoint, get a report link back in a popup.

### The Real Challenge
The hard part wasn't the validation logic. It was designing a workflow non-technical users would actually adopt. Forcing people to leave Google Sheets to check a file elsewhere would have killed adoption. Keeping everything to one click, inside the tool they already use, was the real product decision here.

### Result
The tool is in production use to check files before every Salesforce import, replacing manual line-by-line review. It has corrected hundreds of files, saving around **5 hours per file** and several thousand euros in integration-partner costs.


