# Skyline Hospital Time Series Forecasting with XGBoost

![https://www.facebook.com/SkylineHospitalAndMedicalCenter](./pictures/skyline_hospital_banner.jpg)

**Photo Source:** [Facebook Page](https://www.facebook.com/SkylineHospitalAndMedicalCenter)

This is a data analysis project that aimed to forecast future patient arrivals data on the outpatient unit of Skyline Hospital and Medical Center. This is a dedicated repository for the data analytics feature of the [appointment management system](thesis-manuscript/appointment_management_system_thesis.pdf) for our bachelor's degree thesis.

The data analysis workflow can be outlined as follows:

- [Data Collection](#data-collection)
- [Environment Setup and Data Loading](#environment-setup-and-data-loading)
- [Data Cleaning](#data-cleaning)
- [Feature Engineering](#feature-engineering)
- [Time Lags Creation](#time-lags-creation)
- [Time Series Cross Validation](#time-series-cross-validation)
- [Model Fitting, Forecasting, and Evaluation](#model-fitting-forecasting-and-evaluation)
- [Solution Selection](#solution-selection)

## Data Collection

- Hospital sent daily time series data of patient arrivals in a csv file through email
- The time series data time frame was **from May 18, 2020 to December 31, 2022.**

## Environment Setup and Data Loading

The time series data was **loaded into Jupyter Lab using Python**. Relevant libraries for data analysis were also imported:

- `pandas`: for Data Management and Data Manipulation
- `numpy`: for numerical and scientific computing
- `matplotlib`, `seaborn`, `plotly`: for data visualization
- `sklearn.metrics` (scikit-learn): for model evaluation metrics such as RMSE, MAPE, and SMAPE
- `xgboost.XGBRegressor`: a gradient boosting type decision tree machine learning algorithm used for time series forecasting
- `TimeSeriesSplit`: for time series cross-validation

## Data Cleaning

The data cleaning methods used in here include:

-  Merging duplicate dates with corresponding patient arrival counts
- Outlier analysis
- Missing value imputation

## Feature Engineering

- Added time series features (e.g., day of week, day of year, month, etc.)
- Added rolling statistics and quantiles

## Time Lags Creation

- Added lags in time to let the XGBoost Regressor model learn historical values and the temporal structure of the data.

## Time Series Cross Validation

- Made use of `TimeSeriesSplit` for expanding window cross-validation
- Created training and validation sets

## Model Fitting, Forecasting, and Evaluation

- Fit the XGBoost model on the training
- Validated on the testing set
- Generated future patient arrival forecasts
- Evaluated the model with performance metrics across all the folds with root mean squared error (RMSE), mean absolute percentage error (MAPE), and symmetric mean absolute percentage error (sMAPE).

---

## Solution Selection

- [Solution 1](https://nbviewer.org/github/jpsam07/skyline-hospital-time-series-forecasting-with-xgboost/blob/0e4cbc6abc432b8f6b2d1a347240c293a1fe6deb/Solution_1.ipynb) discarded the point in time where the missing values have stopped appearing, and built the XGBoost forecasting model from there.
- [Solution 2](https://nbviewer.org/github/jpsam07/skyline-hospital-time-series-forecasting-with-xgboost/blob/0e4cbc6abc432b8f6b2d1a347240c293a1fe6deb/Solution_2.ipynb) used missing value imputation using linear interpolation to estimate the missing values, and used winsorization to adjust data points that deviate too much from the distribution. Then the XGBoost model was built from there. **This is the favorable solution as the forecast more closely resembles the temporal structure of the time series data** compared to Solution 1.