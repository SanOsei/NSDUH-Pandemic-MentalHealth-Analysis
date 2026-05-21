# Pandemic-Era Shifts in Drug-Substance Co-occurrence and Mental Illness Risk (2020–2024)
## Project Overview
This project performs an extensive exploratory data analysis (EDA) and statistical modeling on national public health survey data across a five-year period (2020–2024). The primary objective is to evaluate the epidemiological trends and associations between Substance Use (Tobacco, Alcohol, and illicit Drugs) and various Mental Health Outcomes, including:
- Any Mental Illness (AMI)
- Serious Mental Illness (SMI)
- Major Depressive Episode (MDE)
- Major Depressive Episode with Severe Role Impairment (MDE_SevereImpairment)

The pipeline integrates both unweighted sample statistics and survey-weighted analyses to ensure the findings accurately reflect broader population estimates while accounting for complex survey designs.

## Data Pipeline & Notebook Structure
1. Environment Setup & Data Ingestion
- Mounts Google Drive to access the dataset directories.
- Loads separate cross-sectional annual survey data modules from 2020 to 2024.
- Standardizes varying variable schemas and maps complex weight features across waves (e.g., handling variable transformations from ANALWTQ1Q4_C to ANALWT2_C).

2. Data Cleaning & Standardization
- Filters and harmonizes demographic variables including Sex, Race, Age Groups (binned neatly into 18-25, 26-34, 35-49, 50-64, 65+), Household Poverty Status, and Family Income.
- Standardizes binary outcomes for substance use and psychological distress indicators, filtering out missing data values and system invalid codes.
- Outputs a finalized, clean analysis file: nsduh_2020_2024_final_standardized.csv.

3. Exploratory Data Analysis (EDA) & Data Visualization
- Generates unweighted and survey-weighted descriptive metrics saved automatically to your Drive (/EDA_Figures/). Visualizations include:
- Prevalence bar plots of mental health outcomes and substance use.
- Chronological trend tracking lines over the 2020–2024 timeline.
- Demographic stratifications (Mental health trends across Sex, Income, and Poverty brackets).
- Comparative Weighted vs. Unweighted Pearson correlation matrix heatmaps.

4. Advanced Statistical Modeling (Logistic Regression)
Employs statsmodels.formula.api to construct robust multi-variable Generalized Linear Models (GLM) using a Binomial family link:
- Main Effects Models: Quantifies Adjusted Odds Ratios (AOR) for Tobacco, Alcohol, and Drug use relative to mental health conditions while strictly controlling for socio-demographic confounders.
- Interaction Models: Evaluates the temporal variations of substance use impacts over time using year interaction terms (Substance * C(YEAR)).
- Likelihood Ratio Tests (LRT): Executes Chi-Squared nested model comparisons to statistically validate the inclusion of year-interaction dynamics.
- Forest Plots: Generates presentation-ready odds ratio charts plotting final risk estimates with corresponding 95% Confidence Intervals (CI).

## Technical Stack & Dependencies
The notebook runs completely on a standard Python 3 runtime environment. Ensure the following packages are configured:
```python
!pip install pyreadstat statsmodels pandas numpy matplotlib scipy
```
- Pandas & NumPy: Data wrangling, category processing, and numeric parsing.

- Statsmodels: GLM implementation using frequency weighting overrides (freq_weights) and heteroscedasticity-robust standard errors (HC1).

-Matplotlib: Scientific data visualization and forest plotting.

-SciPy: Advanced statistical testing (Chi-squared survival functions for LRT calculations).

## How to Execute the Notebook
1. Mount Drive: Ensure your Google Drive contains the source dataset paths matching "/content/drive/MyDrive/CSV_FILES_PSM691/".

2. Run All Cells: Navigate to the Colab toolbar and select Runtime > Run All (or Ctrl + F9).

3. Inspect Results: Check your mounted directory for generated summary tables (.csv) and visual trend matrices stored automatically inside your Regression_Results/ and EDA_Figures/ outputs folders.
