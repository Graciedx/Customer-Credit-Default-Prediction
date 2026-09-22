# Customer Credit Default Prediction

An empirical machine learning project comparing **Logistic Regression** and **Decision Tree** models for predicting consumer loan default.

The project examines whether a more flexible tree-based model can improve default detection compared with the traditional Logistic Regression approach commonly used in credit scoring. In addition to predictive performance, the analysis considers the practical trade-off between **model performance and interpretability** in credit risk management.

---

## Project Overview

Credit risk modelling is an important part of lending because financial institutions need to estimate the likelihood that a borrower will default on a loan.

Traditional credit scoring approaches such as Logistic Regression are widely used because they are relatively interpretable and easy to communicate to business and regulatory stakeholders. However, their linear structure may limit their ability to capture nonlinear relationships between borrower characteristics.

This project investigates whether a **Decision Tree classifier** can provide stronger predictive performance while considering the interpretability and governance advantages of Logistic Regression.

### Research Question

> **How does a Decision Tree model compare with Logistic Regression in predicting consumer loan default, and what are the practical trade-offs between predictive performance and interpretability?**

---

## Objectives

The project has four main objectives:

1. Prepare and explore a consumer loan dataset for credit default modelling.
2. Build a Logistic Regression model as a traditional credit-scoring benchmark.
3. Build a Decision Tree classifier to capture potentially nonlinear relationships and interactions.
4. Compare both models using classification metrics that are particularly relevant to credit risk management.

The main evaluation metrics are:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC

Because the dataset contains substantially more non-default observations than default observations, particular attention is given to **Recall and ROC-AUC**, rather than relying on accuracy alone.

---

## Dataset

The analysis uses a consumer loan dataset containing **32,577 observations** and borrower/loan characteristics.

The target variable is:

- `loan_status`
  - `0` = non-default
  - `1` = default

### Main Features

The dataset contains borrower characteristics, loan characteristics and previous credit behaviour.

#### Numerical variables

- `person_age` — borrower age
- `person_income` — annual income
- `person_emp_length` — employment length
- `loan_amnt` — loan amount
- `loan_int_rate` — loan interest rate
- `loan_percent_income` — loan amount as a percentage of income
- `cb_person_cred_hist_length` — credit history length

#### Categorical variables

- `person_home_ownership`
- `loan_intent`
- `loan_grade`
- `cb_person_default_on_file`

---

## Data Preprocessing

Several preprocessing steps were performed before model training.

### 1. Missing Value Treatment

Missing values were identified in:

- `person_emp_length`
- `loan_int_rate`

Missing numerical observations were replaced using **median imputation**.

This resulted in a complete dataset with no remaining missing values before model training.

### 2. Categorical Encoding

Categorical variables were transformed into numerical features using **one-hot encoding**.

The first category was dropped where appropriate to reduce perfect multicollinearity.

### 3. Feature and Target Separation

The dataset was divided into:

- `X` — predictor variables
- `y` — `loan_status`

### 4. Train-Test Split

The data was divided into:

- **80% training data**
- **20% test data**

A stratified split was used to preserve the proportion of default and non-default observations in both datasets.

## Results

The models produced the following results on the test set:

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.867 | 0.763 | 0.564 | 0.649 | 0.758 |
| Decision Tree | 0.891 | 0.738 | 0.773 | 0.755 | 0.848 |

### Logistic Regression

Logistic Regression achieved:

- **86.7% accuracy**
- **76.3% precision**
- **56.4% recall**
- **64.9% F1-score**
- **0.758 ROC-AUC**

The model performed strongly on the majority non-default class, but its recall for the default class was substantially lower.

This means that although the model was reasonably accurate overall, it failed to identify a considerable proportion of borrowers who actually defaulted.

---

### Decision Tree

The Decision Tree achieved:

- **89.1% accuracy**
- **73.8% precision**
- **77.3% recall**
- **75.5% F1-score**
- **0.848 ROC-AUC**

Compared with Logistic Regression, the Decision Tree achieved:

- Higher overall accuracy
- Higher recall
- Higher F1-score
- Higher ROC-AUC

Its precision was slightly lower than Logistic Regression.

The largest difference was in **recall**, where the Decision Tree achieved 77.3% compared with 56.4% for Logistic Regression.

This indicates that the Decision Tree was able to identify substantially more of the actual default cases in this dataset.

---

## Model Comparison

The results show an important trade-off between **predictive performance and interpretability**.

### Predictive Performance

The Decision Tree achieved stronger performance across the main evaluation metrics, particularly:

- Recall: **77.3% vs 56.4%**
- F1-score: **75.5% vs 64.9%**
- ROC-AUC: **0.848 vs 0.758**

The higher recall is particularly relevant for credit risk applications because missing genuine defaults can lead to financial losses.

### Interpretability

Logistic Regression retains important practical advantages.

Its coefficients provide a relatively straightforward way to understand how individual variables are associated with predicted default probability.

This can be valuable in financial institutions where model transparency, validation and governance are important.

Therefore, predictive performance should not be considered in isolation when selecting a credit risk model.

---

## Key Findings

The analysis suggests several important findings:

### 1. Accuracy alone is not sufficient

The dataset is imbalanced, with approximately 22% of observations belonging to the default class.

Therefore, a model can achieve relatively high accuracy while still failing to identify a meaningful proportion of actual defaults.

For this reason, recall and ROC-AUC are important complementary measures.

### 2. Decision Tree captured more default cases

The Decision Tree achieved substantially higher recall than Logistic Regression.

This suggests that the nonlinear structure of the Decision Tree helped capture relationships in the borrower and loan characteristics that were not fully represented by the linear Logistic Regression model.

### 3. Logistic Regression remained more interpretable

Although Logistic Regression produced weaker predictive performance in this experiment, its simpler structure provides advantages for explaining model decisions to stakeholders.

This is particularly relevant in regulated financial environments.

### 4. Model selection depends on the business objective

A model that performs better statistically is not automatically the best model for every financial institution.

Credit risk model selection should consider:

- Predictive performance
- Cost of false negatives
- Interpretability
- Model stability
- Regulatory requirements
- Model validation
- Governance requirements
- Deployment context

---

## Practical Credit Risk Implications

From a credit risk perspective, the difference in recall is particularly important.

The Logistic Regression model identified approximately **56% of actual defaults**, while the Decision Tree identified approximately **77%**.

This means the Decision Tree captured a substantially larger proportion of borrowers who belonged to the default class in the test set.

However, the Decision Tree also produced slightly lower precision.

Therefore, increasing default detection may come with an increase in false positive classifications.

In a real lending environment, this trade-off would need to be assessed against the financial cost of:

- approving a borrower who later defaults, and
- rejecting or reviewing a borrower who would have repaid successfully.

---

## Limitations

This project has several limitations that should be considered before using the models in a real lending environment.

### 1. Model selection

Only two classification algorithms were compared:

- Logistic Regression
- Decision Tree

More advanced approaches such as Random Forest, Gradient Boosting, XGBoost or ensemble methods could provide additional benchmarks.

### 2. Decision Tree overfitting risk

The Decision Tree model was not constrained by a maximum depth during model fitting.

Although it achieved strong test-set performance, a more comprehensive analysis should investigate:

- Cross-validation
- Hyperparameter tuning
- Maximum tree depth
- Minimum samples per split
- Minimum samples per leaf
- Pruning

### 3. Single train-test split

The analysis uses one stratified 80/20 train-test split.

Cross-validation would provide a more robust assessment of model stability.

### 4. Class imbalance

The default class represents a minority of observations.

The analysis focuses on recall and ROC-AUC, but additional techniques could be investigated, including:

- Class weighting
- Resampling
- SMOTE
- Cost-sensitive learning
- Threshold optimisation

### 5. Dataset limitations

The dataset represents a particular consumer lending population.

Model performance may change when applied to:

- Different customer populations
- Different geographical markets
- Different economic environments
- Different lending products
- Future loan cohorts

Therefore, strong performance on this dataset should not automatically be interpreted as evidence of production readiness.

---

## Technologies and Tools

The project was developed using Python and Jupyter Notebook.

### Python Libraries

- Python
- pandas
- NumPy
- matplotlib
- seaborn
- scikit-learn

### Machine Learning

- Logistic Regression
- Decision Tree Classifier
- StandardScaler
- Train-test split
- Classification metrics
- ROC-AUC

### Development Environment

The project was originally developed in Google Colab and subsequently reproduced in GitHub Codespaces using a Python virtual environment.
