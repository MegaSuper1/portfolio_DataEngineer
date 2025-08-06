## 🧾 Legacy Report Automation and BI Modernization

**Company:** FedEx Supply Chain / Genco Logistics  
**Role:** BI Developer / Report Automation Specialist  
**Tools:** Microsoft Access, Excel VBA, QlikView, Windows Task Scheduler, Postman  
**Skills:** Process automation, legacy system migration, API integration, batch scripting, stakeholder collaboration, cost reduction

---

## 🔧 Project Overview

FedEx Supply Chain relied on manually generated Excel-based reports sourced from MercuryGate, consuming substantial time and resources. These processes required full-time associates to manually run and compile reports each week, introducing risk and inefficiency.

My responsibility was to design and implement a fully automated reporting system using Microsoft Access, VBA, and batch scripting, with long-term migration to QlikView for enterprise reporting.

---

## 📌 Responsibilities

- **Automated MercuryGate report generation** via batch scripting and REST API calls  
- **Integrated Microsoft Access and Excel** to build logic-driven data workflows and output formatted Excel reports  
- **Used VBA macros** to export, pivot, and visualize data within Excel automatically  
- **Implemented scheduled automation** via Windows Task Scheduler to eliminate manual involvement  
- **Collaborated with stakeholders** to gather requirements, prioritize use cases, and ensure compliance with operational KPIs  
- **Planned BI modernization strategy** for transitioning to QlikView and phasing out Excel-based legacy reporting  

---

## 💻 Sample Automation Code

### ✅ Batch File to Call MercuryGate API and Run Access Macro

```batch
@echo off
REM === Configuration ===
set "API_URL=https://api.mercurygate.net/rest/reports/export"
set "USERNAME=your_username"
set "PASSWORD=your_password"
set "REPORT_ID=your_report_id"
set "OUTPUT_FILE=C:\Reports\MercuryGate_Report.csv"
set "LOG_FILE=C:\Reports\MercuryGate_Automation.log"

echo Starting MercuryGate report automation at %DATE% %TIME% > "%LOG_FILE%"

curl -u "%USERNAME%:%PASSWORD%" ^
     -X GET "%API_URL%?reportId=%REPORT_ID%" ^
     -H "Accept: text/csv" ^
     -o "%OUTPUT_FILE%" >> "%LOG_FILE%" 2>&1

IF %ERRORLEVEL% NEQ 0 (
    echo Error: Failed to retrieve the report >> "%LOG_FILE%"
    exit /b 1
)

set "ACCESS_DB=C:\Path\ReportDatabases\MGReport.accdb"
set "MACRO_NAME=mcr_Run_MG_Report"
start "" "C:\Program Files (x86)\Microsoft Office\root\Office16\MSACCESS.EXE" "%ACCESS_DB%" /x "%MACRO_NAME%" >> "%LOG_FILE%" 2>&1
