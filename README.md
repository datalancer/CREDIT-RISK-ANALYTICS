# 💳 Credit Risk & Default Analytics Dashboard (Power BI)

An end-to-end credit risk intelligence solution built in **Power BI** using the **UCI Default of Credit Card Clients** dataset (`N = 30,000`). Designed on a custom **1920 × 1080** executive canvas, this two-page interactive report uncovers demographic default patterns, tracks 6-month delinquency escalation, and isolates high-risk borrower segments using custom DAX risk scoring and AI root-cause decomposition.

---

## 📸 Dashboard Preview

## 📂 Repository Files

| File | Format | Description |
| :--- | :---: | :--- |
| **`Project Credit Risk Analytics Dashboard.pbix`** | Power BI (`.pbix`) | Interactive 2-page report with Power Query ETL, Star Schema, DAX measures, and AI Decomposition Tree |
| **`Project Credit Risk Analytics Dashboard.pdf`** | Static Report (`.pdf`) | High-resolution exported executive report for quick viewing without Power BI Desktop |
| **`Project Credit Risk Analytics Dashboard.mp4`** | Video Demo (`.mp4`) | Guided walkthrough demonstrating slicer filtering, bookmark reset, and root-cause drilldowns |

## 🚀 to Explore This Project
1. **Quick Preview (No Software Required):** Watch the inline video walkthrough above or open the **`.pdf`** export directly in GitHub to review both dashboard pages.
2. **Interactive Exploration in Power BI Desktop:**
   ```bash
   git clone [https://github.com/datalancer/CREDIT-RISK-ANALYTICS.git](https://github.com/datalancer/CREDIT-RISK-ANALYTICS.git)




---

## 🎯 Business Problem & Objectives
Financial institutions face significant capital erosion when revolving credit balances transition into delinquency. The goal of this project is to transform raw, wide-format monthly billing and repayment logs (April–September 2005) into an actionable risk-monitoring system that answers:
1. **Portfolio Exposure:** What is our baseline default rate, credit exposure, and repayment velocity across 30,000 cardholders?
2. **Borrower Profiling:** How do credit limits, age, education, gender, and marital status correlate with default probability?
3. **Early Warning Signals:** How rapidly does delinquency escalate across risk tiers over a 6-month window?
4. **Root-Cause Segmentation:** Which intersecting borrower attributes account for the highest concentration of defaults?

---

## 📊 Key Portfolio KPIs & Analytical Insights

| Metric | Value | Business Takeaway |
| :--- | :---: | :--- |
| **Total Customers** | **30,000** | Full Taiwan credit card portfolio analyzed across 6 billing cycles |
| **Default Customers** | **6,636** | Total accounts entering default status |
| **Portfolio Default Rate** | **22.12%** | Baseline risk benchmark used for conditional heatmap thresholds |
| **Average Credit Limit** | **167.48K** | Mean approved credit line (NT$) |
| **Average Bill Amount** | **44.98K** | Monthly billed balance trending upward from Apr to Sep 2005 |
| **Average Payment Amount** | **5.28K** | ~11.7% payment-to-bill ratio, signaling rising revolving debt |

### 🔍 Core Risk Findings
* **High-Risk Concentration:** Out of **6,636** total defaulters, **3,880 (58.5%)** belong to the **High Risk** tier, where default rates exceed **45%** across both female (`45.23%`) and male (`47.65%`) borrowers.
* **Delinquency Escalation (Apr–Sep 2005):** Portfolio-wide monthly delinquency more than doubles from **~10% in April/May 2005** to **>22% in September 2005**, driven by High Risk delinquency climbing past **60%** while average statement balances outpace monthly repayments.
* **Credit Limit Inverse Correlation:** Borrowers in the **Low (`≤50K`)** credit band experience the highest default rate (**>30%**), whereas **Premium (`>300K`)** cardholders show the lowest default incidence.
* **Demographic & AI Root-Cause Drivers:** High School (`25.16%`) and University (`23.73%`) segments exhibit higher default rates than Graduate School (`19.23%`). The AI Decomposition Tree isolates **`High Risk` → `Female` → `University`** as the single largest volume cluster of defaults (`1,133` accounts).

---

## 🗂️ Data Modeling & ETL Architecture

Rather than reporting directly off a flat 25-column table, the dataset was normalized in **Power Query** into a clean **Star Schema**:

1. **`Customers` (Dimension Table — 30,000 rows)**
   * Cleaned categorical labels (`Gender`, `Education`, `Marital Status`).
   * Engineered custom demographic and financial bands (`Age Group`, `Credit Limit Band`) with dedicated sort-order columns.
   * Created behavioral risk tiers (`Low Risk`, `Medium Risk`, `High Risk`) derived from maximum repayment delay and credit utilization.
2. **`Monthly_History` (Fact Table — 180,000 rows)**
   * Unpivoted 6 months of wide billing (`BILL_AMT1`–`6`), payment (`PAY_AMT1`–`6`), and repayment status (`PAY_0`–`6`) columns into a normalized longitudinal table (`Apr 2005`–`Sep 2005`).
   * Linked to `Customers` via a **One-to-Many (`1:*`)** single-direction relationship on `Customer_ID`.

---

## 🧮 Featured DAX Measures

```dax
// Portfolio Default Rate
Default Rate = 
DIVIDE([Default Customers], [Total Customers], 0)

// Longitudinal Monthly Delinquency Rate
Monthly Delinquency Rate = 
DIVIDE(
    CALCULATE(COUNTROWS('Monthly_History'), 'Monthly_History'[Repayment_Status] > 0),
    COUNTROWS('Monthly_History'),
    0
)

// Average Statement Bill & Payment Velocity
Average Bill Amount = AVERAGE('Monthly_History'[Bill_Amount])
Average Payment Amount = AVERAGE('Monthly_History'[Payment_Amount])
