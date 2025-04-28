# Forecasting Individual Household Electric Power Consumption

Authors: Catherine Hua, Lyric Li, Anni Zheng
Affiliation: New York University
Course: Probabilistic Time Series Analysis, Fall 2024


⸻

**Project Overview
**
This project explores predictive modeling of household electric power consumption using three distinct approaches:
	•	Statistical model: ARIMA
	•	Machine learning model: XGBoost
	•	Deep learning model: LSTM

The objective is to identify the model that best captures temporal and seasonal patterns in energy usage data. We focus on improving forecasting accuracy to support energy management, optimize resource distribution, and promote sustainable practices.

Through a series of preprocessing, feature engineering, modeling, and evaluation steps, we benchmarked model performance using RMSE and R-squared metrics. Among the models tested, LSTM on the full dataset achieved the best predictive performance.

⸻

**Dataset**

We use the Individual Household Electric Power Consumption dataset from UCI Machine Learning Repository.
Key facts:
	•	Location: Sceaux, France (7 km from Paris)
	•	Time span: December 2006 – November 2010
	•	Measurements: 9 attributes including active/reactive power, voltage, intensity, and sub-metering for different appliances
	•	Sampling rate: 1-minute intervals (aggregated to hourly for this project)

For modeling:
	•	We selected a 2-year period for training and testing.
	•	The dataset was aggregated to hourly intervals to manage complexity and highlight daily/seasonal trends.

⸻

**Methods**

ARIMA
	•	Focused on seasonal trends using differencing and autocorrelation analysis.
	•	Identified optimal (p, d, q) and seasonal parameters via ACF, PACF, and iterative testing.
	•	Best model: ARIMA(1, 0, 1)(1, 1, 1)[48]

XGBoost
	•	Applied feature engineering, adding features like is_weekend, is_holiday, and day_of_week.
	•	Constructed time-based lag features to improve sequential learning, while avoiding data leakage.
	•	Tuned hyperparameters: 30 tree depth, 0.01 learning rate, 1000 epochs.

LSTM
	•	Built RNN models to capture long-term dependencies.
	•	Baseline model used hourly active power.
	•	Enhanced model with additional features (is_weekend, is_holiday).
	•	Final best-performing model trained on the full global active power dataset (~1M records) with adjusted dropout to handle large input size.
 
⸻

**Results**

| Model                        | R² Score | Test RMSE |
|-------------------------------|:--------:|----------:|
| ARIMA                         | 0.151    | 0.8757    |
| XGBoost                       | 0.25     | 0.822     |
| LSTM (hourly active power)     | 0.2029   | 0.8487    |
| LSTM (with feature engineering)| 0.2175   | 0.8409    |
| **LSTM (global active power)** | **0.8412** | **0.3745** |


Key findings:
	•	LSTM (global active power) achieved the highest R² and lowest RMSE.
	•	ARIMA struggled with non-linearities and unexpected spikes.
	•	XGBoost captured general trends but faced challenges modeling sequential dependencies.
	•	LSTM was the most flexible but prone to overfitting on large datasets.

⸻

**Future Work**
	•	Introduce anomaly detection and data augmentation to better handle sudden shifts in patterns.
	•	Incorporate validation monitoring during training to address overfitting.
	•	Expand models to broader datasets beyond a single household (e.g., web traffic, weather data).
	•	Explore transformer-based time series models for further improvement.

