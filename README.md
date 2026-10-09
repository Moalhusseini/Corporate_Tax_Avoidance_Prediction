# Machine Learning-Based Analysis of Corporate Tax Avoidance
### Evidence from Korean Listed Companies 🇰🇷

An integrated machine learning research framework for corporate tax avoidance analysis using the Korean Tax Avoidance Panel (KoTaP) dataset.

[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)](https://www.python.org/)
[![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Predictive%20Analytics-orange)](https://scikit-learn.org/)
[![Explainable AI](https://img.shields.io/badge/Explainable%20AI-SHAP-purple)](https://shap.readthedocs.io/)
[![Research](https://img.shields.io/badge/Focus-Financial%20Research-green)]()

---

## Project Overview

Corporate tax avoidance is an important topic in accounting, finance, and taxation research because it affects tax revenues, corporate transparency, and the interpretation of financial performance.

Traditional statistical approaches can provide valuable insights into corporate financial behavior. However, machine learning techniques can also capture nonlinear relationships and interactions among financial variables, offering additional opportunities for predictive analysis.

This research develops a comprehensive machine learning framework to analyze corporate tax avoidance among listed companies in South Korea. Using the Korean Tax Avoidance Panel (KoTaP) dataset, the study integrates statistical analysis, predictive modeling, firm segmentation, model optimization, and explainable artificial intelligence.

The framework examines corporate tax avoidance from multiple analytical perspectives rather than relying on a single predictive model.

## Research Objectives

The main objectives of this project are:

- Develop regression models to predict future corporate tax avoidance indicators.
- Build classification models to categorize firms according to corporate tax avoidance risk.
- Apply unsupervised clustering to identify groups of firms with similar financial characteristics.
- Evaluate the impact of hyperparameter optimization on model performance.
- Compare machine learning models using appropriate evaluation metrics.
- Apply SHAP to interpret the contribution of financial variables to model predictions.
- Implement chronological evaluation procedures to reduce temporal information leakage.
- Investigate relationships between financial performance, corporate characteristics, governance indicators, and tax-related measures.

## Dataset Description

The study uses the Korean Tax Avoidance Panel (KoTaP) dataset, which contains firm-level financial, governance, and tax-related information for publicly listed non-financial companies in South Korea.

<details>
<summary><strong>Dataset overview</strong></summary>

| Attribute | Description |
|---|---|
| Dataset | Korean Tax Avoidance Panel (KoTaP) |
| Country | South Korea |
| Study period | 2011–2024 |
| Number of observations | 12,653 |
| Number of variables | 65 |
| Number of unique firms | 1,754 |
| Observation structure | Firm-year panel data |
| Primary research domain | Corporate tax avoidance |
| Data format | CSV |

</details>

The dataset includes firms listed on the Korea Exchange, covering both KOSPI and KOSDAQ markets.

Its panel structure supports the examination of changes in corporate financial characteristics and tax-related indicators over time.

### Data Acquisition

The data preparation process involved:

1. Obtaining the publicly released KoTaP dataset.
2. Reviewing the accompanying variable definitions and documentation.
3. Loading the CSV file into Python.
4. Handling the Korean text encoding using `euc-kr`.
5. Examining the panel structure and verifying the suitability of variables for the analytical tasks.

## 🧩 Key Variables

The dataset contains several groups of variables relevant to corporate tax avoidance research.

| Category | Variables | Description |
|---|---|---|
| Firm Identification | `name`, `stock`, `year` | Company identity and fiscal year |
| Financial Structure | `asset`, `liab`, `equit`, `LEV` | Assets, liabilities, equity, and leverage |
| Profitability | `ROA`, `ROE`, `ni` | Profitability and net income |
| Operating Performance | `sales`, `CFO`, `GRW` | Revenue, operating cash flow, and growth |
| Corporate Governance | `big4`, `forn`, `own` | Auditor category, foreign ownership, and ownership concentration |
| Market Characteristics | `MB`, `TQ`, `KOSPI` | Market-to-book ratio, Tobin's Q, and listing category |
| Corporate Characteristics | `SIZE`, `AGE`, `LOSS` | Firm size, age, and loss indicator |
| Tax Indicators | `GETR`, `CETR` | GAAP effective tax rate and cash effective tax rate |
| Multi-year Tax Indicators | `GETR3`, `CETR3`, `GETR5`, `CETR5` | Multi-year effective tax rate measures |
| Adjusted Tax Indicators | `A_GETR`, `A_CETR`, and related variables | Adjusted versions of the tax measures |

The study uses multiple tax-related indicators because corporate tax avoidance cannot always be adequately represented by a single measure.

**Important:** Effective tax rates are proxies for tax-related behavior, not direct proof of illegal conduct. Tax avoidance and tax evasion are distinct concepts.

## Research Methodology

The project follows a structured analytical workflow.

### 1. Data Understanding and Quality Assessment

The initial stage examines the dataset's structure and statistical properties.

The analysis includes:

- Dataset dimensions and data types.
- Missing-value analysis.
- Duplicate-record detection.
- Numerical descriptive statistics.
- Unique-value analysis.
- Outlier detection using the interquartile range (IQR) method.
- Skewness and kurtosis analysis.
- Firm and year coverage assessment.

The initial data inspection reports 12,653 observations and 65 variables, with no missing values or duplicate records detected.

Potential outliers are retained during the initial assessment because extreme financial values may represent genuine differences between firms. Their influence should nevertheless be evaluated during subsequent modeling.

### 2. Exploratory Data Analysis

Exploratory data analysis is used to understand the distribution of financial variables and examine their relationships with tax-related indicators.

The analysis includes:

- Descriptive statistical summaries.
- Histograms and density plots.
- Box plots.
- Correlation matrices.
- Correlation rankings for `CETR` and `GETR`.
- Variance Inflation Factor (VIF) analysis.
- Yearly tax-indicator trends.
- Pivot-table comparisons across firm characteristics.

The study also examines differences across groups defined by:

- Audit category.
- Firm size.
- Financial leverage.
- Profitability.
- Foreign ownership.
- Ownership concentration.

These comparisons provide descriptive evidence of heterogeneity among firms. They do not, by themselves, establish causal relationships.

### 3. Feature Selection and Engineering

Candidate predictors are selected from financial, governance, profitability, and firm-characteristic variables.

Examples include:

- `SIZE`
- `LEV`
- `CUR`
- `GRW`
- `ROA`
- `CFO`
- `PPE`
- `AGE`
- `INVREC`
- `TQ`
- `LOSS`
- `big4`
- `forn`
- `own`

Feature selection considers statistical relationships, multicollinearity, variable importance, and the research context.

The study also evaluates redundancy among financial variables using correlation analysis and VIF.

### 4. Regression Modeling

Regression is used to predict future corporate tax avoidance indicators from current-period firm information.

The research follows a one-year-ahead forecasting design:

$$
X_{i,t} \longrightarrow Y_{i,t+1}
$$

where \(X_{i,t}\) represents the available characteristics of firm \(i\) in year \(t\), and \(Y_{i,t+1}\) represents its tax avoidance indicator in the following year.

The target indicators include measures such as `GETR`, `CETR`, and their multi-year or adjusted variants, subject to the target definition used in each experiment.

This approach evaluates whether current corporate characteristics contain predictive information about future tax-related outcomes.

### 5. Classification Modeling

Classification models are used to categorize firms according to different levels of future corporate tax avoidance risk.

This task differs from regression:

- **Regression:** Predicts a continuous tax-related indicator.
- **Classification:** Predicts a discrete tax-risk category.

The classification stage compares multiple machine learning algorithms using consistent evaluation criteria.

The precise category thresholds and final algorithm rankings should be taken from the implemented experiments rather than assumed from the project design.

### 6. Unsupervised Clustering

Clustering is used to identify groups of firms with similar financial and tax-related characteristics.

Unlike regression and classification, clustering does not require predefined target labels.

The purpose is to explore firm heterogeneity and determine whether the data contain distinguishable financial profiles that may help researchers understand differences in corporate behavior.

Cluster interpretation should be based on the characteristics of the resulting groups, rather than treating clusters as inherently meaningful tax-risk categories.

### 7. Hyperparameter Optimization

Hyperparameter optimization evaluates whether alternative model configurations improve predictive performance.

The optimized models are compared with their corresponding baseline models under the same evaluation protocol.

A meaningful improvement should be established using validation data and confirmed on a separate chronological test period.

### 8. Explainable Artificial Intelligence (SHAP)

SHAP (SHapley Additive exPlanations) is used to interpret predictions from the selected machine learning model.

The analysis examines:

- Global feature importance.
- The contribution of individual predictors to model outputs.
- Differences in feature contributions across observations.
- Financial characteristics associated with higher or lower model predictions.

SHAP values explain model behavior; they do not independently establish causal effects or prove that a particular firm has engaged in improper tax behavior.

### 9. Leakage-Free Temporal Evaluation

A central methodological component is the use of chronological evaluation rather than relying exclusively on random train-test splitting.

The intended design uses earlier observations for model development and later observations for evaluation.

Preprocessing steps, including feature scaling and other learned transformations, must be fitted using training data only.

This is important because information from future periods can otherwise influence the model and produce overly optimistic performance estimates.

For panel data, temporal separation should also be checked at the firm-year level to ensure that the evaluation matches the intended forecasting scenario.

## Technology Stack

| Category | Tools |
|---|---|
| Programming Language | Python |
| Data Manipulation | Pandas, NumPy |
| Statistical Analysis | SciPy, Statsmodels |
| Data Visualization | Matplotlib, Seaborn |
| Machine Learning | Scikit-learn |
| Data Preprocessing | StandardScaler, LabelEncoder |
| Explainable AI | SHAP |
| Development Environment | Google Colab / Jupyter Notebook |
| Data Format | CSV |



# Research Findings and Interpretation

## 1. Descriptive and Exploratory Findings

The Korean Tax Avoidance Panel (KoTaP) dataset contains 12,653 firm-year observations, 65 variables, and 1,754 Korean listed non-financial firms covering 2011–2024. No missing values or duplicate observations were identified.

The analysis revealed differences in corporate tax behavior across firms. CETR was negatively associated with ROA, ROE, and growth, while positive associations appeared with firm size, leverage, and historical tax indicators. Average CETR increased from 0.1921 for the smallest firms to 0.2755 for the largest firms.

## 2. Regression Results

The regression analysis used 10,899 observations to predict the following year's cash effective tax rate (CETR).

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Multiple Linear Regression | 0.1753 | 0.2320 | -0.0983 |
| LightGBM (17 features) | 0.1724 | 0.2229 | -0.0145 |
| LightGBM (full features) | 0.1651 | 0.2178 | 0.0315 |
| Optimized LightGBM | 0.1494 | 0.2094 | 0.1051 |
| Residual MLP | 0.1606 | 0.2291 | -0.0718 |

Optimized LightGBM achieved the best regression performance, reducing MAE by approximately 14.8% compared with the linear baseline. However, its R² of 0.1051 indicates that much of the variation in future CETR remains unexplained.

## 3. Classification Results

The classification models predicted three corporate tax-risk categories: Low, Medium, and High.

| Model | Accuracy | F1-score | Weighted ROC-AUC |
|---|---:|---:|---:|
| Logistic Regression | 55.00% | 0.4800 | 0.6745 |
| Random Forest (optimized) | 58.99% | 0.5640 | 0.7242 |
| SVM (baseline) | 58.00% | 0.5000 | 0.7203 |
| SVM (optimized) | 56.08% | 0.5092 | 0.6666 |

Optimized Random Forest achieved the strongest overall classification performance. Nevertheless, its accuracy of 58.99% indicates limited predictive reliability, particularly across all three risk categories.

## 4. Clustering Results

Isolation Forest identified 127 potential outliers, leaving 12,526 observations for clustering. K-Means identified a dominant group and smaller, more distinctive groups. A four-cluster Gaussian Mixture Model (GMM) further revealed differences in firm size, foreign ownership, leverage, liquidity, cash holdings, growth, and asset structure.

These clusters represent statistical groupings rather than definitive tax-risk categories.

## 5. SHAP Explainability

SHAP analysis identified historical tax indicators as the most influential features in the optimized LightGBM model.

| Feature | Mean Absolute SHAP |
|---|---:|
| A_GETR | 0.031094 |
| GETR5 | 0.024150 |
| PTI | 0.010275 |
| CETR5 | 0.009807 |
| TSDA | 0.008222 |

A_GETR was the most influential feature, followed by GETR5. These results highlight the predictive value of historical tax information but do not establish causal relationships.

## 6. Overall Interpretation

The results show that optimized LightGBM performed best for predicting future CETR, while optimized Random Forest achieved the strongest classification results. Clustering revealed differences in firms' financial characteristics, and SHAP highlighted the importance of historical tax indicators.

However, the regression R² of 0.1051 and classification accuracy of 58.99% indicate limited predictive capability. The findings support combining regression, classification, clustering, and explainability, while further financial and governance variables may be needed to improve future predictions.

## Research Contributions

The project integrates several complementary approaches into one analytical framework:

1. **Predictive analysis:** Forecasting future corporate tax avoidance indicators.
2. **Risk classification:** Categorizing firms according to future tax-related outcomes.
3. **Firm segmentation:** Exploring heterogeneity through unsupervised learning.
4. **Model optimization:** Comparing baseline and optimized configurations.
5. **Model explainability:** Interpreting predictions through SHAP.
6. **Temporal rigor:** Using leakage-aware procedures to improve the credibility of out-of-sample evaluation.

The combined framework supports a more comprehensive analysis of corporate tax avoidance than an isolated modeling task.

## Limitations

- The dataset represents South Korean listed non-financial firms; results may not generalize to other countries or private companies.
- Effective tax rates are imperfect proxies for corporate tax avoidance.
- Extreme financial values and multicollinearity may influence model behavior.
- Predictive associations do not establish causal relationships.
- Temporal evaluation does not automatically eliminate every form of information leakage.
- Classification outcomes depend on the definition and thresholds of the target categories.
- Model interpretability does not establish legal or regulatory misconduct.

## Future Research

Potential extensions include:

- Testing the framework on corporate datasets from additional countries.
- Comparing model performance across different tax avoidance proxies.
- Evaluating temporal stability across different economic periods.
- Applying firm-grouped and time-aware validation strategies.
- Investigating the sensitivity of results to feature selection and target definitions.
- Comparing explainability results across multiple predictive models.
- Examining whether predictive indicators remain informative under alternative evaluation designs.

## Author : Mohammed Alhusseini
ة
**Research Project:** Machine Learning-Based Analysis of Corporate Tax Avoidance: Evidence from Korean Listed Companies

**Research Areas:** Machine Learning, Financial Analytics, Corporate Taxation, Explainable AI, and Business Intelligence.

## Disclaimer

This project is intended for academic and research purposes. The models analyze statistical patterns in corporate financial and tax-related data; their predictions should not be treated as proof of tax avoidance, tax evasion, or legal non-compliance by any individual company.
