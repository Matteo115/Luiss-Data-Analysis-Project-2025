# MLB Salary Prediction using Multinomial Logistic Regression

This repository contains an **R Markdown** analysis that builds and evaluates a **Multinomial Logistic Regression** model to predict **baseball players’ salary levels** (Low / Medium / High) using performance and categorical predictors.

The main file is:

- `ProjectWork_DataBros.Rmd` — the full report (EDA + modeling + evaluation + improvement steps)

---

## What this project does

The R Markdown document is organized into three main parts:

### 1) Overview (Theory)
A short introduction to **multinomial logistic regression**, explaining when it is used (response variable with 3+ classes) and the intuition behind the model.

### 2) Exploratory Data Analysis (EDA)
Steps performed on the dataset include:

- **Load data** from `Hitters.csv`
- **Summary statistics** (numeric + categorical)
- **Missing values handling** (rows with missing values are removed)
- **Factor conversion** for categorical predictors
- **Target engineering**:
  - The numeric variable `Salary` is discretized into 3 classes using salary **terciles**:
    - `LowSalary`, `MediumSalary`, `HighSalary`
- Visual exploration:
  - Barplots for categorical variables (`League`, `Division`, `NewLeague`, `SalaryLevel`)
  - Distribution summaries for numeric predictors
  - **Correlation heatmap** for numeric variables

### 3) Model & Performance + Improvements
The workflow includes:

- **Data split** into:
  - training / validation / test (with fixed random seeds for reproducibility)
- **Baseline model**:
  - Multinomial regression with **all predictors** (`SalaryLevel ~ .`)
- **Evaluation methods**:
  - “Vanilla” validation accuracy
  - Manual **5-fold cross-validation**
  - Test set evaluation with:
    - **Confusion matrix**
    - Per-class metrics computed manually:
      - Sensitivity, Specificity, Precision
    - Overall Accuracy

#### Model improvement
Two simplification strategies are implemented:

1. **Significance-based feature removal**
   - Removes predictors with high p-values / low z-scores (as identified from the full model output), e.g.:
     - `Hits`, `RBI`, `CRBI`, `CHmRun`, `CRuns`, `Runs`

2. **Backward elimination (wrapper approach)**
   - A custom backward-selection routine that iteratively removes features based on accuracy impact.
   - Includes additional evaluation with cross-validation for the selected formula.

---

## Dataset

This project expects a CSV file named:

- `Hitters.csv`

It should contain at least:
- A numeric salary column: `Salary`
- Baseball performance metrics (numeric)
- Categorical variables such as `League`, `Division`, `NewLeague` (used in the plots and modeling)

> Note: The report removes rows with missing values before modeling.

---

## Requirements

### Software
- R (recommended: recent version)
- RStudio (recommended for knitting `.Rmd`)

### R packages used
The script loads these libraries:

- `dplyr`
- `ggplot2`
- `tidyr`
- `corrplot`
- `caret`
- `nnet` (for `multinom()`)

Install them with:

```r
install.packages(c("dplyr", "ggplot2", "tidyr", "corrplot", "caret", "nnet"))

   git clone [https://github.com/YOUR_USERNAME/MLB-Salary-Prediction-Multinomial-Regression.git](https://github.com/YOUR_USERNAME/MLB-Salary-Prediction-Multinomial-Regression.git)
