#  Power Consumption Prediction in Wellington (Zone 1) 

This project focuses on predicting power consumption in Zone 1 of **Wellington, New Zealand**, using environmental and meteorological data. It involves data cleaning, feature engineering, model building, and evaluation using regression techniques.

---

##  Objective

To build a machine learning model that accurately predicts power consumption based on environmental factors such as:

- Temperature
- Humidity
- Wind Speed
- General Diffuse Flows
- Cloudiness

---

##  Dataset Overview

- **Source**: Google Sheets (CSV)
- **Total Records**: 52,583
- **Features**: 9
- **Target Variable**: `Power Consumption in A Zone`

---

##  Data Cleaning

- Removed duplicates and irrelevant columns (`S no`)
- Converted object data types (`Temperature`, `Humidity`, `Wind Speed`) to numeric
- Dropped rows with missing values (less than 1%)
- Renamed target column to `Power Consumption`

---

##  Feature Selection

| Feature                   | Correlation with Target | Action           |
|---------------------------|--------------------------|------------------|
| Temperature               | +0.558                   | ✅ Kept          |
| Humidity                  | -0.230                   | ✅ Kept          |
| Wind Speed                | +0.204                   | ✅ Kept          |
| General Diffuse Flows     | +0.208                   | ✅ Kept          |
| Cloudiness                | -0.103 (Binary)          | ✅ Kept (Optional)|
| Diffuse Flows             | +0.060                   | ❌ Dropped       |
| Air Quality Index (PM)    | -0.002                   | ❌ Dropped       |

---

##  Outlier Treatment

- Used **IQR method** to cap outliers for:
  - Temperature
  - Humidity
  - General Diffuse Flows

- Outliers were capped at calculated upper/lower bounds
- Cloudiness: binary, outlier detection not applicable

---

##  Exploratory Data Analysis (EDA)

- **Temperature** shows strong positive correlation with power usage
- **Humidity** has a weak negative impact
- **Wind Speed** shows abnormal clustering (bimodal)
- **General Diffuse Flows** has weak or non-linear patterns

---

##  Data Preprocessing & Transformations

- Applied `log1p` transformation to:
  - Wind Speed
  - General Diffuse Flows  
   - Helps normalize skewed distributions

- Used `StandardScaler` for feature scaling
- Train-test split (80-20) applied **before** transformation to avoid data leakage

---

##  Model Building

- **Model Used**: `RandomForestRegressor`
- **Train-Test Split**: 80/20
- **Features Used**: 5 (excluding dropped ones)

---

##  Model Evaluation (Random Forest)

| Metric       | Value     |
|--------------|-----------|
| MAE          | 3382.14   |
| RMSE         | 4913.97   |
| R² Score     | 0.6224    |
| CV R² (5-Fold)| 0.6068   |

- Predicts with ±3.3k kWh average error
- Captures ~62.2% of power consumption variance

---

## Feature Importance (Random Forest)

1. **Temperature** 
2. Humidity 
3. General Diffuse Flows 
4. Wind Speed 
5. Cloudiness 

---

##  Observations

- Temperature is the dominant factor influencing power consumption.
- Wind Speed may have complex non-linear effects.
- Cloudiness has minimal effect (binary and weak correlation).
- Diffuse Flows and AQI were redundant and removed.

---

##  Future Improvements

- Add time-based features (e.g., hour, season, holidays)
- Include socio-demographic or building-level usage data
- Try ensembling (XGBoost, LightGBM) or time-series models
- Perform hyperparameter tuning for optimal performance

---


##  Conclusion

This project successfully demonstrates how machine learning can be applied to predict power consumption using real-world environmental data. The Random Forest model explained ~62% of the variability in power demand, highlighting the importance of weather-related features in energy forecasting and smart city planning.

---

