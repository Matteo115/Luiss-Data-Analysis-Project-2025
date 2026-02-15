# MLB Salary Prediction using Multinomial Logistic Regression

## Project Overview
[cite_start]This project focuses on the application of **Multinomial Logistic Regression** to predict baseball players' salary levels based on their performance statistics. [cite_start]Unlike binary logistic regression, this model handles outcomes with more than two categories, classifying players into **Low**, **Medium**, or **High** salary tiers.

[cite_start]The analysis aims to construct a predictive model, evaluate its performance using various validation techniques, and optimize it through feature selection to improve generalization and interpretability.

## Dataset
[cite_start]The project utilizes the **Hitters.csv** dataset.
* [cite_start]**Original Dimensions:** 317 observations, 20 variables.
* **Preprocessing:**
    * [cite_start]Removed 58 rows containing missing values (NAs) in the target `Salary` column.
    * [cite_start]Final dataset size: **259 rows**.
* [cite_start]**Target Variable:** `Salary` was discretized into a categorical variable `SalaryLevel` (LowSalary, MediumSalary, HighSalary) based on quantiles.
* [cite_start]**Features:** Includes performance metrics such as `AtBat`, `Hits`, `Home Runs`, `Years`, and categorical variables like `League` and `Division`.

## Methodology

### 1. Exploratory Data Analysis (EDA)
* [cite_start]**Data Cleaning:** Handling missing values and ensuring correct data types (factorizing categorical variables).
* [cite_start]**Visualization:** Analyzed distributions of categorical variables (League, Division) and numerical predictors using histograms.
* [cite_start]**Correlation Analysis:** A heatmap was generated to identify multicollinearity among predictors, revealing strong correlations between career totals (e.g., `CAtBat`, `CHits`).

### 2. Modeling Strategy
* [cite_start]**Model Type:** Multinomial Logistic Regression (using the `nnet` package).
* **Validation Techniques:**
    * [cite_start]**Vanilla Validation:** Splitting data into Training, Validation, and Test sets (70% Training / 30% Test).
    * [cite_start]**K-Fold Cross-Validation:** Utilized **K=5** to ensure robust performance estimation.
    * [cite_start]**Random Seed:** Set to `26091998` for reproducibility.

### 3. Model Improvement
* [cite_start]**Feature Selection:** Variables with high p-values and low Wald z-statistics (e.g., `Hits`, `RBI`, `Runs`) were removed to reduce noise.
* [cite_start]**Backward Stepwise Selection:** An algorithmic approach was used to iteratively remove predictors to maximize accuracy and minimize AIC.

## Results and Performance
The project compared a "Full Model" (all predictors) against an "Improved Model" (reduced predictors). The improved model demonstrated better generalization and efficiency.

| Metric | Full Model | Improved Model |
| :--- | :--- | :--- |
| **Test Accuracy** | [cite_start]61.8%  | [cite_start]**64.5%**  |
| **5-Fold CV Accuracy** | [cite_start]59.2%  | [cite_start]**64.7%**  |
| **AIC** (Lower is better) | [cite_start]264.13  | [cite_start]**255.02**  |

**Key Findings:**
* [cite_start]The simplified model achieved higher accuracy on unseen data.
* [cite_start]The model performed well in identifying **Low** and **High** salary players but faced some difficulty distinguishing **Medium** salary players due to class overlap.
* [cite_start]High specificity (>0.80) across all classes indicates a low false-positive rate.

## 💻 Requirements
[cite_start]To run this analysis, the following R libraries are required:

```r
library(tidyr)
library(dplyr)
library(ggplot2)
library(caret)
library(nnet)
library(corrplot)
