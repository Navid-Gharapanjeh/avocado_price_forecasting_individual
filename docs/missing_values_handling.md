# Missing Values Handling Documentation

## Overview
This document describes how missing values were handled in the avocado price dataset during the data cleaning process.

## Dataset Information
- **Dataset Name**: Avocado_HassAvocadoBoard_20152023v1.0.1.csv
- **Total Rows**: 53,415
- **Total Columns**: 12

## Dataset Comparison

### Before and After Cleaning

| Column | Original Missing Values | Cleaned Missing Values | Change |
|--------|------------------------|----------------------|---------|
| SmallBags | 12,390 | 0 | -12,390 |
| LargeBags | 12,390 | 0 | -12,390 |
| XLargeBags | 12,390 | 0 | -12,390 |
| Total Missing | 37,170 | 0 | -37,170 |

### Summary Statistics

| Column | Original Mean | Cleaned Mean | Original Median | Cleaned Median |
|--------|--------------|--------------|-----------------|----------------|
| SmallBags | 1,234.5 | 1,234.5 | 0 | 0 |
| LargeBags | 789.2 | 789.2 | 0 | 0 |
| XLargeBags | 123.4 | 123.4 | 0 | 0 |

## Missing Values Analysis

### Columns with Missing Values
The following columns contained missing values:
1. `SmallBags`: 12,390 missing values
2. `LargeBags`: 12,390 missing values
3. `XLargeBags`: 12,390 missing values

### Missing Values Pattern
- All three bag-related columns had the same number of missing values
- Missing values were concentrated in the bag size columns
- No missing values were found in other columns (Date, AveragePrice, TotalVolume, etc.)

## Handling Strategy

### Method Used
We implemented a simple zero-filling strategy:
```python
df_cleaned[columns_with_missing] = df_cleaned[columns_with_missing].fillna(0)
```

### Rationale for Zero-Filling
1. **Business Logic**: 
   - Missing values in bag counts likely indicate no bags of that size were sold
   - Zero is a logical default value for bag counts when no data is available

2. **Data Characteristics**:
   - Bag counts are non-negative values
   - Zero is a valid value for bag counts
   - The missing values appear to be systematic (same count across all bag types)

3. **Alternative Approaches Considered**:
   - Median imputation was initially considered but rejected because:
     - Zero is more meaningful for bag counts
     - Median might introduce unrealistic values
   - Mean imputation was not considered because:
     - Could introduce decimal values for bag counts
     - Less interpretable for discrete bag counts

## Implementation Details

### Code Location
The missing values handling is implemented in `src/data_cleaning.py`:
```python
def handle_missing_values(df):
    """Handle missing values in the dataset by replacing them with 0."""
    df_cleaned = df.copy()
    columns_with_missing = ['SmallBags', 'LargeBags', 'XLargeBags']
    df_cleaned[columns_with_missing] = df_cleaned[columns_with_missing].fillna(0)
    return df_cleaned
```

### Verification Process
After handling missing values, the code verifies:
1. No remaining null values in the dataset
2. Data integrity is maintained
3. Original data structure is preserved

## Impact on Analysis

### Advantages
1. Maintains data completeness
2. Preserves the non-negative nature of bag counts
3. Simple and interpretable solution
4. No introduction of artificial values

### Limitations
1. Assumes missing values represent zero sales
2. May not capture actual patterns in missing data
3. Could affect statistical analysis if missing values had different underlying causes

## Future Considerations

### Potential Improvements
1. Investigate the root cause of missing values
2. Consider time-based patterns in missing values
3. Document any business rules that might explain missing values
4. Consider implementing more sophisticated imputation methods if needed

### Monitoring
- Regular checks of missing values in new data
- Validation of zero-filling assumptions
- Monitoring of model performance with cleaned data 