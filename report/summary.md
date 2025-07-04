# Air Pollution Prediction in the United States (2020)

### Executive Summary

This project explores the relationships between air quality indicators and PM2.5 exceedance days across U.S. counties using the 2020 EPA dataset. Two predictive models – linear regression and random forest – are built and evaluated. The results show that in the PM2.5 prediction task, the random forest model performs better than the linear model, achieving higher accuracy and lower error indicators such as root mean square error (RMSE) and mean absolute value (MAE).

---

## 1. Project Objective

- Predict the number of days in a year where PM2.5 levels exceed safe thresholds (`Days PM2.5`).
- Compare the performance of linear model and random forest model.
- Generalize model performance by forecasting 2021 PM2.5 pollution levels.

---

## 2. Dataset Overview

**Source:** [EPA Air Quality Annual Summary (2020)](https://aqs.epa.gov/aqsweb/airdata/download_files.html#Annual)

- **Target Variable:**
  - `Days PM2.5` – Number of days with PM2.5 concentrations exceeding the regulatory threshold.
- **Predictor Variables:**
  - **AQI Metrics:** `Max AQI`, `90th Percentile AQI`, `Median AQI`
  - **Pollutant Days:** `Days CO`, `Days NO2`, `Days Ozone`, `Days PM10`
  - **Health-Based AQI Days:** `Unhealthy Days`, `Very Unhealthy Days`, `Hazardous Days`, `Good Days`, `Moderate Days`, `Unhealthy for Sensitive Groups Days`
  - **General Metadata:** `State`, `County`, `Year`, `Days with AQI`

---

## 3. Exploratory Data Analysis

### 3.1 Target Variable Distribution Analysis
To understand the distribution characteristics of the target variable, we examined PM2.5 exceedance days using multiple visualization techniques:

- **Histogram Analysis**: Created a distribution histogram of `Days.PM2.5` with 30 bins to visualize the frequency distribution and identify the overall shape of the data distribution.

<img src="figures\PM2.5_Days_Distribution.png" alt="PM2.5 Days Distribution" width="600">

- **Boxplot Analysis**: Generated a boxplot to examine the central tendency, spread, and presence of outliers in PM2.5 exceedance days across all observations.

<img src="figures\Boxplot_of_PM2.5_Days.png" alt="PM2.5 Days Distribution" width="600">

### 3.2 Correlation Analysis
Conducted correlation analysis to assess relationships between variables and identify potential multicollinearity issues:

- **Variable Selection**: Selected 14 relevant numeric variables for modeling including air quality metrics (`Good.Days`, `Moderate.Days`, `Unhealthy.Days`, etc.), AQI measurements (`Max.AQI`, `Median.AQI`, `X90th.Percentile.AQI`), and pollutant-specific days (`Days.CO`, `Days.NO2`, `Days.Ozone`, `Days.PM10`).

- **Correlation Matrix Visualization**: Generated a colored correlation plot using the corrplot package to visualize the strength and direction of correlations between all modeling variables.

<img src="figures\correlation_matrix.png" alt="Correlation Matrix" width="600">

### 3.3 Geographic Distribution Analysis
Analyzed the geographic variation in PM2.5 exceedance across different states:

- **State-level Aggregation**: Calculated average PM2.5 exceedance days for each state and ranked them in descending order to identify the most affected regions.

- **Comparative Visualization**: Created a horizontal bar chart displaying average PM2.5 days by state, providing insights into geographic patterns and regional air quality differences.

<img src="figures\pm25_by_state.png" alt="Average PM2.5 Days by State" width="600">

### Key Findings
- A significant negative correlation was identified between PM2.5 exceeding the standard and `Days Ozone`
- Revealed significant geographic variation in PM2.5 exceedance patterns across states
- Confirmed the suitability of selected variables (`Max.AQI`, `X90th.Percentile.AQI`, `Median.AQI`, `Days.CO`, `Days.NO2`, `Days.Ozone`, `Days.PM10`) for predictive modeling
---

## 4. Modeling Approach

### 4.1 Linear Regression

- Used multiple selected predictors to model `Days PM2.5`.
- Applied Variance Inflation Factor (VIF) to check for multicollinearity.
- Evaluated model on 30% held-out test data.
- Forecasted 2021 PM2.5 exceedance using 2020-trained model.

### 4.1 Linear Regression

- Used multiple selected predictors to model `Days PM2.5`.
- Applied Variance Inflation Factor (VIF) to check for multicollinearity.

| Variable | VIF Value |
|----------|-----------|
| Max.AQI | 1.57 |
| X90th.Percentile.AQI | 4.42 |
| Median.AQI | 3.85 |
| Days.CO | 1.04 |
| Days.NO2 | 1.03 |
| Days.Ozone | 1.15 |
| Days.PM10 | 1.10 |

- Evaluated model on 30% held-out test data.
- Forecasted 2021 PM2.5 exceedance using 2020-trained model.

<img src="figures\linear_regression_results.png" alt="Linear Regression Model Results" width="600">

### 4.2 Random Forest

- Trained using the same predictors as linear model.
- Tuned number of trees to optimize OOB error.

<img src="figures\rf_error_plot.png" alt="Random Forest OOB Error by Number of Trees" width="600">

- Visualized feature importance to interpret key factors.

<img src="figures\feature_importance.png" alt="Random Forest Feature Importance" width="600">

- Achieved improved performance on both 2020 test set and 2021 forecast.

<img src="figures\random_forest_results.png" alt="Random Forest Model Results" width="600">

---

## 5. Model Performance Summary

| Metric            | Linear Regression | Random Forest   |
|-------------------|-------------------|------------------|
| R² (2020 test set) | 0.69         | (fill in)        |
| R² (2021 forecast) | 0.72        | 0.83      |
| RMSE (2021 forecast)        | 66.31         | 51.62        |
| MAE (2021 forecast)         | 51.29         | 31.17       |


> The random forest model consistently outperformed the linear regression model, with better R² scores and lower prediction errors. It also generalized more effectively to 2021 data.

## 5. Model Performance Summary

| Metric            | Linear Regression | Random Forest   |
|-------------------|-------------------|-----------------|
| R² (2020 test set) | 0.69         | (fill in)        |
| R² (2021 forecast) | 0.72        | 0.83      |
| RMSE (2021 forecast)        | 66.31         | 51.62        |
| MAE (2021 forecast)         | 51.29         | 31.17       |

> The random forest model consistently outperformed the linear regression model, with better R² scores and lower prediction errors. It also generalized more effectively to 2021 data.

### Model Comparison Visualization

To further evaluate model performance, we generated actual vs. predicted scatter plots for both models using 2021 forecast data:

<img src="figures\linear_vs_actual.png" alt="Linear Regression: Actual vs Predicted" width="500">

<img src="figures\rf_vs_actual.png" alt="Random Forest: Actual vs Predicted" width="500">

The scatter plots reveal significant differences in predictive performance between the two models:

**Linear Regression Model:**
- Shows considerable scatter around the diagonal line, particularly in the mid-range values (100-300 days)
- Exhibits some systematic bias with predictions often deviating from the perfect prediction line
- Demonstrates reasonable performance but with notable prediction errors

**Random Forest Model:**
- Displays much tighter clustering around the diagonal line across all value ranges
- Shows more consistent predictions with reduced scatter
- Demonstrates superior performance especially for higher PM2.5 values (>200 days)
- Exhibits less systematic bias and more accurate predictions overall

These visualizations confirm the quantitative metrics, clearly demonstrating that the random forest model provides more reliable and accurate forecasts for PM2.5 exceedance days, making it the preferred choice for operational air quality forecasting.

---

## 6. Key Insights

### 6.1 Model Performance Comparison
- **Linear Regression**: R² = 0.686, residual standard error = 69.24
- **Random Forest**: 80.96% variance explained, mean squared residual = 2839.426
- Random forest significantly outperformed linear regression in 2021 forecasts (R² 0.83 vs 0.72, RMSE 51.62 vs 66.31)

### 6.2 Key Predictors
**Linear Regression Coefficients:**
- **Max.AQI**: +0.114 (highly significant, p < 2e-16)
- **Median.AQI**: +3.128 (strong positive effect, p = 2.22e-11)
- **Days.CO, Days.NO2, Days.Ozone, Days.PM10**: All negative coefficients

*Note: Negative coefficients for pollutant-specific days likely reflect that when other pollutants dominate (CO, NO2, Ozone, PM10), PM2.5 days may be relatively fewer, suggesting different pollution patterns or seasonal effects.*

### 6.3 Model Insights
- **Non-linear relationships**: Random forest captured 12% more variance than linear regression, indicating complex interactions between air quality variables
- **AQI metrics** emerged as the strongest predictors for PM2.5 exceedance
- Random forest provides more reliable forecasting for operational air quality management

### 6.4 Practical Value
The random forest model offers robust PM2.5 forecasting capabilities with high accuracy, supporting proactive air quality management and public health protection.

---

## 7. Tools and Environment

- **Language:** R
- **Key Libraries:** 
  - `tidyverse`: Data manipulation and visualization
  - `randomForest`: Random forest modeling
  - `caret`: Model training and evaluation
  - `ggplot2`: Data visualization
  - `corrplot`: Correlation matrix visualization
  - `car`: Variance Inflation Factor (VIF) analysis
- **Platform:** Google Colab (R kernel)

---

## 8. Project Files

- `notebook/AirPollution_US_2020_Analysis.ipynb` – Full code, visualizations, and modeling steps
- `report/summary.md` – This summary report
- `figures/` – Exported visualizations
- `README.md` – Project overview and usage instructions

---

## 9. About the Author

- **Name:** Jing
- **Background:** Master's student in Information Technology (NSW, Australia)
- **Focus:** Data Analytics, Business Intelligence
- **Goal:** Seeking internship or graduate roles in data analysis