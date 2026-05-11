# Drivers of Cyberattack Severity: A Data Science Analysis of Financial Loss, User Impact, and Incident Response

## Project Overview

This project studies **cyberattack severity** using a data science approach and two independent cybersecurity datasets. Severity is treated as a single measurable quantity (a composite index combining financial loss, affected users, and incident resolution time), and the analysis examines which characteristics of cyberattacks — about the attacker, the target, or the defender — are linked to higher severity.

The project combines **data cleaning**, **exploratory data analysis**, **hypothesis testing with effect sizes**, **multivariate modelling**, and **cross-dataset validation** in order to investigate cyberattack severity from both a business-impact and an operational perspective.

---

## Main Research Question

**Which characteristics of cyberattacks — describing the attacker, the target, or the defender — are most strongly linked to higher severity, and how big are these effects in practice?**

### Sub-questions

The hypotheses are grouped into three families that each test the same question against different feature groups:

- **Family A (Attacker)** — does severity depend on attack type or attack source?
- **Family B (Target)** — does severity depend on target industry or country?
- **Family C (Defender)** — does severity depend on the exploited vulnerability or the defense mechanism in place?
- **Joint analysis** — can severity be predicted from all features together in a multivariate model?
- **Cross-dataset validation** — do the conclusions hold when re-tested on the second dataset?

---

## Datasets Used

This project uses **two independent datasets** in a primary/validation framework:

1. [Global Cybersecurity Threats (2015–2024)](https://www.kaggle.com/datasets/atharvasoundankar/global-cybersecurity-threats-2015-2024) — **primary dataset** (3,000 rows). Used to define the severity index, run the main hypothesis tests, and fit the predictive models.

2. [Cybersecurity Attacks](https://www.kaggle.com/datasets/teamincribo/cyber-security-attacks/data) — **validation dataset** (40,000 rows). Used to re-test the conclusions on independent data with different variables and different severity measures (`anomaly_scores` and `severity_level`).

The two datasets do not share a row-level merge key, so they are used as independent samples in a cross-dataset validation rather than a combined dataset.

---

## Project Structure

- **1. Abstract**
- **2. Introduction**
- **3. Problem Formulation**
- **4. Research Questions and Objectives**
- **5. Data Exploration**
- **6. Data Cleaning and Validation** (includes operational definition of severity)
- **7. Exploratory Data Analysis**
- **8. Statistical Analysis, Hypothesis Testing, and Predictive Modeling**
  - 8.1 Effect Sizes and Multiple-Comparison Correction
  - 8.2 Statistical Methodology
  - 8.3 Hypothesis Testing for Dataset 1 (H1–H6)
  - 8.4 Pairwise Differences with Cohen's d
  - 8.5 Odds Ratios for High-Severity Incidents
  - 8.6 Sensitivity Analysis on Severity Weights
  - 8.7 Multivariate Analysis with Random Forest
  - 8.8 Predictive Modeling for Dataset 1
  - 8.9 Cross-Dataset Validation on Dataset 2 (V1–V8)
  - 8.10 Predictive Modeling for Dataset 2
  - 8.11 Sub-question 5 Answer
- **9. Answer to the Main Research Question** (includes unified effect-size summary)
- **10. Limitations**
- **11. Conclusion**
- **12. Resources**

---

## Methods Used

### Data Preparation
- missing value analysis
- duplicate checking
- type conversion
- feature simplification
- categorical encoding preparation

### Operational Definition of Severity
- composite severity index built from three normalised components (financial loss, affected users, resolution time)
- min-max normalisation to [0, 1]
- equal-weight aggregation
- binary `severity_high` flag at the 75th percentile for binary analyses

### Exploratory Data Analysis
- bar charts, histograms, boxplots
- correlation matrices, heatmaps
- grouped summary tables

### Statistical Analysis
- one-way **ANOVA** with **η² (eta-squared)** as the effect-size metric
- **Chi-square test of independence** with bias-corrected **Cramér's V**
- **Cohen's d** with **bootstrap 95% confidence intervals** for pairwise comparisons
- **Odds ratios** with Woolf log-scale 95% CIs for binary comparisons
- **Pearson correlations** with Fisher-z 95% CIs
- **Holm-Bonferroni correction** for multiple-comparison control
- **Sensitivity analysis** on the severity weights

### Multivariate and Predictive Modeling
- **Random Forest Regressor** with 5-fold cross-validation and **permutation feature importance**
- **Linear Regression**
- **Logistic Regression**
- **Random Forest Classifier**
- baseline models (dummy) for comparison

### Evaluation Metrics
- **MAE, RMSE, R²** for regression
- **Accuracy, F1-score** for classification

---

## Main Findings

The analysis reaches a consistent negative result across two independent datasets, three operationalisations of severity, and three families of statistical tests:

- **Every η² in the six main hypothesis tests (H1–H6) is below 0.005**, well under Cohen's small-effect threshold of 0.01. The largest single-feature effect is `country` (η² ≈ 0.004), still negligible by Cohen's standards.
- **Of 36 category-vs-rest odds ratios for `severity_high`, zero have a 95% confidence interval that excludes 1.0**. No single category meaningfully sorts incidents into "more severe" or "less severe."
- **The pairwise check finds one statistically distinguishable difference** (Brazil vs India for country, Cohen's d ≈ 0.24) — the closest thing to a real signal in the entire analysis, but still small.
- **Sensitivity analysis** shows that the conclusions do not depend on the severity weights — η² for `attack_type` stays in [0.0007, 0.0014] across seven different weighting schemes.
- **A multivariate Random Forest using all seven features achieves a cross-validated R² of about -0.04**, slightly worse than predicting the mean. Permutation importance scores are within sampling noise of zero for every feature.
- **The cross-dataset validation (V1–V8) on Dataset 2 reaches the same conclusion**. All eight effect sizes are negligible. The only "significant" raw p-value (V3, p = 0.044) corresponds to η² = 0.00016 and disappears after Holm correction.

### Final Conclusion

The high-level cyberattack descriptors available in these two datasets are not meaningfully associated with severity. The fact that this conclusion replicates across two independent datasets with very different sizes and variables is much stronger evidence than either dataset alone could provide. The remaining variance in severity — over 99.6% — comes from sources the datasets do not capture, most likely incident-specific details such as organisation size, security maturity, the specific vulnerability or CVE exploited, and dwell time before detection.
