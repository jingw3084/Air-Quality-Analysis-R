# Air Pollution Prediction in the United States (2020)

## 📋 Project Overview

This project analyzes air quality data from the EPA to predict PM2.5 exceedance days across U.S. counties. Using machine learning techniques, we compare linear regression and random forest models to forecast air pollution patterns and support public health decision-making.

## 🎯 Objectives

- Predict the number of days per year where PM2.5 levels exceed safe thresholds
- Compare performance between linear regression and random forest models
- Evaluate model generalization by forecasting 2021 PM2.5 pollution levels
- Identify key predictors for PM2.5 exceedance patterns

## 📊 Dataset

**Source:** [EPA Air Quality Annual Summary (2020)](https://aqs.epa.gov/aqsweb/airdata/download_files.html#Annual)

- **Target Variable:** `Days PM2.5` – Number of days with PM2.5 concentrations exceeding regulatory thresholds
- **Key Predictors:** AQI metrics, pollutant-specific days, health-based AQI categories
- **Coverage:** U.S. counties, 2020 data

## 🔍 Key Findings

- **Random Forest outperformed Linear Regression:**
  - R² improvement: 0.83 vs 0.72 (2021 forecast)
  - RMSE reduction: 51.62 vs 66.31
  - MAE reduction: 31.17 vs 51.29

- **Most Important Predictors:**
  - Max AQI
  - Median AQI
  - Days with other pollutants (CO, NO2, Ozone, PM10)

- **Geographic Variation:** Significant differences in PM2.5 exceedance patterns across states

## 🛠️ Technologies Used

- **Language:** R
- **Environment:** Google Colab
- **Key Libraries:**
  - `tidyverse` - Data manipulation and visualization
  - `randomForest` - Random forest modeling
  - `caret` - Model training and evaluation
  - `ggplot2` - Data visualization
  - `corrplot` - Correlation analysis
  - `car` - Variance Inflation Factor analysis

## 📁 Project Structure

```
air-pollution-prediction/
├── notebook/
│   └── AirPollution_US_2020_Analysis.ipynb
├── report/
│   └── summary.md
├── figures/
│   ├── PM2.5_Days_Distribution.png
│   ├── correlation_matrix.png
│   ├── pm25_by_state.png
│   ├── linear_vs_actual.png
│   └── rf_vs_actual.png
└── README.md
```

## 🚀 Getting Started

### Prerequisites
- R (version 4.0 or higher)
- Google Colab account (recommended)

### Installation
1. Clone this repository:
```bash
git clone https://github.com/yourusername/air-pollution-prediction.git
cd air-pollution-prediction
```

2. Install required R packages:
```r
install.packages(c("tidyverse", "randomForest", "caret", "ggplot2", "corrplot", "car"))
```

3. Open the Jupyter notebook in Google Colab or your preferred environment

### Running the Analysis
1. Load the EPA dataset (2020 Air Quality Annual Summary)
2. Run the exploratory data analysis sections
3. Execute the modeling pipeline (Linear Regression + Random Forest)
4. Generate visualizations and performance metrics

## 📈 Model Performance

| Metric | Linear Regression | Random Forest |
|--------|-------------------|---------------|
| R² (2021 forecast) | 0.72 | 0.83 |
| RMSE (2021 forecast) | 66.31 | 51.62 |
| MAE (2021 forecast) | 51.29 | 31.17 |

## 📊 Key Visualizations

- **Distribution Analysis:** Histograms and boxplots of PM2.5 exceedance days
- **Correlation Matrix:** Relationships between air quality variables
- **Geographic Analysis:** State-level PM2.5 patterns
- **Model Comparison:** Actual vs. predicted scatter plots
- **Feature Importance:** Random forest variable importance rankings

## 🔬 Methodology

1. **Data Preprocessing:** Variable selection, missing value handling, train/test split
2. **Exploratory Analysis:** Distribution analysis, correlation assessment, geographic patterns
3. **Model Development:** Linear regression with VIF analysis, Random forest with hyperparameter tuning
4. **Evaluation:** Cross-validation, out-of-sample testing, 2021 forecast validation

## 📝 Results & Insights

- Random forest successfully captured non-linear relationships in air quality data
- AQI metrics emerged as the strongest predictors for PM2.5 exceedance
- Geographic analysis revealed significant regional variation in pollution patterns
- Model provides reliable forecasting capabilities for operational air quality management

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👤 Author

**Jing**
- Master's student in Information Technology (NSW, Australia)
- Focus: Data Analytics, Business Intelligence
- Seeking internship/graduate roles in data analysis

## 📧 Contact

For questions or collaboration opportunities, please reach out via GitHub issues or email.

## 🙏 Acknowledgments

- EPA for providing comprehensive air quality data
- Google Colab for computational resources
- R community for excellent machine learning libraries