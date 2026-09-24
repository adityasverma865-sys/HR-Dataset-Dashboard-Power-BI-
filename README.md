# HR People Analytics Dashboard (Power BI)

An end-to-end **HR analytics solution in Power BI** built on a 100,000-employee dataset. The report covers workforce composition, attrition and retention, compensation and pay equity, performance and wellbeing, flight-risk scoring, HR alerting, and what-if scenario planning across **13 report pages**.

![Executive Overview](Executive%20Overview.png)

---

## Highlights

| Metric | Value |
|---|---|
| Total employees | 100,000 |
| Active / Resigned | 89,990 / 10,010 |
| Attrition rate | 10.01% |
| Average tenure | 4.48 years |
| Average monthly salary | 6.40K |
| Total compensation cost | 640M |
| Employees at high flight risk | 15,491 (17% of workforce) |
| Hiring window covered | 2014 - 2024 |

---

## Report Pages

| # | Page | What it answers |
|---|---|---|
| 1 | **Executive Overview** | Headcount, attrition, retention, tenure, overall workforce alert |
| 2 | **Attrition & Retention Deep-Dive** | Which departments lose the most people? Pareto-style attrition concentration and outlier detection |
| 3 | **Segmentation** | Attrition by job title, education level and generation; key-role concentration risk |
| 4 | **Compensation & Pay Equity** | Salary by department, job title, education; salary bands vs. median |
| 5 | **Performance & Wellbeing** | Performance and satisfaction tiers, overtime vs. satisfaction by department |
| 6 | **Career Growth, Training & Work Style** | Promotions, training hours, projects handled, remote work; slicers for tenure and gender |
| 7 | **Flight Risk & Retention Priority** | Employee-level flight-risk score and segments, high-value retention priority list |
| 8 | **HR Alerts & Escalation Center** | Severity-based alerts, dynamic thresholds per department, breach detection |
| 9 | **Scenario Planning (What-If)** | Simulate compensation increase % and headcount change % with worst / expected / best cases |
| 10 | **Dynamic KPI Explorer** | Switch between KPIs using a field-parameter selector |
| 11 | **Workforce Demographics & Composition** | Gender, generation, education, technical vs. non-technical, department category |
| 12 | **Hiring Trends & Seasonality** | New hires by month, season, quarter and year |
| 13 | **Data Quality, Model Info & Admin** | Row counts, model health score, version and ownership |

<details>
<summary><b>Click to view all page screenshots</b></summary>

### Attrition & Retention Deep-Dive
![Attrition](Attrition%20%26%20Retention%20Deep%20Dive.png)

### Segmentation
![Segmentation](Segmentaion-%20Job%2CTitle%2CGeneration.png)

### Compensation & Pay Equity
![Compensation](Compensation%20%26%20Pay%20Equity.png)

### Performance & Wellbeing
![Performance](Performance%20%26%20Wellbeing.png)

### Career Growth, Training & Work Style
![Career](Carrier%20Growth%20Training%20%26%20Work%20Style.png)

### Flight Risk & Retention Priority
![Flight Risk](Flight%20Risk%20%26%20Retintion%20Priority.png)

### HR Alerts & Escalation Center
![Alerts](HR%20Alerts%20%26%20Escalations.png)

### Scenario Planning (What-If)
![Scenario](Sceario%20Planning%20%28What%20IF%29.png)

### Dynamic KPI Explorer
![KPI Explorer](Dynamic%20KPI%20Explorer.png)

### Workforce Demographics & Composition
![Demographics](Workforce%20Demographics%20%26%20Composition.png)

### Hiring Trends & Seasonality
![Hiring](Hiring%20Trend%20And%20Seasonality.png)

### Data Quality, Model Info & Admin
![Admin](Data%20Quality%20and%20Admin%20Info.png)

</details>

---

## Data Model

The model follows a **star schema** with a central fact table and dimension tables for department, employee, job title, education and date.

![Data Model](Data%20Modeling.png)

**Fact table**
- `Fact_Employee`: employee-level metrics and calculated columns (flight risk score, flight risk segment, high-value retention priority)

**Dimensions**
- `Dim_Department` (department, department category)
- `Dim_employee` (employee ID, age, gender)
- `Dim_Job_Title` (job title, is technical role)
- `Dim_Education` (education, education rank)
- `Dim_Date` (date, hire season, month, quarter)

**Supporting tables**
- Calculation groups (3)
- What-if parameter tables: `Compensation Increase %`, `Headcount Change %`
- Field parameter: `Key People Metrics`

---

## Key Features

- **Star schema** data model with one-to-many relationships
- **Calculation groups** for reusable time-intelligence and measure logic
- **Field parameters** for a dynamic KPI selector
- **What-if parameters** for compensation and headcount scenarios
- **Flight-risk scoring** with segments (Low / Moderate / Elevated / High) and a high-value retention priority flag
- **Dynamic thresholds and outlier detection** (1.5 sigma) on department attrition
- **Alerting logic** with severity, priority score and breach status
- **Dynamic narrative text** measures (for example, the flight-risk snapshot)
- **Pareto / cumulative attrition contribution** classification (A / B / C)
- **Generation and tenure bucket** segmentation

---

## Dataset

**File:** `Extended_Employee_Performance_and_Productivity_Data.csv`
**Size:** 100,000 rows x 22 columns (about 10 MB)

| Category | Columns |
|---|---|
| Identity / demographics | Employee_ID, Gender, Age, Education_Level |
| Job | Department, Job_Title, Level, Dept Code, Hire_Date, Years_At_Company |
| Performance | Performance_Score, Projects_Handled, Promotions, Training_Hours |
| Workload | Work_Hours_Per_Week, Overtime_Hours, Remote_Work_Frequency, Team_Size |
| Wellbeing | Sick_Days, Employee_Satisfaction_Score |
| Compensation | Monthly_Salary |
| Outcome | Resigned |

### Data Notes
- `Hire_Date` appears malformed in the raw CSV (values like `03:05.6`, a spreadsheet time-format artifact). It was corrected during data preparation in Power BI, which is why hiring trends from 2014 to 2024 render correctly in the report.
- `Dept Code` has about 11,000 blank values in the raw file. The report uses the `Department` column for all department analysis.
- The dataset appears to be **synthetic**, so many splits (for example, attrition by department) look nearly uniform. Insights should be read as a demonstration of the analytical framework rather than real-world findings.

---

## How to Use

1. Clone the repo:
   ```bash
   git clone https://github.com/<your-username>/hr-people-analytics-powerbi.git
   ```
2. Open `HR_People_Analytics.pbix` in **Power BI Desktop** (June 2025 release or later recommended, for calculation groups and field parameters).
3. If Power BI asks for the data source path, go to **Home > Transform data > Data source settings** and point it to `Extended_Employee_Performance_and_Productivity_Data.csv`.
4. Refresh and explore.

---

## Repository Structure

```
hr-people-analytics-powerbi/
├── README.md
├── HR_People_Analytics.pbix
├── Extended_Employee_Performance_and_Productivity_Data.csv
└── *.png   (data model + 13 report page screenshots)
```

---

## Tools & Skills

`Power BI` · `DAX` · `Power Query` · `Data Modeling (Star Schema)` · `Calculation Groups` · `Field Parameters` · `What-If Analysis` · `HR Analytics`

---

## Author

**Aditya S Verma**
Model v1.0, built 23-Jul-2026

[LinkedIn](#) · [GitHub](#)
