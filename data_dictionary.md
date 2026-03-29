# 📖 Data Dictionary — Healthcare Financial Dataset

**File:** `healthcare_financial_data.xlsx`
**Rows:** 500 | **Columns:** 12 | **Years:** 2023–2024

---

## Column Reference

| Column | Data Type | Description | Example Values |
|--------|-----------|-------------|----------------|
| `Date` | String (Date) | Date of the healthcare transaction | `2023-08-20` |
| `Region` | Categorical | Geographic region of the hospital | East, West, North, South |
| `Department` | Categorical | Hospital department | Cardiology, Emergency, General Medicine, Oncology, Orthopedics, Pediatrics |
| `Treatment_Type` | Categorical | Type of medical treatment provided | Surgery, Diagnostics, Therapy, Consultation, Medication |
| `Number_of_Patients` | Integer | Number of patients for the record | 1 – 50 |
| `Treatment_Cost` | Float | Cost per patient for the treatment (in currency unit) | 106.67 – 4998.43 |
| `Total_Revenue` | Float | Total revenue generated from the record | Varies |
| `Expense` | Float | Total expense incurred for the record | Varies |
| `Profit` | Float | Net profit (Total Revenue - Expense) | 120.40 – 104,906.27 |
| `Year` | Integer | Year of the transaction | 2023, 2024 |
| `Currency` | Categorical | Currency of the transaction | USD, EUR, INR |
| `Payment_Method` | Categorical | Mode of payment used | Online Payment, Cash, Insurance |

---

## Categorical Values

### Region (4 unique)
- **East** — Eastern region hospitals
- **West** — Western region hospitals
- **North** — Northern region hospitals
- **South** — Southern region hospitals

### Department (6 unique)
- **Cardiology** — Heart-related treatments
- **Emergency** — Emergency care services
- **General Medicine** — General outpatient/inpatient care
- **Oncology** — Cancer treatment
- **Orthopedics** — Bone and joint treatments
- **Pediatrics** — Child healthcare

### Treatment Type (5 unique)
- **Surgery** — Surgical procedures
- **Diagnostics** — Tests and diagnostic procedures
- **Therapy** — Physical or medical therapy
- **Consultation** — Doctor consultations
- **Medication** — Prescription and medication services

### Currency (3 unique)
- **USD** — US Dollar
- **EUR** — Euro
- **INR** — Indian Rupee

### Payment Method (3 unique)
- **Online Payment** — Digital/online transactions
- **Cash** — Direct cash payments
- **Insurance** — Insurance-covered payments

---

## Derived / Calculated Fields (used in Tableau)

| Field | Formula | Description |
|-------|---------|-------------|
| `Profit Margin` | `Profit / Total_Revenue` | Profitability ratio per record |
| `Cost Efficiency` | `Expense / Number_of_Patients` | Average cost per patient |

---

## Data Quality Notes

- No null/missing values in any column
- `Date` stored as string — convert to datetime for time-series analysis
- `Currency` is mixed (USD, EUR, INR) — values are NOT normalized to a single currency
- `Profit` = `Total_Revenue` - `Expense` (verify: floating point rounding may cause minor differences)
