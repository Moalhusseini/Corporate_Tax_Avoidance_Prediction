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


### 4. Execute the Analysis

Run the notebook sequentially, beginning with data acquisition and understanding, followed by exploratory analysis, preprocessing, modeling, evaluation, clustering, and explainability.

## Research Findings and Interpretation

### 1. Descriptive and Exploratory Findings

The empirical analysis was conducted using the Korean Tax Avoidance Panel (KoTaP) dataset, which contains **12,653 firm-year observations, 65 variables, and 1,754 unique Korean listed non-financial firms** covering the period from 2011 to 2024. The initial data quality assessment identified no missing values or duplicate observations.

The exploratory analysis revealed substantial variation in corporate tax avoidance indicators across firms and years. The accounting-based effective tax rate (GETR) and cash effective tax rate (CETR) did not follow identical yearly patterns, indicating that the choice of tax avoidance measure can influence the interpretation of corporate tax behaviour.

Several financial variables exhibited skewed distributions and extreme observations. These observations were retained in the initial descriptive analysis because they may reflect genuine differences in firm size, financial structure, and operating performance. The correlation analysis identified negative associations between CETR and variables such as return on assets (ROA), return on equity (ROE), and growth (GRW). Positive associations were observed between CETR and several historical tax-related variables, firm size, and leverage.

The quartile analysis further showed differences in tax indicators across firm characteristics. In particular, average CETR increased from **0.1921 in the smallest firm-size quartile to 0.2755 in the largest quartile**. Firms in higher leverage quartiles also generally exhibited higher tax-rate measures than firms in the lowest leverage group. These findings demonstrate heterogeneity in corporate tax behaviour and support the use of multiple financial and tax-related indicators in the predictive analysis.

### 2. Regression Findings

The regression experiments evaluated the ability of machine learning models to predict the subsequent year's cash effective tax rate (\(CETR_{t+1}\)) using information available in the current period. After excluding firm-year observations without an available subsequent-year target, the predictive dataset contained **10,899 observations**.

Multiple Linear Regression established the baseline performance, achieving an MAE of 0.1753, an RMSE of 0.2320, and an \(R^2\) of −0.0983. The negative \(R^2\) indicates that the baseline model performed poorly in explaining variation in future CETR under the temporal evaluation setting.

LightGBM produced progressively better results as relevant explanatory variables were added. The initial 17-feature configuration achieved an MAE of 0.1724, an RMSE of 0.2229, and an \(R^2\) of −0.0145. Expanding the model to include the full financial feature configuration reduced the MAE to 0.1651 and the RMSE to 0.2178, while increasing \(R^2\) to 0.0315.

The strongest regression results were obtained after incorporating historical tax-related variables. The optimized LightGBM model achieved a final **MAE of 0.1494, RMSE of 0.2094, and \(R^2\) of 0.1051** on the independent test period. Compared with the Multiple Linear Regression baseline, the optimized LightGBM model reduced MAE by approximately 14.8% and RMSE by approximately 9.7%.

The Residual Multi-Layer Perceptron achieved an MAE of 0.1606, an RMSE of 0.2291, and an \(R^2\) of −0.0718. Although its MAE was lower than that of the linear baseline, it did not outperform the optimized LightGBM model.

Overall, the regression findings show that the optimized LightGBM model provided the best predictive performance among the reported regression configurations. However, its \(R^2\) of 0.1051 indicates that it explained only a limited proportion of the variation in future CETR. The results therefore support the predictive usefulness of historical tax information while also demonstrating that substantial variation remains unexplained.

### 3. Classification Findings

The classification experiments assigned observations to three corporate tax-risk categories: Low, Medium, and High. Logistic Regression, Random Forest, and Support Vector Machine (SVM) were evaluated using Accuracy, Precision, Recall, F1-score, and weighted multiclass ROC-AUC.

Logistic Regression achieved an accuracy of 0.5500, precision of 0.5300, recall of 0.5500, F1-score of 0.4800, and weighted ROC-AUC of 0.6745. This established a baseline for comparison with nonlinear classification models.

The baseline Random Forest improved upon Logistic Regression, achieving an accuracy of 0.5800 and a weighted ROC-AUC of 0.7068. Following hyperparameter optimization, the Random Forest achieved an accuracy of **0.5899**, precision of 0.5722, recall of 0.5899, F1-score of 0.5640, and weighted ROC-AUC of 0.7242.

The improvement was observed across all reported metrics. Accuracy increased by 0.0099, while the F1-score increased by 0.0340 and weighted ROC-AUC increased by 0.0174. These results indicate that hyperparameter optimization improved the overall balance of the Random Forest classifier, although the increase in accuracy remained modest.

The baseline SVM achieved an accuracy of 0.5800 and a weighted ROC-AUC of 0.7203. However, its optimized version performed less effectively, with accuracy decreasing to 0.5608 and weighted ROC-AUC to 0.6666. This demonstrates that hyperparameter optimization does not necessarily improve every model.

The classification analysis also showed that the models identified the Medium-risk category more successfully than the Low-risk category. Therefore, overall accuracy alone does not fully describe their classification performance.

Among the evaluated classifiers, the **optimized Random Forest achieved the strongest overall balance of classification metrics**. Nevertheless, its accuracy of 58.99% indicates that the three tax-risk categories cannot be predicted reliably using the available features alone.

### 4. Clustering Findings

The clustering analysis was conducted to investigate whether firms could be grouped according to their financial and governance characteristics. Because extreme observations affected distance-based clustering, Isolation Forest was applied within the clustering workflow. It identified 127 potential outlier observations, leaving **12,526 observations** for the subsequent clustering analysis.

The K-Means results indicated a dominant group of firms with relatively similar characteristics, alongside smaller groups with more distinctive profiles. This suggests that the dataset does not contain extremely strong natural segmentation across all firms.

A four-cluster solution was also examined using the Gaussian Mixture Model (GMM). The resulting cluster profiles revealed differences in firm size, foreign ownership, leverage, cash holdings, liquidity, growth, and asset structure. The largest and more resource-intensive group was characterized by higher firm size, foreign ownership, leverage, cash holdings, and asset tangibility. Other groups represented different combinations of firm size, governance characteristics, liquidity, and growth.

These findings indicate that clustering can provide a complementary perspective on firm heterogeneity. However, the clusters should be interpreted as statistical groupings based on the selected features rather than as definitive economic or tax-risk categories.

### 5. SHAP Explainability Findings

SHAP analysis was applied to the optimized LightGBM regression model to identify the variables contributing most strongly to its predictions of future CETR. The global feature-importance results showed that historical tax-related indicators were among the most influential explanatory variables.

The highest mean absolute SHAP values were observed for:

| Feature | Mean absolute SHAP value |
|---|---:|
| A_GETR | 0.031094 |
| GETR5 | 0.024150 |
| PTI | 0.010275 |
| CETR5 | 0.009807 |
| TSDA | 0.008222 |
| ROE | 0.006354 |
| GRW | 0.004650 |
| lag1_ni | 0.004524 |
| A_CETR | 0.004159 |
| PPE | 0.003830 |

A_GETR was the most influential feature, followed by GETR5. The importance of these variables suggests that historical tax-related information contains useful predictive signals for future CETR. The SHAP dependence analysis also indicated a nonlinear relationship between A_GETR and the model output, providing additional support for using a nonlinear model in this forecasting task.

These SHAP values measure the magnitude of each variable's contribution to model predictions. They do not establish causal relationships, nor do they independently demonstrate whether a variable increases or decreases predicted CETR. The direction of the relationship must be interpreted using the corresponding SHAP dependence or summary plots.

### 6. Overall Interpretation

Taken together, the findings demonstrate that corporate tax avoidance can be examined from complementary predictive and exploratory perspectives. The regression results identify optimized LightGBM as the strongest reported model for one-year-ahead CETR prediction, while the optimized Random Forest provides the strongest overall classification performance among the evaluated classifiers. The clustering analysis reveals meaningful differences in firms' financial profiles, and SHAP analysis highlights the predictive importance of historical tax-related variables.

The findings also reveal important limitations. The final regression \(R^2\) of 0.1051 and classification accuracy of 0.5899 indicate moderate predictive capability rather than highly accurate forecasting. Furthermore, the negative \(R^2\) of the linear baseline and Residual MLP shows that greater model complexity does not automatically guarantee better predictive performance.

The chronological evaluation design provides a more realistic assessment of forecasting performance than a random split when the objective is to predict future observations. Nevertheless, the results should be interpreted within the scope of the available dataset, features, and evaluation period. In addition, SHAP results describe model behaviour rather than causal effects.

Overall, this study demonstrates the value of integrating regression, classification, clustering, and explainability into a single machine learning framework for analysing corporate tax avoidance. The results particularly highlight the importance of historical tax measures while showing that additional financial, governance, institutional, and macroeconomic information may be needed to improve future predictions.


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
