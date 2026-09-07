# 🏥 Healthcare Financial Performance Review

An interactive, currency-normalized **Tableau dashboard** paired with a **Python data pipeline** to analyze healthcare financial performance, department efficiency, and regional profitability.

🔗 **Live Interactive Dashboard:** [View on Tableau Public](https://public.tableau.com/app/profile/ayushi.dhimmar/viz/Healthcare_Financial_Performance_Review_dashboard/HealthcareFinancialPerformanceReview)

---

## 📋 Executive Summary

### 1. Project Objective & Business Case

Healthcare organizations operate on tight margins where operational costs must be balanced against clinical delivery. The objective of this project is to build an interactive dashboard for hospital administrators and financial stakeholders (CFO, Clinical Directors) to:

- Monitor overall revenue, expenses, and profit margins.
- Analyze departmental cost-efficiency to identify margin leakage.
- Identify high-volume treatment categories and payment methods to improve billing workflows.
- Pinpoint underperforming regions to optimize marketing and resource allocation.

### 2. The Business Problem

In the raw financial dataset, transactions occurred in mixed currencies (**USD, EUR, and INR**) due to cross-border billing operations. Direct summation of the raw database columns led to a **critical logic error** (reporting ₹33.0M total revenue by adding 1 USD + 1 EUR + 1 INR directly).

To solve this and ensure a consistent base of comparison, all financial values were normalized to Indian Rupee (₹) using fixed reference exchange rates (1 USD = ₹83, 1 EUR = ₹90) to enable consistent financial analysis and comparison across all records.

---

## 🛠️ Tools & Technologies Used

- **Python (pandas, numpy)** — Data ingestion, cleaning, and currency normalization pipeline.
- **Jupyter Notebooks** — Exploratory Data Analysis (EDA) and pipeline testing.
- **Tableau Desktop Public Edition** — Interactive dashboard design and calculated field implementation.
- **Tableau Public Cloud** — Hosting and deployment.
- **Microsoft Excel** — Raw data source storage.

---

## 📊 Dashboard KPIs & Visualizations

The corrected dashboard displays the following validated financial metrics:

| Metric             | Corrected Value (INR) | Calculation / Source Field               |
| ------------------ | --------------------- | ---------------------------------------- |
| **Total Revenue**  | ₹ 1,886.2M            | `Sum(Total_Revenue)` (Normalized to INR) |
| **Total Expense**  | ₹ 1,314.3M            | `Sum(Expense)` (Normalized to INR)       |
| **Total Profit**   | ₹ 571.9M              | `Revenue - Expense`                      |
| **Profit Margin**  | 30.32%                | `Total Profit / Total Revenue`           |
| **Total Patients** | 12,851                | `Sum(Number_of_Patients)`                |

### Visuals Breakdown

1. **Regional Revenue Analysis (Side-by-Side Bar Chart):** Compares Expense (Blue) vs. Revenue (Green) across East, South, North, and West regions.
2. **Department Cost Efficiency (Heatmap Matrix):** Plots Region vs. Department to identify average expense per patient (cost efficiency = `Expense / Number_of_Patients`).
3. **Profit Trend Analysis (Line Chart):** Illustrates profit margin fluctuations and consistency across 2023–2024.
4. **Patient Mix by Treatment (Horizontal Bar Chart):** Shows patient distributions across Surgery, Medication, Therapy, Consultation, and Diagnostics.
5. **Interactive Slicers:** Dynamically filters the entire dashboard by _Treatment Type_, _Region_, and _Department_.

---

## 📁 Repository Structure

```
healthcare-financial-dashboard/
│
├── data/
│   ├── healthcare_financial_data.xlsx      # Original raw multi-currency data source
│   ├── healthcare_cleaned.csv             # Cleaned dataset (mixed currencies maintained)
│   └── healthcare_normalized.csv          # Final normalized dataset (INR base currency)
│
├── notebooks/
│   ├── 01_data_cleaning.ipynb             # Python cleaning & currency normalization pipeline
│   └── 02_eda.ipynb                       # Exploratory Data Analysis and statistical reports
│
├── dashboard/
│   └── Healthcare_Financial_Performance_Review_dashboard.twbx # Tableau packaged workbook
│
├── docs/
│   ├── data_dictionary.md                 # Column schemas and data quality notes
│   └── insights.md                        # Business insights and strategic recommendations
│
├── screenshots/
│   ├── dashboard_overview.png             # Dashboard layout overview
│   ├── kpi_summary.png                    # KPI metrics breakdown
│   ├── regional_analysis.png              # Revenue vs Expense by region
│   ├── department_analysis.png            # Heatmap of department cost-efficiency
│   └── interactive_filters.png            # Dynamic filtering controls
│
└── README.md
```

---

## ⚙️ Data Pipeline & Normalization Workflow

The ingestion, normalization, and visualization pipeline is structured as follows:

```
      Raw Excel
          ↓
   Python (Pandas)
          ↓
Currency Normalization
          ↓
    Data Cleaning
          ↓
  Tableau Dashboard
```

### In-Place Transformations (Calculated Fields)

- **Profit Margin (Tableau Calculated Field):** `[Profit] / [Total Revenue]`
- **Cost Efficiency (Tableau Calculated Field):** `[Expense] / [Number of Patients]`

The transparent data cleaning steps are documented in `notebooks/01_data_cleaning.ipynb`.

---

## 🔑 Key Business Insights & Actionable Recommendations

### Top Findings

- **East Region Leads Revenue:** After currency normalization, East actually generated the highest revenue (**₹ 513.5M**), followed closely by South (**₹ 504.7M**). West represents the lowest performing region (**₹ 416.9M**).
- **Orthopedics is Most Profitable:** **Orthopedics** drives the highest profit margin at **32.47%** (₹ 288.7M revenue), while **Emergency** has the lowest margin at **27.83%** due to operational overhead.
- **Negative Growth Trend:** YoY revenue declined by **-3.45%** (dropping from ₹ 959.7M in 2023 to ₹ 926.6M in 2024), highlighting potential patient leakage or shift to low-cost diagnostics.

### Strategic Recommendations

1. **Cost Containment in Emergency:** Implement resource-optimization protocols in Emergency and Cardiology to bring their profit margins closer to the 30% baseline.
2. **Expansion Campaigns in West & North:** West represents a major underperforming market; launching regional clinical partnerships can capture local demand.
3. **Insurance Transition:** Standardize billing integrations to increase the share of insurance-based transactions (currently lowest at 29.4%), decreasing cash flow risk.

---

## ⚠️ Challenges & Future Enhancements

- **The Currency Challenge:** The raw database mixed USD, EUR, and INR without conversion. Directly aggregating these values created major inaccuracies. Applying a Python pandas preprocessing step solved this.
- **Tableau Rendering Bug (Layout):** On Tableau Public, container text boxes can render values as `###` if not scaled correctly. KPI cards were adjusted to fit variable resolutions.
- **Future Work:**
  - Connect the pipeline to a live PostgreSQL/SQL Server database for automated, daily dashboard refreshes.
  - Implement time-series forecasting (ARIMA/Prophet) to predict monthly revenue trends and clinical demand.

---

## 🚀 How to Run and Reproduce

1. **Requirements:** Install Python 3.x and libraries (`pandas`, `numpy`, `openpyxl`).
2. **Pipeline Execution:** Re-run the data cleaning script to export the normalized dataset:
   ```bash
   jupyter nbconvert --to notebook --execute notebooks/01_data_cleaning.ipynb
   ```
3. **Tableau Update:** Open the packaged workbook in Tableau Desktop, refresh the connection to `data/healthcare_normalized.csv`, and publish to Tableau Public.
