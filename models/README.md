# Models Directory

This directory contains all trained models, model predictions, and model evaluation summaries for the avocado price forecasting project.

## Directory Structure

- **trained/**: Serialized trained models
- **predictions/**: Model predictions and forecasts
- **evaluation/**: Model performance metrics and evaluations

## Modeling Approach

For this project, we implemented and compared several forecasting models:

### 1. Time Series Models

#### ARIMA/SARIMA
- Description: Autoregressive Integrated Moving Average with Seasonality
- Implementation: Using statsmodels package
- Parameters:
  - p (AR order): 1-3
  - d (differencing): 1
  - q (MA order): 1-3
  - Seasonal parameters: (1,1,1,52) for weekly data
- Performance:
  - Statistically significant P-Value target: < 0.05 (not achieved, got 2.5)
  - Limited success for complex multi-regional forecasting

### 2. Machine Learning Regression Models

#### Linear Regression
- Description: Standard multiple linear regression
- Implementation: Using scikit-learn
- Features:
  - Region (encoded)
  - Type (organic/conventional)
  - Temporal features (year, month, week)
  - Sales volumes
  - Weather data (temperature)
- Performance:
  - R² target: > 0.7 (not achieved, got 0.60)
  - Model not well-suited for this complex forecasting task

#### Random Forest Regressor
- Description: Ensemble of decision trees
- Implementation: Using scikit-learn
- Hyperparameters:
  - n_estimators: 100
  - max_depth: optimized via grid search
  - min_samples_split: 2
  - random_state: 42
- Performance:
  - R² target: > 0.9 (achieved, got 0.93)
  - MAE: 0.07 (target < 0.1 achieved)
  - RMSE: 0.10 (target < 0.15 achieved)
  - Best overall performance across all models

#### Gradient Boosting Regressor
- Description: Gradient boosting ensemble method
- Implementation: Using scikit-learn
- Hyperparameters:
  - n_estimators: 200
  - learning_rate: 0.1
  - max_depth: 5
  - min_samples_split: 5
- Performance:
  - R²: 0.845
  - Competitive performance but not as strong as Random Forest

## Feature Importance

The feature importance analysis from the Random Forest model identified these key predictors:
1. Type (organic vs. conventional)
2. Region
3. Time of year (seasonality)
4. Temperature
5. Total volume

## Model Selection Process

The model selection process was guided by these criteria:
1. Predictive accuracy (R², MAE, RMSE)
2. Interpretability for stakeholders
3. Ability to incorporate diverse feature types
4. Cross-validation stability
5. Performance on unseen data

The Random Forest model was selected as the final model due to its superior performance across all evaluation metrics and strong performance in cross-validation tests.

## Model Usage

To use the trained models for prediction:

1. Load the serialized model from the `trained/` directory
2. Prepare input data with the same features used during training
3. Use the model's predict() method to generate price forecasts

Example code can be found in the `avocado_price_forecasting_individual/modeling/predict.py` module.

## Model Persistence

Models are saved using Python's pickle serialization. For production use, consider using more robust serialization methods like joblib for scikit-learn models or dedicated model serving frameworks. 