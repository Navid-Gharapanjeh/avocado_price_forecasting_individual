# Avocado Price Forecasting Project

![Avocado](https://img.shields.io/badge/Avocado-Price%20Prediction-brightgreen)
![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![CRISP-DM](https://img.shields.io/badge/Methodology-CRISP--DM-lightgrey)

## Project Overview

This project develops machine learning models to predict Hass avocado prices across various regions of the United States. By leveraging historical price data, sales volumes, and weather information, we create forecasts that provide actionable insights for retailers, distributors, farmers, and consumers.

> "Everyone loves avocados—it's only a shame that the prices vary so much each season. Wouldn't it be great to predict the price of avocados in the upcoming months?"

## Business Value

Accurate avocado price prediction delivers significant value to multiple stakeholders:

- **Retailers**: Optimize pricing strategies and inventory management
- **Distributors**: Better plan operations and logistics
- **Farmers**: Make informed decisions about harvesting and market timing
- **Consumers**: Benefit from more stable pricing through improved market efficiency

## CRISP-DM Methodology

This project follows the Cross-Industry Standard Process for Data Mining (CRISP-DM) methodology:

1. **Business Understanding**: Clearly defined objectives, success criteria, and constraints
2. **Data Understanding**: Comprehensive exploration of avocado pricing datasets and weather data
3. **Data Preparation**: Rigorous cleaning, feature engineering, and integration of multiple data sources
4. **Modeling**: Implementation of time series and machine learning approaches
5. **Evaluation**: Thorough assessment against business and technical success criteria
6. **Deployment**: Production of actionable forecasts and recommendations

## Data Sources

### Avocado Price Data
- **Original Dataset (2015-2018)**: [Kaggle - Avocado Prices](https://www.kaggle.com/datasets/neuromusic/avocado-prices)
  - Located at: `data/raw/avocado.csv`
- **Extended Dataset (2015-2023)**: [Kaggle - Avocado Prices and Sales Volume](https://www.kaggle.com/datasets/vakhariapujan/avocado-prices-and-sales-volume-2015-2023)
  - Located at: `data/raw/Avocado_HassAvocadoBoard_20152015v1.0.1.csv`

### Weather Data
- Historical weather data retrieved via Meteostat API for corresponding US regions
- Integrated datasets:
  - `data/raw/avocado2015to2022withweather.csv`: Training dataset with weather features
  - `data/raw/avocadoafter2023withweather.csv`: Validation dataset for 2023+

## Technical Approach

### Feature Engineering & Preprocessing
- **Temporal Features**: Extraction of year, month, day, quarter, day of week
- **Seasonality Analysis**: Seasonal decomposition and trend identification
- **Weather Integration**: Temperature, precipitation, and weather event correlations
- **Regional Encoding**: One-hot encoding for regional market characteristics
- **Type-Based Features**: Organic vs. conventional distinctions
- **Volume Metrics**: Total volume, bags by size category

### Machine Learning Models
- **Time Series Models**
  - ARIMA (AutoRegressive Integrated Moving Average)
  - SARIMA (Seasonal ARIMA)
  - Prophet (Facebook's forecasting tool)
- **Traditional ML Models**
  - Random Forest Regressor
  - Gradient Boosting Regressor
  - Linear Regression with regularization
- **Ensemble Methods**
  - Stacking of multiple model predictions
  - Weighted averaging of forecasts

### Evaluation Metrics
- **R²**: Coefficient of determination (target: >0.7 for LR, >0.9 for RF)
- **MAE**: Mean Absolute Error (target: <0.1)
- **RMSE**: Root Mean Squared Error (target: <0.15)
- **MAPE**: Mean Absolute Percentage Error
- **Statistical Tests**: Durbin-Watson, ADF for time series

## Key Findings

- Random Forest model achieved best performance with R² of 0.93, MAE of 0.07, and RMSE of 0.10
- Most influential price predictors:
  - Avocado type (organic vs. conventional)
  - Geographic region
  - Seasonal factors (particularly Q2 and Q4)
  - Weather conditions (especially temperature extremes)
- Pronounced regional price variations with highest volatility in West and Northeast regions
- Organic avocados show greater price stability but consistently higher pricing

## Project Structure

```
├── LICENSE                          <- Open-source license
├── Makefile                         <- Makefile with convenience commands
├── README.md                        <- This file; project documentation
├── data                             <- All project data
│   ├── external                     <- Data from third party sources
│   ├── interim                      <- Intermediate transformed data
│   ├── processed                    <- Final, canonical data for modeling
│   └── raw                          <- Original, immutable data
│
├── docs                             <- Documentation generated with mkdocs
│
├── models                           <- Trained models, predictions, summaries
│   └── trained                      <- Serialized trained models
│
├── notebooks                        <- Jupyter notebooks following CRISP-DM phases
│   ├── 1_Business_Understanding.ipynb
│   ├── 2_Data_Understanding.ipynb
│   ├── 3_Data_Preparation.ipynb
│   ├── 4_Modeling.ipynb
│   ├── 5_Evaluation.ipynb
│   ├── 6_Deployment.ipynb
│   └── avocado_price_forecasting.ipynb
│
├── reports                          <- Generated analysis reports
│   └── figures                      <- Generated graphics and figures
│
├── requirements.txt                 <- Project dependencies
│
└── avocado_price_forecasting_individual <- Source code package
    ├── __init__.py                  <- Makes package importable
    ├── config.py                    <- Configuration parameters
    ├── dataset.py                   <- Data downloading and loading utilities
    ├── features.py                  <- Feature engineering functions
    ├── modeling                     <- Model training and prediction code
    │   ├── __init__.py
    │   ├── predict.py               <- Prediction functionality
    │   └── train.py                 <- Model training functionality
    └── plots.py                     <- Visualization utilities
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
- **Machine Learning**: scikit-learn, xgboost, lightgbm
- **Time Series**: statsmodels, prophet
- **Weather Data**: meteostat
- **Utilities**: jupyter, tqdm

## Future Work

- Incorporate additional economic indicators (fuel prices, labor costs, inflation)
- Develop region-specific specialized models
- Create an interactive dashboard for real-time pricing forecast updates
- Extend model to predict prices by avocado size categories
- Explore causal inference methods for deeper relationship understanding

## License

This project is licensed under the MIT License - see the LICENSE file for details.

<a target="_blank" href="https://cookiecutter-data-science.drivendata.org/">
    <img src="https://img.shields.io/badge/CCDS-Project%20template-328F97?logo=cookiecutter" />
</a>
