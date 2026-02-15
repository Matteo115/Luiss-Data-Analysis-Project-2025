# MLB Salary Prediction using Multinomial Logistic Regression

## Team Group
* Matteo Bruni
* Matteo Rapisarda
* Federico Romano Gargarella

## Project Overview
This project focuses on the application of **Multinomial Logistic Regression** to predict baseball players' salary levels based on their performance statistics. Unlike binary logistic regression, this model handles outcomes with more than two categories, classifying players into **Low**, **Medium**, or **High** salary tiers.

The analysis aims to construct a predictive model, evaluate its performance using various validation techniques, and optimize it through feature selection to improve generalization and interpretability.

## Dataset
The project utilizes the **Hitters.csv** dataset.
* **Original Dimensions:** 317 observations, 20 variables.
* **Preprocessing:**
    * Removed 58 rows containing missing values (NAs) in the target `Salary` column.
    * Final dataset size: **259 rows**.
* **Target Variable:** `Salary` was discretized into a categorical variable `SalaryLevel` (LowSalary, MediumSalary, HighSalary) based on quantiles.
* **Features:** Includes performance metrics such as `AtBat`, `Hits`, `Home Runs`, `Years`, and categorical variables like `League` and `Division`.

## Methodology

### 1. Exploratory Data Analysis (EDA)
* **Data Cleaning:** Handling missing values and ensuring correct data types (factorizing categorical variables).
* **Visualization:** Analyzed distributions of categorical variables (League, Division) and numerical predictors using histograms.
* **Correlation Analysis:** A heatmap was generated to identify multicollinearity among predictors, revealing strong correlations between career totals (e.g., `CAtBat`, `CHits`).

### 2. Modeling Strategy
* **Model Type:** Multinomial Logistic Regression (using the `nnet` package).
* **Validation Techniques:**
    * **Vanilla Validation:** Splitting data into Training, Validation, and Test sets (70% Training / 30% Test).
    * **K-Fold Cross-Validation:** Utilized **K=5** to ensure robust performance estimation.
    * **Random Seed:** Set to `26091998` for reproducibility.

### 3. Model Improvement
* **Feature Selection:** Variables with high p-values and low Wald z-statistics (e.g., `Hits`, `RBI`, `Runs`) were removed to reduce noise.
* **Backward Stepwise Selection:** An algorithmic approach was used to iteratively remove predictors to maximize accuracy and minimize AIC.

## Results and Performance
The project compared a "Full Model" (all predictors) against an "Improved Model" (reduced predictors). The improved model demonstrated better generalization and efficiency.

| Metric | Full Model | Improved Model |
| :--- | :--- | :--- |
| **Test Accuracy** | 61.8%  | **64.5%**  |
| **5-Fold CV Accuracy** | 59.2%  | **64.7%**  |
| **AIC** (Lower is better) | 264.13  | **255.02**  |

**Key Findings:**
* The simplified model achieved higher accuracy on unseen data.
* The model performed well in identifying **Low** and **High** salary players but faced some difficulty distinguishing **Medium** salary players due to class overlap.
* High specificity (>0.80) across all classes indicates a low false-positive rate.

## Requirements
To run this analysis, the following R libraries are required:

```r
library(tidyr)
library(dplyr)
library(ggplot2)
library(caret)
library(nnet)
library(corrplot)
