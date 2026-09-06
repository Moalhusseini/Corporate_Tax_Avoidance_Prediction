# Machine Learning-Based Analysis of Corporate Tax Avoidance

## Evidence from Korean Listed Companies

This repository contains the code, analysis, and documentation for a research study on corporate tax avoidance among Korean listed companies using machine learning methods.

The study uses the **Korean Tax Avoidance Panel (KoTaP)** dataset and investigates whether financial characteristics and historical tax-related information can be used to predict future corporate tax avoidance.

---

## Abstract

Corporate tax avoidance is an important issue in corporate finance because firms differ substantially in their tax behavior and in the factors associated with their effective tax rates. This study examines corporate tax avoidance among Korean listed companies using a machine learning-based empirical framework.

The analysis combines descriptive analysis, regression, classification, clustering, hyperparameter optimization, and explainable machine learning. Corporate tax avoidance is measured primarily using the Cash Effective Tax Rate (CETR) and related historical tax measures. The predictive task focuses on one-year-ahead CETR using information available in the previous year.

Several machine learning models are evaluated against traditional statistical baselines. LightGBM is used for regression, while Logistic Regression, Random Forest, and Support Vector Machine models are used for classification. Hyperparameter optimization is applied to the main tree-based models. In addition, clustering methods are used to identify groups of firms with different financial characteristics, and SHAP is applied to the optimized LightGBM model to improve the interpretation of its predictions.

The results indicate that nonlinear machine learning methods can provide better predictive performance than the linear baseline, although the overall predictive power remains moderate. Historical tax-related variables are among the most important contributors to future CETR predictions.

---

## Research Objectives

The main objectives of this study are to:

1. Analyze corporate tax avoidance patterns among Korean listed companies.
2. Identify financial and tax-related factors associated with future CETR.
3. Compare traditional statistical models with machine learning approaches.
4. Classify firms according to their expected level of future tax avoidance.
5. Identify meaningful groups of firms using clustering techniques.
6. Optimize machine learning model performance using hyperparameter search.
7. Interpret the most important predictors of future CETR using SHAP.

---

## Dataset

The study uses the **Korean Tax Avoidance Panel (KoTaP)** dataset.

### Dataset characteristics

- **Country:** South Korea
- **Period:** 2011–2024
- **Firms:** 1,754 Korean listed non-financial firms
- **Firm-year observations:** 12,653
- **Variables:** 65

The dataset contains financial, ownership, governance-related, and tax-related variables used to examine corporate tax behavior.

The main tax avoidance measures used in the study are:

- **CETR:** Cash Effective Tax Rate
- **GETR:** Generally accepted effective tax rate / total tax expense based measure
- Historical CETR and GETR measures over multiple years

---

## Methodology

The empirical framework consists of several complementary analyses.

### 1. Descriptive Analysis and EDA

The first stage examines:

- Distribution of the main variables
- Missing values
- Duplicate observations
- Outliers
- Correlation patterns
- Yearly changes in CETR and GETR
- Differences across firm characteristics

Financial outliers are generally retained because they represent actual heterogeneity among firms. Outlier removal is applied only where required for clustering.

### 2. Regression Analysis

The regression task predicts **one-year-ahead CETR**.

The models include:

- Multiple Linear Regression (MLR)
- LightGBM
- Residual Multi-Layer Perceptron (MLP)

The prediction framework follows a chronological setting to avoid using future information when constructing model inputs.

### 3. Classification Analysis

Firms are classified into three tax avoidance categories based on one-year-ahead CETR:

- **High tax avoidance**
- **Medium tax avoidance**
- **Low tax avoidance**

The classification models are:

- Logistic Regression
- Random Forest
- Support Vector Machine (SVM)

Random Forest and SVM models are evaluated both before and after hyperparameter optimization.

### 4. Clustering Analysis

Unsupervised learning is used to identify groups of firms with similar financial characteristics.

The clustering process includes:

- Robust scaling
- Isolation Forest for anomaly detection
- K-Means clustering
- Gaussian Mixture Model (GMM)

Cluster quality is evaluated using appropriate clustering criteria such as silhouette score, AIC, and BIC.

### 5. Hyperparameter Optimization

Hyperparameter optimization is used to improve the performance of the main machine learning models.

For the LightGBM regression model, **Optuna** is used to search for effective hyperparameter combinations.

The optimization process considers parameters such as:

- Number of estimators
- Learning rate
- Maximum depth
- Number of leaves
- Minimum child samples
- Subsample ratio
- Feature sampling ratio

### 6. Explainable Machine Learning

**SHAP (SHapley Additive exPlanations)** is applied only to the optimized LightGBM regression model.

The analysis is used to determine which variables contribute most to model predictions and to examine the economic interpretation of the most influential predictors.

SHAP values are interpreted as model contributions and are **not treated as causal effects**.

---

## Feature Set

The main predictive variables include:

```text
big4
forn
own
SIZE
LEV
CUR
GRW
ROA
CFO
cash
PPE
tan
intan
AGE
INVREC
TQ
LOSS
