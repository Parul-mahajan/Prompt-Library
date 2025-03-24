# Basic Data Preprocessing with GitHub Copilot

## Prompt 1: Simple Data Preprocessing Steps
```
Intent: To help data scientists and ML engineers create basic preprocessing code using GitHub Copilot.

Context: You are preprocessing a simple dataset for a machine learning model. The dataset details are as follows:

dataset_type: {dataset_type}
target_variable: {target_variable}
basic_issues: {basic_issues}

Generate a preprocessing script focusing on:
- Loading data
- Basic cleaning
- Simple feature transformations
- Standard preprocessing steps

Example:
dataset_type: "Tabular data with numeric and categorical features"
target_variable: "customer_churn (binary: 0=no, 1=yes)"
basic_issues: "Missing values, outliers in numeric columns"

Data Preprocessing Script:
```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline

# Load and examine data
def load_data(file_path):
    """
    Load data from CSV file
    """
    df = pd.read_csv(file_path)
    print(f"Dataset shape: {df.shape}")
    return df

# Basic data exploration
def explore_data(df):
    """
    Perform basic exploratory analysis
    """
    # Check data types
    print("\nData types:")
    print(df.dtypes)
    
    # Check for missing values
    print("\nMissing values:")
    missing_values = df.isnull().sum()
    print(missing_values[missing_values > 0])
    
    # Basic statistics for numeric columns
    print("\nNumeric column statistics:")
    numeric_cols = df.select_dtypes(include=['int64', 'float64'])
    print(numeric_cols.describe())
    
    return numeric_cols.columns, df.select_dtypes(include=['object']).columns

# Basic preprocessing function
def preprocess_data(df, target_col, numeric_cols, categorical_cols):
    """
    Preprocess data with standard steps
    """
    # Separate features and target
    X = df.drop(columns=[target_col])
    y = df[target_col]
    
    # Create preprocessing pipeline
    numeric_transformer = Pipeline(steps=[
        ('imputer', SimpleImputer(strategy='median')), 
        ('scaler', StandardScaler())
    ])
    
    categorical_transformer = Pipeline(steps=[
        ('imputer', SimpleImputer(strategy='most_frequent')),
        ('encoder', OneHotEncoder(handle_unknown='ignore'))
    ])
    
    preprocessor = ColumnTransformer(transformers=[
        ('num', numeric_transformer, numeric_cols),
        ('cat', categorical_transformer, categorical_cols)
    ])
    
    # Fit and transform the data
    X_processed = preprocessor.fit_transform(X)
    
    print(f"Processed feature matrix shape: {X_processed.shape}")
    return X_processed, y, preprocessor

# Handle outliers with simple capping
def handle_outliers(df, numeric_cols):
    """
    Cap outliers using IQR method
    """
    df_clean = df.copy()
    
    for col in numeric_cols:
        # Calculate IQR
        q1 = df[col].quantile(0.25)
        q3 = df[col].quantile(0.75)
        iqr = q3 - q1
        
        # Define bounds
        lower_bound = q1 - 1.5 * iqr
        upper_bound = q3 + 1.5 * iqr
        
        # Cap outliers
        df_clean[col] = np.where(df[col] < lower_bound, lower_bound, df[col])
        df_clean[col] = np.where(df[col] > upper_bound, upper_bound, df[col])
    
    return df_clean

# Simple example usage
if __name__ == "__main__":
    # Example usage
    file_path = "customer_data.csv"
    target_col = "customer_churn"
    
    # Load data
    df = load_data(file_path)
    
    # Explore and get column types
    numeric_cols, categorical_cols = explore_data(df)
    
    # Handle outliers
    df_clean = handle_outliers(df, numeric_cols)
    
    # Preprocess data
    X_processed, y, preprocessor = preprocess_data(
        df_clean, target_col, numeric_cols, categorical_cols
    )
    
    print("Preprocessing complete!")
```

Key points to consider:
1. Use standard libraries like pandas, numpy, and scikit-learn
2. Focus on common preprocessing steps rather than complex techniques
3. Include basic data exploration in your workflow
4. Use standard approaches for handling missing values and outliers
5. Create reusable preprocessing functions