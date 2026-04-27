# Drivers of Cyberattack Severity: A Data Science Analysis of Financial Loss, User Impact, and Incident Response

## Project Overview

This project studies **cyberattack severity** using a data science approach and two independent cybersecurity datasets. The main goal is to explore which cyberattack characteristics are related to:

- higher financial loss
- greater user impact
- longer incident resolution time

The project combines **data cleaning**, **exploratory data analysis**, **hypothesis testing**, and **predictive modeling** in order to better understand cyberattack severity from both a business-impact and an operational perspective.

---

## Main Research Question

**Which characteristics of cyberattacks are most strongly associated with higher financial loss, greater user impact, and longer incident response times?**

### Sub-questions

1. Which attack types are associated with the highest average financial loss?
2. Which industries or sectors experience the greatest user impact from cyber incidents?
3. Which factors are associated with longer incident resolution times?
4. How do vulnerability categories, defense mechanisms, and operational indicators relate to severity?
5. To what extent can severity-related outcomes be estimated or predicted from available cyberattack features?

---

## Datasets Used

This project uses **two independent datasets** downloaded from Kaggle:

1. [Global Cybersecurity Threats (2015–2024)](https://www.kaggle.com/datasets/atharvasoundankar/global-cybersecurity-threats-2015-2024)
   Used as the main dataset for analyzing:
   - financial loss
   - number of affected users
   - incident resolution time

2. **[Cybersecurity Attacks](https://www.kaggle.com/datasets/teamincribo/cyber-security-attacks/data)**  
   Used as the supporting dataset for analyzing:
   - anomaly scores
   - severity level
   - action taken
   - other operational indicators

These datasets were analyzed separately because they describe different aspects of cybersecurity and do not share a direct row-by-row merge key.

---

## Project Structure

- **1. Introduction**
- **2. Problem Formulation**
- **3. Research Questions and Objectives**
- **4. Dataset Exploration**
- **5. Data Cleaning and Validation**
- **6. Exploratory Data Analysis**
- **7. Statistical Analysis and Hypothesis Testing**
- **8. Predictive Modeling**
- **9. Main Research Question: Final Answer**
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

### Exploratory Data Analysis
- bar charts
- histograms
- boxplots
- correlation matrices
- grouped summary tables
- heatmaps

### Statistical Analysis
- one-way **ANOVA**
- **Chi-square test of independence**

### Predictive Modeling
- **Linear Regression**
- **Random Forest Regressor**
- **Logistic Regression**
- **Random Forest Classifier**
- baseline models for comparison

### Evaluation Metrics
- **MAE**
- **RMSE**
- **R²**
- **Accuracy**
- **F1-score**

---

## Main Findings

- In **Global Cybersecurity Threats (2015-2024)**, some groups showed slightly higher average severity outcomes:
  - **DDoS** had the highest average financial loss
  - **IT** had the highest average number of affected users
  - **Unpatched Software** was linked to the longest average incident resolution time

- However, these differences were generally **small**.

- In **Cyber Security Attacks**, operational indicators such as `attack_type`, `action_taken`, `anomaly_scores`, and `severity_level` also showed **weak differences** between groups.

- The statistical tests did **not** provide enough evidence for strong significant differences in the tested cases.

- The predictive models showed **limited performance**, especially for **Cyber Security Attacks**, which suggests that the available features do not explain severity very well on their own.

### Final Conclusion
No single variable appeared to be a strong standalone driver of cyberattack severity in these datasets. Instead, severity seems to depend on a more complex combination of factors.

---

## Repository Contents

```text
.
├── Drivers of Cyberattack Severity.ipynb
├── Global_Cybersecurity_Threats_2015-2024.csv
├── cybersecurity_attacks.csv
├── .gitignore
└── README.md
