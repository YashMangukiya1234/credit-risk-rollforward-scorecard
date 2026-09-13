# credit-risk-rollforward-scorecard
End-to-end early-stage credit collection scorecard predicting 0-to-30+ DPD roll-forward risk using WOE Logistic Regression, SparkR, and OptBinning.

# Enterprise Portfolio: Unsecured Credit Roll-Forward Collection Scorecard

## Project Overview
* **Domain:** Consumer Lending / Credit Risk Analytics
* **Role:** Lead Data Scientist
* **Stack:** R, SparkR, SQL, OptBinning, Git
* **Notice:** *All data, variable names, and specific institutional metrics have been generalized or synthesized to protect proprietary business information.*

---

## 1. Business Problem & Objective
* **Context:** High early-stage delinquency (0 DPD) driving elevated charge-off rates on unsecured retail products.
* **Goal:** Build an early-stage collection scorecard to rank-order accounts by their probability of rolling forward into 30+ DPD within a 90-day window.
* **Operational Impact:** Enable risk teams to dynamically allocate collection capacity and prioritize high-risk accounts.

---

## 2. Technical Methodology & Workflow

### Data & Feature Engineering
* **Data Sources:** On-us repayment behavior, cross-industry bureau trended data, inquiry patterns, and trade composition.
* **Variable Selection:** Filtered 300+ initial features down to core drivers using:
  1. Statistical Variance Analysis
  2. Feature Importance ranking via shallow XGBoost
  3. Information Value ($IV > 0.05$)
  4. Characteristic Stability Index ($CSI < 0.05$)
  5. Multi-collinearity filtering ($VIF < 2.5$)
  6. Correlation filtering ($CORR < 0.55$)

### Binning & Model Fitting
* Applied Weight of Evidence (WOE) binning with strict monotonic constraints to align with risk domain logic.
* Trained WOE-based Logistic Regression to maintain 100% model explainability for internal governance and regulatory audits.

---

## 3. Validation & Performance Framework
* **Out-of-Time (OOT) Testing:** Validated across 4 distinct quarters to account for macroeconomic seasonality.
* **Key Performance Metrics Achieved:**
  * **KS Statistic:** ~42
  * **Gini Coefficient:** ~56%
  * **Captured Rate:** Successfully identified 70% of actual roll-forward accounts within the top 30% worst risk deciles.

---

## 4. Governance & Deployment Considerations
* Designed Population Stability Index (PSI) and Characteristic Stability Index (CSI) monitoring triggers.
* Formulated decisioning thresholds integrated directly into the automated strategy engine.
