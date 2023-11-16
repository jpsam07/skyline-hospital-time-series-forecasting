# Skyline Hospital Time Series Forecasting with XGBoost

![https://www.facebook.com/SkylineHospitalAndMedicalCenter](./pictures/skyline_hospital_banner.jpg)

**Source:** [Facebook Page](https://www.facebook.com/SkylineHospitalAndMedicalCenter)

This is a data analysis project that aims to forecast future patient arrivals data on the outpatient unit of Skyline Hospital and Medical Center. This is a dedicated repository for the data analytics feature of the [appointment management system](thesis-manuscript/appointment_management_system_thesis.pdf) for our bachelor's degree thesis.

The data analysis workflow can be outlined as follows:

**1. Data Collection**

- Hospital sent us daily time series data of patient arrivals in a csv file through email
- The time series data time frame was from May 18, 2020 to December 31, 2022.

**2. Loading the data and environment setup**: The time series data was loaded into Jupyter Lab using Python. Relevant libraries for data analysis were also imported:

- `pandas`: for Data Management and Data Manipulation
- `numpy`: for numerical and scientific computing
- `matplotlib`, `seaborn`, `plotly`: for data visualization
- `sklearn.metrics` (scikit-learn): for model evaluation metrics such as RMSE, MAPE, and SMAPE
- `xgboost.XGBRegressor`: a gradient boosting type decision tree machine learning algorithm used for time series forecasting
- `TimeSeriesSplit`: for time series cross-validation

**3. Data Cleaning:** The data cleaning methods used in here include:

-  Merging duplicate dates with corresponding patient arrival counts
- Outlier analysis
- Missing value imputation

**4. Feature Engineering**

- Added time series features (e.g., day of week, day of year, month, etc.)
- Added rolling statistics and quantiles

**5. Time Lags Creation**

- Added lags in time to let the XGBoost Regressor model learn historical values and the temporal structure of the data.

**6. Time Series Cross-validation**

- Made use of `TimeSeriesSplit` for expanding window cross-validation
- Created training and testing (validation) sets

**7. Model Fitting, Forecasting, and Evaluation**

- Fit the XGBoost model on the training and testing data
- Trained on the training set, and validated on the testing set
- Generated future patient arrival forecasts
- Evaluated the model with performance metrics across all the folds with root mean squared error (RMSE), mean absolute percentage error (MAPE), and symmetric mean absolute percentage error (sMAPE).

---

Two Jupyter Notebooks here have proposed two solutions:

- [Solution 1](Skyline_Hospital_Time_Series_Forecasting_with_XGBoost_Solution_1.ipynb) discarded the point in time where the missing values have stopped appearing, and built the XGBoost forecasting model from there.
- [Solution 2](Skyline_Hospital_Time_Series_Forecasting_with_XGBoost_Solution_2.ipynb) used missing value imputation using linear interpolation to estimate the missing values, and used winsorization to adjust data points that deviate too much from the distribution. Then the XGBoost model was built from there.