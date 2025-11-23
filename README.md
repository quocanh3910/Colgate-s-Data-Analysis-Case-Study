# RBAC Project: Colgate Manufacturing Efficiency Case Study

## Project Overview
This project focuses on analyzing production line performance for Colgate's manufacturing operations. The primary goal is to calculate Overall Equipment Effectiveness (OEE), identify root causes of inefficiency, and quantify the business impact of downtime and defects.

By leveraging data cleaning, exploratory data analysis (EDA), and advanced time-series modeling (Vector Autoregression), this case study highlights systemic issues in maintenance and quality management and provides data-driven recommendations for operational excellence.

## 📂 Repository Structure
- **Dataset-cleaning-file.ipynb**: The data preprocessing pipeline. It handles missing values, merges disparate data sources (maintenance orders, production logs, cross-references), and feature engineers key metrics like "days since last maintenance".
- **Dataset-analysis-file.ipynb**: The core analytical engine. It calculates OEE, visualizes performance trends across shifts and machines, performs root cause analysis, and utilizes VAR modeling to forecast the impact of inefficiencies.

## Data Processing Pipeline
**File Reference:** <a href="https://github.com/quocanh3910/Colgate-s-Data-Analysis-Case-Study/blob/be5619951957286036e7618010e3842cc115ff5b/Dataset-cleaning-file.ipynb">Data Cleaning File</a>

The raw data consisted of three primary sources:
- **Maintenance Orders:** Equipment maintenance history (maintenance_order.csv).
- **Production Logs:** Daily operational logs including downtime, runtime, and defects (production_logs.csv).
- **Cross Reference:** Mapping between equipment IDs and operational names (cross_reference.csv).

**Key Cleaning Steps:**
- **Data Merging:** Integrated maintenance summaries and equipment metadata into the main production log using EQUIPMENT_ID and LINE_NAME.
- **Handling Missing Values:**
  - Hierarchical Mode Imputation for CO_TYPE and CREW_ID values.
  - Categorical Unknowns: AE_MODEL_CATEGORY and UTIL_REASON_DESCRIPTION labeled as "Unknown".
- **Feature Engineering:**
  - Calculated `avg_days_between_maintenance`.
  - Standardized date formats for time-series analysis.

## Analysis & Methodology
**File Reference:** <a href="https://github.com/quocanh3910/Colgate-s-Data-Analysis-Case-Study/blob/be5619951957286036e7618010e3842cc115ff5b/Dataset-analysis-file.ipynb">Data Analysis File</a>

1. **OEE Calculation**
   - Availability: (Run Time / Production Available Time)
   - Performance: (Ideal Cycle Time × Total Production / Run Time)
   - Quality: (Good Production / Total Production)
   - OEE Score: Availability × Performance × Quality

2. **Root Cause Analysis**
   - Shift Performance: Night-3 shift shows extreme downtime spikes (~50% in Feb–Mar).
   - Downtime Drivers: Planned Maintenance only 10–12% of total; unplanned dominates, mainly "02-Quality – 0202-Rework".

3. **Business Impact Modeling (VAR)**
   - **Granger Causality:** Downtime leads availability degradation.
   - **FEVD:** Downtime explains ~60% of availability variance; defect rate driven by downtime shocks.

## Key Findings
- **Systemic Reactive Culture:** High ratio of unplanned to planned maintenance.
- **The "Rework" Loop:** Quality rework is the top cause of downtime.
- **Performance Instability:** OEE fluctuates sharply (40%-70%), with a subtle downward trend indicating equipment deterioration.

## Recommendations
- **Shift to Predictive Maintenance:** Increase planned maintenance to reduce unexpected stops.
- **In-Process Quality Control:** Implement checks during production to reduce rework.
- **Target Night Shift Support:** Address operational gaps in Night-3 shift with training, resources, or on-call support.
