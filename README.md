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
| **Submission Date** | _To be filled by team_ |

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
| **Column Count** | _34 (raw) → 37 (Tableau-ready)_ |
| **Time Period Covered** | _2019_ |
| **Format** | _CSV_ |

**Key Columns Used**

| Column Name | Description | Role in Analysis |
|---|---|---|
| `status` | Loan default indicator (0 = No Default, 1 = Default) | Target variable |
| `ltv` | Loan-to-Value ratio | Strongest numerical predictor of default |
| `debt_to_income_ratio` | Debt-to-Income ratio | Second strongest predictor |
| `loan_amount` | Total loan amount | Exposure at Default computation |
| `income` | Borrower income | Risk scoring component |
| `credit_score` | Borrower credit score | Validated as non-predictive (p=0.735) |
| `neg_ammortization` | Negative amortisation flag | Strongest categorical risk signal (χ²=363.1) |
| `lump_sum_payment` | Lump sum payment flag | Protective factor (χ²=498.5) |
| `ltv_risk_bucket` | LTV risk band (Low/Moderate/High/Very High) | Risk segmentation |
| `risk_tier` | Computed risk tier | Final lending decision driver |

For full column definitions, see [`docs/data_dictionary.md`](docs/data_dictionary.md).

---

## KPI Framework

| KPI | Definition | Formula / Computation |
|---|---|---|
| Portfolio Default Rate | Overall percentage of loans that defaulted | `(Defaults / Total Loans) × 100` → **23.72%** |
| Exposure at Default (EAD) | Total loan amount at risk from defaults | `SUM(loan_amount) WHERE status=1` → **₹1.12B (22.64% of portfolio)** |
| Avg DTI by Default Status | Mean DTI for defaulters vs non-defaulters | Defaulters: **39.59** vs Non-defaulters: **37.49** (2.1pt gap) |
| Avg LTV by Default Status | Mean LTV for defaulters vs non-defaulters | Defaulters: **75.78** vs Non-defaulters: **71.65** (4.1pt gap) |
| Default Rate by LTV Bucket | Per-segment default rate | Low: 13.29% → Moderate: 31.65% → Very High: 23.42% |
| Default Rate by Loan Type | Per-product default rate | Personal Loan: **33.49%** vs Home Loan: **21.74%** |
| Default Rate by Region | Geographic default distribution | North-East: **33.60%** (highest) vs North: **22.04%** (lowest) |
| Composite Risk Score | Weighted DTI + LTV + product features | Computed in `notebooks/05_final_load_prep.ipynb` |
| Risk Tier | Categorical risk band | Score → Low / Medium / High / Very High |

KPI logic is documented in `notebooks/04_statistical_analysis.ipynb` and `notebooks/05_final_load_prep.ipynb`.

---

## Tableau Dashboard

| Item | Details |
|---|---|
| **Dashboard URL** | _Paste Tableau Public link here_ |
| **Executive View** | _Describe the high-level KPI summary view_ |
| **Operational View** | _Describe the detailed drill-down view_ |
| **Main Filters** | _List the interactive filters used_ |

Store dashboard screenshots in [`tableau/screenshots/`](tableau/screenshots/) and document the public links in [`tableau/dashboard_links.md`](tableau/dashboard_links.md).

---

## Key Insights

1. **Credit score is not a valid risk predictor** — T-test (p=0.735), point biserial correlation (r=-0.0028), and logistic regression coefficient (-0.0033) all confirm credit score has zero discriminatory power in this portfolio. Lending decisions based on credit score alone will not reduce defaults.

2. **LTV is the strongest numerical predictor of default** — Point biserial r=0.0976 (highest), logistic regression coefficient 0.2239 (odds ratio 1.251). Each standard deviation increase in LTV raises default odds by 25.1%.

3. **DTI is the second strongest predictor** — Point biserial r=0.0929, logistic regression coefficient 0.1952 (odds ratio 1.216). DTI > 35 shows 28.0% default vs 13.0% below — a 15-point gap.

4. **The industry-standard DTI threshold of 43% is ineffective** — At DTI=43%, the default rate difference is just -2.2%, near zero discriminatory power. Only extreme bands work: DTI < 35 = low risk, DTI > 50 = 40.6% default rate.

5. **Product features are the strongest categorical risk signals** — Negative amortisation (χ²=363.1) and lump sum payment (χ²=498.5) far exceed credit score bands (χ²=2.13, p=0.722) in default prediction.

6. **Personal loans carry 54% higher default risk than home loans** — 33.49% vs 21.74% default rate. Personal loans require stricter screening despite smaller average amounts.

7. **North-East region shows 33.60% default rate** — highest across all regions, 52% higher than North (22.04%). Geographic concentration risk needs monitoring.

8. **Exposure at Default is ₹1.12 billion (22.64% of portfolio)** — Nearly a quarter of the portfolio's total loan exposure is at risk, underscoring the need for proactive risk segmentation.

9. **Defaulters have 4.1 points higher average LTV than non-defaulters** — LTV 75.78 vs 71.65, confirming that over-leveraged borrowers default more frequently.

10. **Higher income is protective against default** — Logistic regression confirms income has a negative coefficient (-0.0463), with lower-income borrowers showing elevated default probability.

---

## Recommendations

| # | Insight | Recommendation | Expected Impact |
|---|---|---|---|
| 1 | Credit score has zero predictive power (p=0.735) | Replace credit-score-first screening with LTV + DTI dual-band risk assessment | Eliminate false confidence in 3,773+ approvals based on non-predictive metric |
| 2 | DTI < 35 = 13% default vs > 50 = 40.6% default | Implement DTI dual-band policy: approve DTI < 35, restrict DTI > 50, review 35–50 | Reduce high-DTI default exposure by up to 40% |
| 3 | Negative amortisation (χ²=363.1) strongly predicts default | Restrict or eliminate negative amortisation products for Medium/High risk tiers | Directly reduce the strongest categorical default signal |
| 4 | Personal loans default at 33.49% vs home loans at 21.74% | Apply risk-based pricing: higher rates or reduced amounts for personal loans | Offset higher expected losses through appropriate risk premiums |
| 5 | North-East region has 33.60% default rate | Implement regional exposure caps and enhanced due diligence for North-East | Prevent geographic concentration risk from compounding portfolio losses |

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
|       |-- loan_final_cleaned.csv   # Output of notebook 02
|       `-- loan_tableau_ready.csv   # Output of notebook 05 (Tableau export)
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
| _Member 1_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ |
| _Member 2_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ |
| _Member 3_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ |
| _Member 4_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ |
| _Member 5_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ |
| _Member 6_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ |

_Declaration: We confirm that the above contribution details are accurate and verifiable through GitHub Insights, PR history, and submitted artifacts._

**Team Lead Name:** _____________________________

**Date:** _______________


*Newton School of Technology - Data Visualization & Analytics | Capstone 2*
