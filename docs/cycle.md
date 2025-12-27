
# Daily Reporting Cycle (End-to-End)

## Goal
Deliver a refreshed daily dashboard and daily report package with consistent KPIs and clean data.

---

## Job 1 — Prepare Daily Reporting Folder
**Purpose:** Create a new daily folder based on the most recent available date.  
**Inputs:** Yesterday’s folder structure and report templates.  
**Process:** 
- Create new day folder
- Copy previous day’s reports
- Rename files to match the new date
**Outputs:** New daily folder ready for data refresh.

---

## Job 2 — Collect & Transform Leads (Voluntary / Fresh)
**Purpose:** Prepare clean lead dataset for analytics and DB loading.  
**Inputs:** Raw leads file(s).  
**Process:**
- Standardize column names
- Clean text fields and remove noise
- Validate phone formats and required fields
- Deduplicate contacts inside each lead
- Flag callable vs non-callable leads
**Outputs:** Clean leads dataset.

---

## Job 3 — Extract Calls Feedback (Portal / Dialer / Genesys)
**Purpose:** Collect interaction/call results for the previous day.  
**Inputs:** System exports (portal feedback, dialer attempts, call results).  
**Process:**
- Export/download daily files
- Normalize different formats
- Filter records for “yesterday”
- Standardize dispositions and key fields
**Outputs:** Clean feedback datasets.

---

## Job 4 — Load Feedback into SQL Database
**Purpose:** Centralize feedback data for reporting.  
**Inputs:** Clean feedback datasets (Job 3).  
**Process:**
- Insert into DB tables (e.g., Portal_Data, Genesys_Data)
- Validate schema alignment
- Log insertion results
**Outputs:** Updated DB with latest feedback.

---

## Job 5 — Load Leads into SQL Database + Data Quality Rules
**Purpose:** Store new leads with quality flags and dedup rules.  
**Inputs:** Clean leads dataset (Job 2).  
**Process:**
- Insert leads table + contact table
- Deduplicate vs previous lead sets (historical checks)
- Mark DNC / invalid numbers
- Run cleansing/dedup procedure (if used internally)
**Outputs:** Updated DB with fresh leads and quality flags.

---

## Job 6 — Extract KPI Outputs from DB
**Purpose:** Produce CSV datasets for dashboards and re-upload lists.  
**Inputs:** SQL tables/views/functions/procedures.  
**Process:**
- Generate KPIs for the day (and month-to-date if needed)
- Export datasets as CSV
- Generate “Reupload Lists” (e.g., language barrier, alternative numbers, redial candidates)
**Outputs:** KPI CSVs + operational CSV outputs.

---

## Job 7 — Refresh Dashboards & Share Output Package
**Purpose:** Deliver final dashboards and daily report package to stakeholders.  
**Inputs:** Dashboard files + DB exports/CSVs.  
**Process:**
- Refresh Power Query / connections
- Recalculate measures
- Save final dashboards
- Copy final package to shared team folder
**Outputs:** Final dashboards and reports shared.

---

## Scheduling & Dependencies
Typical schedule: run once daily, depends on:
- Availability of system exports (Job 3)
- DB load completion (Jobs 4–5)
- KPI export completion (Job 6)
- Dashboard refresh last (Job 7)
