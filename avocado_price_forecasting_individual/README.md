# Avocado Price Forecasting Source Code

This directory contains the Python source code for the avocado price forecasting project. The code is organized into modular components that handle different aspects of the forecasting pipeline.

## Module Structure

- **\_\_init\_\_.py**: Makes the directory a Python package
- **config.py**: Configuration parameters and constants
- **dataset.py**: Data loading and processing utilities
- **features.py**: Feature engineering functions
- **modeling/**: Model training and prediction code
  - **\_\_init\_\_.py**: Makes the directory a Python sub-package
  - **train.py**: Model training functions
  - **predict.py**: Prediction and forecasting functions
- **plots.py**: Visualization utilities

## Key Components

### Configuration (config.py)

Contains project-wide configuration settings:
- File paths for data sources and outputs
- Model parameters and hyperparameters
- Evaluation metrics thresholds
- Visualization settings

### Data Management (dataset.py)

Functions for loading and processing avocado and weather data:
- Data loading from CSV files
- Data cleaning and validation
- Data partitioning for training/testing
- Data preparation utilities
- Weather data integration

Example usage:
```python
from avocado_price_forecasting_individual.dataset import load_data

# Load the training dataset with weather data
data = load_data('avocado2015to2022withweather.csv')
```

### Feature Engineering (features.py)

Functions for creating model features:
- Temporal feature extraction (year, month, week, day)
- Categorical encoding (region, type)
- Weather data transformations
- Volume-based feature calculations
- Seasonality and trend extraction

Example usage:
```python
from avocado_price_forecasting_individual.features import create_features

# Generate features for modeling
X, y = create_features(data, target_col='AveragePrice')
```

### Modeling (modeling/)

#### Training (train.py)

Functions for training and evaluating models:
- Model initialization and configuration
- Training pipelines for different model types
- Hyperparameter tuning
- Cross-validation
- Model serialization

Example usage:
```python
from avocado_price_forecasting_individual.modeling.train import train_random_forest

# Train a Random Forest model
model, metrics = train_random_forest(X_train, y_train, X_test, y_test)
```

#### Prediction (predict.py)

Functions for making predictions with trained models:
- Loading serialized models
- Prediction preprocessing
- Single and batch predictions
- Forecast generation
- Confidence intervals

Example usage:
```python
from avocado_price_forecasting_individual.modeling.predict import predict_price

# Predict avocado price for a specific date, region, and type
price = predict_price('2023-06-15', 'Chicago', 'conventional', 24.5)
```

### Visualization (plots.py)

Functions for creating visualizations:
- Price trend plots
- Feature importance visualizations
- Prediction vs. actual comparisons
- Regional comparison plots
- Seasonal analysis charts
- Model performance visualizations

Example usage:
```python
from avocado_price_forecasting_individual.plots import plot_price_forecast

# Plot price forecast for a specific region
plot_price_forecast(region='Chicago', start_date='2023-01-01', end_date='2023-12-31')
```

## Development

When extending this codebase:

1. Follow the established modular design
2. Document all functions with docstrings
3. Add type hints for better code maintainability
4. Implement unit tests for new functionality
5. Update the relevant notebooks to demonstrate new features

## Usage

This code is designed to be imported and used within Jupyter notebooks or scripts. The primary interface is through the functions provided in each module, which are documented with docstrings explaining their parameters and return values. 