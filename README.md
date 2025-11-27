 Advanced Time-Series Power Demand Forecasting (Valencia)

Project Overview

This repository provides an individual enhancement of a collaborative project focused on predicting electrical load (energy consumption). The core challenge involved modeling complex temporal dependencies to meet a critical utility requirement: accurate forecasting of the Daily Peak Load (Maximum Total Load).

The final model achieved an exceptional 98.38% $R^2$ score by focusing on robust time-series feature engineering and ensemble methods.

🎯 Key Findings & Results Summary

| Model | Target | Test RMSE | Test R-squared | 
| ----- | ----- | ----- | ----- | 
| **Random Forest Regressor (RFR)** | **Daily Peak Load (Max MW)** | **397.23 MW** | **0.9838** | 
| XGBoost Regressor (Baseline) | Daily Peak Load (Max MW) | 411.39 MW | 0.9825 |

📈 Methodology and Feature Importance

The success of the model relied on adapting classical ML to a time-series context:

1. Data Preparation and Feature Engineering

Time-Series Split: The data was split strictly chronologically (training on the past, testing on the future) to avoid data leakage.

Critical Features (Top Statistical Predictors): The correlation analysis confirmed that the model’s predictive power comes from engineered historical features. The following features showed the strongest linear relationship with the Daily Peak Load (sorted by absolute correlation):

total load forecast ($\approx 0.99$) - The single most dominant feature (utility forecast).

Lag_24 ($\approx 0.41$) - Yesterday's peak load.

generation fossil gas ($\approx 0.49$) - Strong link to peak generation needs.

DayOfWeek ($\approx 0.33$) - Captures the difference between weekday and weekend usage.

generation fossil oil ($\approx 0.43$) - Secondary link to peak generation.

generation fossil hard coal ($\approx 0.35$) - Baseline generation link.

Data Integrity: Handled missing values using Forward Fill (ffill) for the target variable and systematically dropped unreliable features (columns with $>90\%$ missing data) to maintain model stability.

2. Model Selection (Homogeneous Ensemble)

Model Choice: A Random Forest Regressor (RFR) was chosen over the XGBoost Regressor as the final model because it exhibited lower RMSE and better generalization on the unseen test data.

Business Pivot: Successfully converted hourly data to daily data using the .resample('D').max() function to align with the stakeholder requirement for peak load forecasting.

🔭 Future Work and Data Requirements

To enhance the model’s performance and robustness for production deployment, the following steps are recommended:

Model Enhancement (Deep Learning): The next logical step is to explore LSTM (Long Short-Term Memory) Neural Networks. 

 LSTMs are specialized for sequential data and may capture subtle, non-linear dependencies over the 5-year forecast horizon better than tree-based models.

External Data Integration (Data Enrichment): For efficient and robust forecasting, providing additional external data points is critical:

Weather Data (Temperature, Cloud Cover) - Crucial for explaining peak load variability.

Area Population Data (Economic/Demographic shifts).

Energy Consumption History for Appliances (Understanding peak load drivers).

Utility Bills Pricing Data (Impact of price on demand).

📚 Project Origin & Citation

This repository is a fork of the original work by [ShreyasLengade](https://github.com/ShreyasLengade/Energy-Consumption-Forecasting). The dataset and initial time-series structure were adapted from the original notebook, with substantial enhancements in feature engineering, cleaning, and model comparison detailed above.