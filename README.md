# Avocado Price Forecasting Project

![Avocado](https://img.shields.io/badge/Avocado-Price%20Prediction-brightgreen)
![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![CRISP-DM](https://img.shields.io/badge/Methodology-CRISP--DM-lightgrey)

## Project Overview

This project develops machine learning models to predict Hass avocado prices across various regions of the United States. By leveraging historical price data, sales volumes, and weather information, we create forecasts that provide actionable insights for retailers, distributors, farmers, and consumers.

> "Everyone loves avocados—it's only a shame that the prices vary so much each season. Wouldn't it be great to predict the price of avocados in the upcoming months?"

## Data Sources

### Avocado Price Data
- **Original Dataset (2015-2018)**: [Kaggle - Avocado Prices](https://www.kaggle.com/datasets/neuromusic/avocado-prices)
  - Located at: `data/raw/avocado.csv`
- **Extended Dataset (2015-2023)**: [Kaggle - Avocado Prices and Sales Volume](https://www.kaggle.com/datasets/vakhariapujan/avocado-prices-and-sales-volume-2015-2023)
  - Located at: `data/raw/Avocado_HassAvocadoBoard_20152015v1.0.1.csv`

### Weather Data
- Historical weather data retrieved via Meteostat API for corresponding US regions
- Integrated datasets with weather features for both training and validation

## Technical Approach

### Feature Engineering & Preprocessing
- **Temporal Features**: Extraction of year, month, day, quarter, day of week
- **Seasonality Analysis**: Seasonal decomposition and trend identification
- **Weather Integration**: Temperature, precipitation, and weather event correlations
- **Regional Encoding**: One-hot encoding for regional market characteristics
- **Type-Based Features**: Organic vs. conventional distinctions
- **Volume Metrics**: Total volume, bags by size category

### Machine Learning Models
- **Traditional ML Models**
  - Linear Regression with regularization
  - Random Forest Regressor
  - Gradient Boosting Regressor
  - XGBoost
- **Time Series Exploration**
  - Trend and seasonality analysis
  - Moving averages and decomposition

### Evaluation Metrics
- **R²**: Coefficient of determination (target: >0.7 for LR, >0.9 for RF)
- **MAE**: Mean Absolute Error (target: <0.1)
- **RMSE**: Root Mean Squared Error (target: <0.15)

## Key Findings

- **Model Performance**:
  - Random Forest achieved best performance with R² of 0.93, MAE of 0.07, and RMSE of 0.11
  - Linear Regression underperformed (R² of 0.45), indicating the non-linear nature of avocado pricing
  - Weather data integration maintained but did not improve model performance

- **Most influential price predictors**:
  - Avocado type (organic vs. conventional)
  - Geographic region
  - Seasonal factors
  - Volume metrics

- **Market Insights**:
  - Pronounced regional price variations with different volatility patterns
  - Organic avocados show greater price stability but consistently higher pricing
  - Clear seasonal patterns affect pricing throughout the year

## Project Structure

```
├── README.md                        <- Project documentation
├── data                             <- All project data
│   ├── external                     <- Data from third party sources
│   ├── interim                      <- Intermediate transformed data
│   ├── processed                    <- Final, canonical data for modeling
│   └── raw                          <- Original, immutable data
│
├── notebooks                        <- Jupyter notebooks following CRISP-DM phases
│   ├── 0-Overview.ipynb             <- Project overview and organization
│   ├── 1_Business_Understanding.ipynb
│   ├── 2_Data_Understanding.ipynb
│   ├── 3_Data_Preparation.ipynb
│   ├── 4_Modeling.ipynb
│   └── 5_Evaluation.ipynb
│
├── src                              <- Source code for data collection and processing
│   └── getweatherdata.py            <- Weather data collection utilities
│
├── requirements.txt                 <- Project dependencies
│
└── .env                             <- Environment variables and configuration
```

## Setup Instructions

1. Clone the repository
2. Create a virtual environment (recommended):
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Start Jupyter Notebook:
```bash
jupyter notebook
```

5. Navigate through the notebooks in numerical order to follow the CRISP-DM process

## Required Libraries

- **Data Manipulation**: pandas, numpy
- **Visualization**: matplotlib, seaborn, plotly
- **Machine Learning**: scikit-learn, xgboost
- **Time Series**: statsmodels
- **Weather Data**: meteostat
- **Utilities**: jupyter, tqdm

## Limitations and Future Work

- **Current Limitations**:
  - Limited to Hass avocados only
  - Weekly granularity (cannot capture daily fluctuations)
  - Limited ability to account for market disruptions
  - Regional aggregation may mask micromarket conditions

- **Future Improvements**:
  - Incorporate more granular weather data
  - Add macroeconomic indicators (inflation, fuel prices, exchange rates)
  - Develop region-specific models for unique market dynamics
  - Experiment with deep learning for capturing complex patterns
  - Implement automated model updating with new data

## License

This project is licensed under the MIT License - see the LICENSE file for details.

<a target="_blank" href="https://cookiecutter-data-science.drivendata.org/">
    <img src="https://img.shields.io/badge/CCDS-Project%20template-328F97?logo=cookiecutter" />
</a>
