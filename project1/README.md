# Customer Churn Prediction with Logistic Regression

## Goal

This project predicts customer churn for a telecommunications company and identifies the key factors that drive churn risk. The objective is to build an interpretable model that can be used to:

- Flag high-risk customers for retention campaigns, and  
- Understand which customer characteristics and contract features are most strongly associated with churn.

Although the context is telecom, the approach is directly applicable to player churn in games (who is likely to stop playing and why).

## Data

- **Source:** Telco customer dataset.
- **Unit of analysis:** Individual customers.
- **Target variable:** `Churn` (Yes/No).
- **Features (selected examples):**
  - Demographics: `gender`, `SeniorCitizen`, `Dependents`, `Partner`
  - Tenure and billing: `tenure`, `MonthlyCharges`, `TotalCharges`, `PaymentMethod`, `PaperlessBilling`
  - Services and contract type: `PhoneService`, `StreamingMovies`, `Contract` (month-to-month, one year, two year)

## Methods & Tools

- **Language:** R
- **Key packages:** `tidyverse`, `broom`, `performance`, `gt`, `kableExtra`, `ggplot2`
- **Steps:**
  1. **Data preparation**
     - Converted character variables to factors.
     - Checked and handled missing values.
     - Created a clean modelling dataset with relevant predictors.
  2. **Initial logistic regression**
     - Fitted a full binomial logistic regression model with all candidate predictors.
     - Interpreted coefficients and odds ratios for churn.
  3. **Multicollinearity diagnostics**
     - Used Variance Inflation Factors (VIF) to assess collinearity.
     - Identified highly collinear variables (`TotalCharges`, `tenure`) and simplified the model accordingly.
  4. **Reduced logistic regression model**
     - Built a more parsimonious model including:
       - `MonthlyCharges`, `tenure`, `SeniorCitizen`, `PhoneService`, `StreamingMovies`,
         `Contract`, `PaperlessBilling`, `PaymentMethod`, `Partner`, `Dependents`, `gender`.
     - Evaluated statistical significance and directions of effects.
  5. **Risk scoring**
     - Computed predicted churn probabilities for each customer.
     - Generated ranked lists of:
       - Top 10 customers with **highest** predicted churn risk.
       - Top 10 customers with **lowest** predicted churn risk.
     - Summarised results in formatted tables.

## Key Insights

- **Customer tenure** has a strong negative effect on churn: longer relationships are associated with substantially lower churn risk.
- **Contract type** is a major driver: one-year and two-year contracts reduce the odds of churn compared with month-to-month contracts.
- **Phone service and bundled services** are associated with lower churn risk, suggesting that offering additional services helps retain customers.
- The model effectively separates high- and low-risk groups: the high-risk list contains many customers who actually churned, while the low-risk list is dominated by stable customers.
- These insights translate into clear managerial actions, such as promoting longer-term contracts and bundled service offerings to reduce churn.

## Files

- `analysis.Rmd` – full R code for the churn analysis:
  - data cleaning and preparation  
  - logistic regression models  
  - VIF diagnostics and reduced model  
  - predicted probabilities and ranked churn lists
