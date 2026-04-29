# FinShield

## NST DVA Capstone 2 - Project Repository

> **Newton School of Technology | Data Visualization & Analytics**
> A 2-week industry simulation capstone using Python, GitHub, and Tableau to convert raw data into actionable business intelligence.


## Project Overview

| Field | Details |
|---|---|
| **Project Title** | _FinShield_ |
| **Sector** | _Finance_ |
| **Team ID** | _DVA-G1_ |
| **Section** | _D_ |
| **Faculty Mentor** | _Archit Raj Sir_ |
| **Institute** | Newton School of Technology |
| **Submission Date** | _29 April 2026_ |

### Team Members

| Role | Name | GitHub Username |
|---|---|---|
| Project Lead | _Daksh Batra_ | `dakshbatra01` |
| Data Lead | _Prakhar Rawat_ | `Prakhar13o3` |
| ETL Lead | _Nitin Kumar_ | `Nitin-0017` |
| Analysis Lead | _Isha Tomar_ | `Bytebard089` |
| Visualization Lead | _Kapish Rohilla_ | `kapish9741` |
| Strategy Lead | _Rishi Raj_ | `rishiraj38` |
| PPT and Quality Lead | _Nishant Ranjan Singh_ | `IAmNishantSingh` |

---

## Business Problem

Financial institutions face significant losses due to loan defaults and inefficient borrower screening. This project identifies the key financial and behavioral factors driving loan defaults and develops a data-driven risk segmentation framework to support more effective lending decisions and improved portfolio performance.

**Core Business Question**

> How can we identify high-risk borrowers before loan approval to minimize default rates and financial losses?

**Decision Supported**

> This analysis enables lenders to redesign their loan approval strategy by identifying which borrower profiles should be prioritised, restricted, or offered modified loan terms — replacing the traditional credit-score-first approach with a statistically validated LTV + DTI dual-band policy.

---

## Dataset

| Attribute | Details |
|---|---|
| **Source Name** | _Kaggle_ |
| **Direct Access Link** | _https://www.kaggle.com/datasets/yasserh/loan-default-dataset_ |
| **Row Count** | _15,000_ |
| **Column Count** | _34_ |
| **Time Period Covered** | _2019_ |
| **Format** | _CSV_ |

**Key Columns Used**

| Column Name | Description | Role in Analysis |
|---|---|---|
| `status` | Loan default indicator (0/1) | Target variable |
| `ltv` | Loan-to-Value ratio | Strongest predictor — KPI / Risk Score |
| `debt_to_income_ratio` | Debt-to-Income ratio | Second strongest — KPI / Risk Score |
| `loan_amount` | Total loan amount | EAD / Expected Loss computation |
| `income` | Borrower income | Risk scoring component |
| `credit_score` | Borrower credit score | Validated as non-predictive (p=0.735) |
| `neg_ammortization` | Negative amortisation flag | Strongest categorical risk signal |
| `lump_sum_payment` | Lump sum payment flag | Protective factor |
| `risk_tier` | Computed risk tier | Final lending decision driver |
| `ltv_risk_bucket` | LTV categorised into Low / Moderate / High / Very High tiers | Core risk segmentation feature — dual-band policy |
| `credit_score_bucket` | Credit score banded into Poor / Fair / Good / Very Good / Excellent | Validated as non-discriminatory — included for comparison |

For full column definitions, see [`docs/data_dictionary.md`](docs/data_dictionary.md).

---

## KPI Framework

| # | KPI | Definition | Target Dashboard |
|---|-----|-----------|------------------|
| 1 | Total Loans | COUNT(*) | Portfolio Exposure & Default Risk Overview |
| 2 | Default Rate | Defaults / Total × 100 | Portfolio Exposure & Default Risk Overview |
| 3 | Total Loan Amount | SUM(loan_amount) | Portfolio Exposure & Default Risk Overview |
| 4 | High Risk % | COUNT(LTV>80) / Total × 100 | Portfolio Exposure & Default Risk Overview |
| 5 | Avg Interest Rate | AVG(rate_of_interest) | Portfolio Exposure & Default Risk Overview |
| 6 | Expected Loss (EL) | Default Rate × LGD × EAD | Portfolio Exposure & Default Risk Overview |
| 7 | Average Income | AVG(income) | Borrower Risk Drivers Analysis |
| 8 | Credit Score Gap | AVG(score, defaulters) / AVG(score, non-defaulters) | Borrower Risk Drivers Analysis |
| 9 | High Borrower Risk % | COUNT(LTV>80) / Total × 100 | Borrower Risk Drivers Analysis |
| 10 | Borrower Income Gap | AVG(income, defaulters) / AVG(income, all) | Borrower Risk Drivers Analysis |
| 11 | Top Loan Purpose | MAX(SUM(defaulted_amount) BY purpose) | Product & Geographic Risk Trends |
| 12 | Average Term | AVG(term) | Product & Geographic Risk Trends |
| 13 | Highest-Loss Region | MAX(SUM(defaulted_amount) BY region) | Product & Geographic Risk Trends |
| 14 | Most Risky Loan Type | MAX(Default Rate BY loan_type) | Product & Geographic Risk Trends |
| 15 | Worst Region–Product Combo | MAX(SUM(defaulted_amount) BY region, loan_type) | Product & Geographic Risk Trends |
| 16 | Loss Share by Purpose | defaulted_per_purpose / total_defaulted × 100 | Product & Geographic Risk Trends |

Full KPI logic is documented in `notebooks/05_final_load_prep.ipynb`.

---

## Tableau Dashboards

| Item | Details |
|---|---|
| **Dashboard URL** | [View Tableau Public Dashboard](https://public.tableau.com/shared/4SBGTH5PQ?:display_count=n&:origin=viz_share_link) |

### 1. Portfolio Exposure & Default Risk Overview
*   **Business Question**: *"How healthy is our current portfolio, and where is our risk concentrated?"*
*   **KPI Cards**: Total Loans, Default Rate, Total Loan Amt, High Risk %, Avg Interest Rate
*   **Charts**: Loan Distribution by Product, Interest Rate vs Default by Loan Purpose, Loan Amount Distribution, Loan Amount by Interest Rate
*   **Filters**: Loan Purpose, Region, Credit Score Bucket

### 2. Borrower Risk Drivers Analysis
*   **Business Question**: *"What borrower characteristics drive default, and how should we adjust underwriting?"*
*   **KPI Cards**: Average Income, Credit Score Gap, High Borrower Risk %, Borrower Income Gap
*   **Charts**: Default Rate by LTV, Default by Income, LTV × Credit Score Heatmap, Loan Volume vs Default Volume by Credit Score, Default Rate by Credit Score Bucket
*   **Filters**: Loan Type, Credit Score Bucket, Region, Approv In Adv, LTV Risk Bucket

### 3. Product & Geographic Risk Trends
*   **Business Question**: *"Which products and regions are bleeding money, and where should we restrict lending?"*
*   **KPI Cards**: Top Loan Purpose, Average Term, Highest-Loss Region, Most Risky Loan Type, Worst Region–Product Combo
*   **Charts**: Loss by Region, Risk vs Pricing by Loan Type, Region × Loan Type Heatmap, Loss Share, Avg DTI by Loan Type, Default Rate by Loan Type
*   **Filters**: Region, Loan Type, Loan Limit, Approv In Adv

Dashboard screenshots are in [`tableau/screenshots/`](tableau/screenshots/) and public links in [`tableau/dashboard_links.md`](tableau/dashboard_links.md).

---

## Key Insights

**1 in 4 Borrowers Defaults — Portfolio Under Systemic Stress**  
The portfolio default rate is **23.72%** — nearly 1 in 4 loans. This is not a borrower-level outlier problem; it signals a structural gap in the underwriting framework that cannot be resolved with incremental fixes.

**LTV Is the Only Reliable Numerical Risk Gate**  
`ltv` is the strongest numerical predictor of default (`r=0.0976`, logistic coefficient=0.2239). Very High LTV borrowers (≥90%) default at **35.8%** — more than double the Moderate LTV bucket (16.2%). LTV-based banding is statistically validated (`χ²=451.9`) and is the strongest single gating variable available.

**DTI Works Only at the Extremes — Not at the Industry Threshold**  
DTI is the second strongest signal (`r=0.0929`), but the industry-standard 43% cutoff is counterproductive in this portfolio — borrowers below it actually default slightly more (24.3%) than those above (22.1%). Risk only concentrates meaningfully below DTI=35 (13.0% default) and above DTI=50 (40.6%), requiring a dual-band replacement policy.

**Credit Score Is Statistically Irrelevant**  
`credit_score` shows near-zero correlation with default (`r=-0.0028`, `p=0.735`). Borrowers rated Excellent default at 23.7% — virtually identical to those rated Poor at 23.9%. The `credit_score_bucket` chi-square test also returned non-significant (`p=0.722`). Score-first screening provides false confidence with no actual risk separation.

**Product Features Outperform Borrower Characteristics**  
Lump sum payment (`χ²=498.5`) and negative amortisation (`χ²=363.1`) are the two strongest default predictors in the entire portfolio — stronger than any borrower metric. These are loan design choices, not borrower traits, meaning the institution's own product catalogue is a primary source of default risk.

**Lump Sum Payment Is the Highest-Risk Feature at 76.8%**  
Borrowers with a lump sum payment structure default at **76.8%** — 3× the portfolio average. Only 315 such loans exist, yet 242 defaulted. These borrowers make no monthly payments and rely on a future windfall that rarely materialises. This is the single most actionable restriction available.

**Negative Amortisation Doubles the Default Rate**  
`neg_ammortization = yes` borrowers default at **43.5%** — nearly double the 23.7% portfolio average. These loans accumulate debt instead of reducing it, directly eroding repayment capacity over time. The strong chi-square association (`χ²=363.1`) confirms this is not coincidence.

**North-East and Home Improvement Are Concentrated Loss Pockets**  
The North-East region has the highest default rate at **~33%**, over 11 percentage points above the North region. Home improvement loans default at **~32%**, the highest of any loan purpose — borrowers stack new debt on existing mortgages, amplifying total financial burden. Geographic and purpose-specific controls deliver more targeted loss containment than uniform policy.

**Personal Loans Carry Structurally Higher Unsecured Risk**  
Personal loans default at **33.5%** — nearly 12 percentage points above home loans (21.7%). Without collateral backing, these loans have no recovery buffer when borrowers face financial stress. A uniform approval standard across loan types systematically misprices this structural difference.

**Risk Tiers Replace Single-Variable Screening**  
The composite `risk_tier` framework (built on LTV, DTI, product features, and behavioural flags) produces clear default rate separation: Very High tier defaults at 45%+ while Low tier defaults at under 10%. This multi-factor segmentation outperforms any single-variable gate and directly supports the LTV + DTI dual-band lending policy.

---

## Recommendations

| # | Insight | Recommendation | Expected Impact |
|---|---|---|---|
| 1 | **LTV & DTI Dual-Band Policy** | Replace the current single-score approval gate with a two-variable threshold system: auto-approve borrowers with LTV < 60% and DTI < 35%; hold for manual review between 60–90% LTV and 35–50% DTI; hard-restrict loans above 90% LTV or DTI above 50%. | Estimated reduction of portfolio default rate from 23.72% to below 20.73%, saving over ₹4.28 Cr in expected loss exposure. |
| 2 | **Credit Score Screening Is Broken** | Retire credit score as the primary approval filter. Replace it with the composite `risk_tier` score built from LTV bucket, DTI band, product flags, and behavioural signals — which produces actual default rate separation unlike credit score bands (23.7% vs 23.9% across all tiers). | Decisions aligned to observed default behaviour instead of a metric with zero statistical predictive power. |
| 3 | **Negative Amortisation Must Be Restricted** | Introduce mandatory eligibility gates for negative amortisation products — minimum LTV < 70% and DTI < 35%, combined with risk-based premium pricing for borderline approvals. At 43.5% default rate with χ²=363.1, this product needs structural controls, not just monitoring. | Reduced structural default risk and a measurable drop in high-tier portfolio concentration. |
| 4 | **Lump Sum Payment Warrants Immediate Halt** | Suspend new lump sum payment approvals pending a portfolio review. At 76.8% default rate across 315 existing loans, this product feature is the single highest-risk element in the portfolio. Existing holders should be proactively migrated to standard amortising structures. | Immediate containment of the most acute default risk in the portfolio with no new capital at risk. |
| 5 | **Region & Purpose Targeted Lending Limits** | Establish a monthly segment watchlist tracking default rates by region × loan type × loan purpose. Apply hard lending caps in the North-East (33% default rate) and on home improvement loans (32% default rate), with enhanced income and DTI verification for new approvals in these segments. | Faster risk containment in known loss pockets and improved capital allocation away from structurally risky segments. |

---

## Repository Structure

```text
SectionD_G1_FinShield/
|
|-- README.md
|
|-- data/
|   |-- raw/                         # Original dataset (never edited)
|   `-- processed/                   # Cleaned output from ETL pipeline
|       |-- loan_stage1_cleaned.csv  # Output of Notebook 01 — initial clean
|       |-- loan_final_cleaned.csv   # Output of Notebook 02 — feature-engineered
|       `-- loan_tableau_ready.csv   # Output of Notebook 05 — KPIs & risk tiers
|
|-- notebooks/
|   |-- 01_extraction.ipynb
|   |-- 02_cleaning.ipynb
|   |-- 03_eda.ipynb
|   |-- 04_statistical_analysis.ipynb
|   `-- 05_final_load_prep.ipynb
|
|-- scripts/
|   `-- etl_pipeline.py
|
|-- tableau/
|   |-- screenshots/
|   `-- dashboard_links.md
|
|-- reports/
|   |-- README.md
|   |-- project_report_template.md
|   `-- presentation_outline.md
|
|-- docs/
|   `-- data_dictionary.md
|
|-- DVA-oriented-Resume/
`-- DVA-focused-Portfolio/
```

---

## Analytical Pipeline

The project follows a structured 7-step workflow:

1. **Define** - Sector selected, problem statement scoped, mentor approval obtained.
2. **Extract** - Raw dataset sourced and committed to `data/raw/`; data dictionary drafted.
3. **Clean and Transform** - Cleaning pipeline built in `notebooks/02_cleaning.ipynb` and optionally `scripts/etl_pipeline.py`.
4. **Analyze** - EDA and statistical analysis performed in notebooks `03` and `04`.
5. **Visualize** - Interactive Tableau dashboard built and published on Tableau Public.
6. **Recommend** - 3-5 data-backed business recommendations delivered.
7. **Report** - Final project report and presentation deck completed and exported to PDF in `reports/`.

---

## Tech Stack

| Tool | Status | Purpose |
|---|---|---|
| Python + Jupyter Notebooks | Mandatory | ETL, cleaning, analysis, and KPI computation |
| Google Colab | Supported | Cloud notebook execution environment |
| Tableau Public | Mandatory | Dashboard design, publishing, and sharing |
| GitHub | Mandatory | Version control, collaboration, contribution audit |
| SQL | Optional | Initial data extraction only, if documented |

**Recommended Python libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `statsmodels`

---


## Contribution Matrix

This table must match evidence in GitHub Insights, PR history, and committed files.

| Team Member | Dataset and Sourcing | ETL and Cleaning | EDA and Analysis | Statistical Analysis | Tableau Dashboard | Report Writing | PPT and Viva |
|---|---|---|---|---|---|---|---|
| _Daksh Batra_ (Project Lead) | Support | Support | Support | Support | Support | Support | Support |
| _Prakhar Rawat_ (Data Lead) | Owner | Support | Support | Support | Support | Support | Support |
| _Nitin Kumar_ (ETL Lead) | Support | Owner | Support | Support | Support | Support | Support |
| _Isha Tomar_ (Analysis Lead) | Support | Support | Owner | Owner | Support | Support | Support |
| _Kapish Rohilla_ (Visualization Lead) | Support | Support | Support | Support | Owner | Support | Support |
| _Rishi Raj_ (Strategy Lead) | Support | Support | Support | Support | Support | Owner | Support |
| _Nishant Ranjan Singh_ (PPT and Quality Lead) | Support | Support | Support | Support | Support | Support | Owner |

_Declaration: We confirm that the above contribution details are accurate and verifiable through GitHub Insights, PR history, and submitted artifacts._

**Team Lead Name:** Daksh Batra

**Date:** 29 April 2026


*Newton School of Technology - Data Visualization & Analytics | Capstone 2*
