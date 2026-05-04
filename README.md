<div align="center">

# ⚡ 2023 Operations Analytics

**End-to-end data analysis of a Nigerian power generation company: cleaning, EDA, dashboard, and reporting across four generation units.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Tool: Power BI](https://img.shields.io/badge/Tool-Power%20BI-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com)
[![Status: Complete](https://img.shields.io/badge/Status-Complete-brightgreen)]()


</div>

---

## Overview

This project is a full analytics case study for a fictional Nigerian electricity generation company operating four units (Alpha, Beta, Delta, Gamma) across the 2023 fiscal year. The dataset was synthetically generated with deliberate data quality issues, mirroring real-world operational data problems in the Nigerian energy sector.

The analysis spans four data tables — daily generation logs, maintenance records, fuel purchases, and staff attendance — covering **1,081 generation records, 147 maintenance jobs, 59 fuel purchases, and 2,510 shift logs**.

> **Key result:** Unit Alpha and Unit Beta together account for 55.2% of ₦82.97B in total revenue, while Unit Beta's 1,402 hours of downtime and ₦27.42M maintenance spent on Unit Gamma represent the company's biggest operational risk heading into 2024.

---

## Business Problem

**Problem statement:** The company's operations generate large volumes of data across generation, maintenance, fuel procurement, and workforce management. However, the data is inconsistently recorded, and not yet used to drive decisions. This project aims to unify, clean, and analyse that data to surface actionable operational and financial insights.

**Objectives:**
- Identify which generation units are performing best by revenue, energy output, and efficiency
- Quantify the financial impact of downtime and maintenance backlog per unit
- Analyse fuel procurement patterns and flag payment risk
- Review workforce composition, shift distribution, and overtime prevalence
- Deliver a Power BI dashboard and report for stakeholder presentation

---

## Dataset

| Attribute | Details |
|-----------|---------|
| **Source** | Synthetically generated (fictional company) |
| **Domain** | Nigerian power generation |
| **Period** | January – December 2023 |
| **Tables** | 4 (Generation, Maintenance, Fuel, Staff) |
| **Total Records** | ~3,797 rows across all tables |
| **Currency** | Nigerian Naira (NGN / ₦) |

**Tables and key fields:**

| Table | Rows | Key Columns |
|-------|------|-------------|
| `Daily_Generation_Log` | 1,081 | `Unit_Name`, `Fuel_Type`, `Energy_Generated_MWh`, `Revenue_NGN`, `Downtime_Hrs` |
| `Maintenance_Log` | 147 | `Job_Type`, `Technician`, `Total_Cost_NGN`, `Status` |
| `Fuel_Purchase_Log` | 59 | `Supplier`, `Fuel_Type`, `Quantity_Litres`, `Payment_Status` |
| `Staff_Log` | 2,510 | `Employee_ID`, `Department`, `Hours_Worked`, `Monthly_Salary_NGN` |

**Data quality issues present in the raw dataset:**
- Headers occupy the first rows
- Duplicate Record IDs
- Mixed date formats (YYYY-MM-DD vs DD/MM/YYYY)
- MWh exceeds maximum MWh
- Multiple naming variants for 4 unit names (e.g. `Unit Beta`, `UNIT BETA`, `unit beta`, `Unit-Beta`)
- Multiple variants for 2 fuel types (e.g. `Natural Gas`, `GAS`, `Nat Gas`, `NG`)
- Multiple missing fuel used, labour cost, and revenue values
- Extreme revenue outliers (>₦100B on individual records)
- 1 occurence of impossible hours worked on maintenance
- Multiple variants for 4 maintenance status values
- Multiple occurence of fuel payment date > delivery date
- At least 1 negative fuel quantity record (-93,868 litres)
- Multiple variants for 4 fuel payment status values
- Multiple missing values for monthly Salary


---

## Methodology

```
Raw Data → Data Dictionary Review → Cleaning & Standardisation → EDA → Dashboard → Report
```


1. **Data Cleaning (Power Query)** — Standardised unit names and fuel types, converted date formats, handled missing values with median imputation, removed negative quantities and extreme outliers
2. **Exploratory Data Analysis — Aggregated revenue and energy by unit and month; built frequency distributions for maintenance job types and staff shift patterns
4. **Custom Columns (M Language)** — Created calculated columns including `Max_Possible_MWh`, `Energy_Generated_Remark`, and `Hours_Worked_Remark` using Power Query M formulas
5. **Dashboard (Power BI)** — Built an interactive Power BI report with KPI cards, bar/line charts, treemaps, and slicers


---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Power Query (M Language) | Data transformation  | Data cleaning |
| Power BI Desktop | Interactive dashboard and visual reporting |

---

## Visualization

- **Performance Analysis**

<img width="1062" height="308" alt="Image" src="https://github.com/user-attachments/assets/a6927737-5665-4c4f-b901-d91f30211daa" />

*Key Insights: Unit Alpha and Unit Beta account for 55.2% of total energy generated, reflecting higher capacity utilisation and better efficiency*
- *Despite Unit Beta recording the highest downtime (1,402 hrs), it maintains the second-highest efficiency rating. When running, Unit Beta operates at high performance.*
- *Unit Gamma’s combination of high downtime AND low efficiency makes it uniquely costly to the organisation.*

**Revenue Analysis**

<img width="836" height="458" alt="Image" src="https://github.com/user-attachments/assets/d94ef944-8f5e-4001-94c0-f8303dec48ed" />

*Key Insights*: 
*Peak Month: April 2023 (₦7.33B)   |  Low-revenue months: February & July (₦6.09B–₦6.43B)    | Average monthly revenue: ₦6.91 billion*

**Maintenance Analysis**

<img width="1031" height="475" alt="Image" src="https://github.com/user-attachments/assets/0c1125b2-a059-4157-b329-76708f3a92d6" />

*Key Insights: Unit Gamma’s 31.29% share of total maintenance spend is consistent with its downtime figure. Unit Alpha follows at 27.21% despite having the lowest downtime, suggesting intensive preventive maintenance activity.*
- *The 13 Emergency Repair events represent reactive maintenance triggered by unexpected failures. These are typically the most disruptive job type, and reducing their frequency is a key lever for lowering total maintenance cost.*
- *61.22% of all maintenance jobs were not completed by year end. The 17 Deferred jobs carry the highest risk — deferred maintenance directly increases the probability of unplanned equipment failure and major cost events in 2024.*
- *Four of the five most expensive maintenance jobs exceeded ₦10 million.*

**Staff & Shift Analysis**

<img width="833" height="464" alt="Image" src="https://github.com/user-attachments/assets/ba5b5d18-56de-4e5b-8e77-f6b6c989560f" />

*Key Insights: Operations is the largest department at 50.32% of headcount, followed closely by maintenance at 39.36%. HSE department is significantly under-resourced with only 1 staff member for a heavy industrial operation managing four generation units.*
- *Of the 2,510 shift records in the Staff Attendance Log, 2,213 (88.17%) involved hours worked in excess of 8 hours. This near-universal overtime rate strongly signals that the current headcount is insufficient for the operational demands of running four generation units year-round.*
- *The top 5 overtime earners each logged over 215 overtime shift events in a single year — approximately 60% of all working days. This level of overtime is unsustainable and carries serious risks including fatigue-related operational errors, burnout, and potential violations of Nigerian labour regulations.*

**Fuel Purchase Analysis**

<img width="838" height="470" alt="Image" src="https://github.com/user-attachments/assets/f02ac2e0-a0ca-4866-b47b-bebabb6054c9" />

*Key Insights: Diesel accounts for the majority of fuel spend (58.37%), despite Natural Gas delivering superior energy output per unit of fuel.*
- *Forte Oil Ltd and Ardova Petroleum are the largest suppliers by spend, each recording 17 purchases and together representing over ₦850 million in fuel spend.*
- *64.41% of fuel purchases (38 of 59) are either Overdue or Pending. This represents a significant cash flow risk and could jeopardise supplier credit terms and continuity of fuel supply if not urgently addressed.

---

 
## Key Findings & Insights

- **Unit Alpha and Unit Beta Dominate Revenue and Output**: Unit Alpha (₦23.02B, 27.74%) and Unit Beta (₦22.57B, 27.2%) together contribute 54.95% of total company revenue and 55.35% of total energy generated. This concentration is driven by higher capacity utilisation and superior generation efficiency. Any significant disruption to either unit would have an outsized negative impact on company revenue.
- **Efficiency gap**: Unit Delta is the most efficient generator at active hour. This makes it the optimal unit for dispatch prioritisation.
- **Unit Gamma is the Primary Operational Risk Asset**: Unit Gamma recorded the second-highest downtime (1,401 hrs) and the highest maintenance expenditure (₦27.42M). This dual impact on availability and cost makes it the single highest-risk asset in the generation portfolio. 
- **Supplier Exposure** : Forte Oil Ltd (₦473.24M) and Ardova Petroleum (₦395.98M) are the most exposed suppliers.
- **Fuel payment backlog is a Critical Cash Flow Risk** : 64.41% of fuel purchases are either Overdue (33.9%) or Pending (30.51%). If unresolved, this backlog risks supplier credit restrictions, interrupted fuel deliveries, and potential operational disruption.
- **Maintenance incompletion** : Only 38.78% of 147 maintenance jobs were completed in 2023. 37 remain Pending and 17 are Deferred — a backlog that threatens plant reliability heading into 2024.
- **Workforce strain** : 88.17% of all shift log records involve overtime hours (>8 hrs worked), and the top 5 employees each recorded 220–241 overtime events. With only 10 staff covering 2,510 shift records, the company is operating at near-maximum labour capacity.
- **Seasonal revenue** — Revenue is relatively stable throughout the year, peaking in April 2023 (₦7.33B) and dipping in February (₦6.09B).
- **Data Quality Issues Undermine Reporting Reliability** : The raw dataset contained multiple variants for values, mixed date formats, missing values, and negative values. Without data entry controls, these issues will persist.


---

## Strategic Recommendations

- **Initiate a Unit Gamma Reliability Improvement Programme**: Commission a formal reliability audit to identify root causes of Unit Gamma’s 1,401-hour downtime and ₦27.42M maintenance spend.
- **Resolve the Fuel Payment Backlog Within 60 Days**: Establish an urgent payment reconciliation process prioritising Forte Oil Ltd and Ardova Petroleum (combined exposure: ₦869M). Negotiate structured repayment schedules for overdue balances and create a dedicated fuel payment reserve fund to prevent recurrence. Review payment approval workflows to remove delays.
- **Clear the Maintenance Job Backlog Before End of Q2 2024**: Develop a structured clearance plan targeting all 37 Pending and 17 Deferred jobs. Assign technician teams per unit with weekly tracking. Consider engaging third-party maintenance contractors to supplement internal capacity.
- **Expand Workforce and Restructure Shift Schedules**: The current 10-person workforce is insufficient — 88.17% of shifts involve overtime, with some employees recording 220+ overtime events annually. Hire a minimum of additional 5 technicians and staff members across all departments. Restructure shift schedules to reduce individual overtime exposure and ensure compliance with labour regulations.
- **Implement Data Governance and Entry Validation Controls**: The volume of data quality issues found in FY 2023 indicates an absence of data entry standards. Deploy dropdown-controlled entry forms to enforce valid unit names, fuel types, and status values at source. Enforce ISO 8601 date formats. Assign a data steward role within Operations to monitor data quality monthly.



---

## License

Distributed under the **MIT License**. See [`LICENSE`](LICENSE) for details.

---

## Contact

**Al-ameen** — [LinkedIn](https://www.linkedin.com/in/al-ameen-lamina/) — laminaalameen2022@gmail.com

Portfolio: [wtech122.github.io](https://wtech122.github.io/) · GitHub: [@Wtech122](https://github.com/Wtech122?tab=)

