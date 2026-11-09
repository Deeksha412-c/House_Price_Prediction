# House Price Prediction — Model Evaluation Report

## 1. Project Overview

### Objective
The objective of this project is to develop and evaluate machine learning regression models that predict house prices based on property characteristics such as area, number of bedrooms, bathrooms, age, location, and property type.

### Problem Statement
House prices depend on several factors, making accurate price estimation challenging. This project uses machine learning techniques to analyze property data and predict house prices.

### Project Goals
- Understand and explore the housing dataset.
- Clean and prepare data for machine learning.
- Build multiple regression models.
- Evaluate model performance using regression metrics.
- Compare models and identify the best-performing candidate.
- Extract meaningful insights for potential home buyers.

## 2. Dataset Description

The dataset contains 300 house-property records and 8 columns.

### Dataset Features

| Column | Description |
|---|---|
| Property_ID | Unique property identifier |
| Area | Area of the property |
| Bedrooms | Number of bedrooms |
| Bathrooms | Number of bathrooms |
| Age | Age of the property |
| Location | Property location category |
| Property_Type | Type of property |
| Price | Target variable (house price) |

### Dataset Summary

- Total records: 300
- Total columns: 8
- Missing values: 0
- Duplicate records: 0
- Unique property IDs: 300
- Target variable: Price

### Descriptive Statistics

| Statistic | Area | Price |
|---|---:|---:|
| Minimum | 520 | 3,695,000 |
| Mean | 2,759.7 | 24,883,660 |
| Median | 2,738 | 22,365,000 |
| Maximum | 4,999 | 58,700,000 |

### Initial Observations

- Area has a strong positive correlation with house price (0.7963).
- Bedrooms have a weak positive correlation with price (0.2025).
- Age has a weak negative correlation with price (-0.1308).
- Bathrooms have a very weak negative correlation with price (-0.0303).

These observations helped identify potentially useful features for the prediction models.

## 3. Data Preprocessing

The dataset was checked and prepared before training the machine learning models.

### 3.1 Data Cleaning
- Checked for missing values.
- Confirmed that no missing values were present.
- Checked for duplicate records.
- Confirmed that no duplicate records were present.
- Excluded `Property_ID` because it is an identifier and does not provide meaningful predictive information.

### 3.2 Feature Selection

**Input features (X):**
- Area
- Bedrooms
- Bathrooms
- Age
- Location
- Property_Type

**Target variable (y):**
- Price

### 3.3 Categorical Encoding

One-Hot Encoding was applied to convert categorical variables into numerical features.

Categorical columns:
- Location
- Property_Type

The encoded dataset contained 10 input features.

### 3.4 Train-Test Split

The dataset was divided into training and testing sets.

| Dataset | Records | Percentage |
|---|---:|---:|
| Training | 240 | 80% |
| Testing | 60 | 20% |
| Total | 300 | 100% |

The `random_state=42` parameter was used to make the split reproducible.

## 4. Machine Learning Models Implemented

Four regression models were developed and evaluated.

### 4.1 Linear Regression

Linear Regression was used as the baseline model to understand the relationship between property features and house prices.

### 4.2 Polynomial Regression

Polynomial Regression with degree 2 was implemented to capture nonlinear relationships between features and house prices.

### 4.3 Decision Tree Regression

A Decision Tree Regressor was trained to model nonlinear patterns using decision-based splits.

### 4.4 Random Forest Regression

A Random Forest Regressor with 100 estimators was implemented. It combines multiple decision trees to improve prediction performance and reduce the limitations of a single tree.

### Model Training

All four models were trained using the training dataset and evaluated using the held-out test dataset.

## 5. Model Evaluation

The models were evaluated using three regression metrics: Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and R² Score.

### 5.1 Evaluation Metrics

- **MAE:** Measures the average absolute difference between actual and predicted house prices. Lower values are better.
- **RMSE:** Measures prediction error while giving greater weight to larger errors. Lower values are better.
- **R² Score:** Measures how much of the variation in house prices is explained by the model. Higher values are better.

### 5.2 Model Comparison

| Model | MAE | RMSE | R² Score |
|---|---:|---:|---:|
| Linear Regression | 2,188,736.34 | 2,907,633.21 | 0.9406 |
| Polynomial Regression | 714,540.73 | 896,287.75 | 0.9944 |
| Decision Tree | 2,194,416.67 | 2,864,232.30 | 0.9424 |
| Random Forest | 1,453,575.83 | 1,932,346.94 | 0.9738 |

### 5.3 Evaluation Insights

- Polynomial Regression achieved the lowest MAE and RMSE.
- Polynomial Regression also achieved the highest R² score on the test dataset.
- Random Forest performed better than Linear Regression and Decision Tree on all three reported metrics.
- Decision Tree produced the weakest overall test performance among the four models.

Based on the held-out test results, Polynomial Regression was the best-performing model in this experiment.

## 6. Cross-Validation and Overfitting Analysis

### 6.1 Training vs Testing Performance

Training and testing R² scores were compared to identify potential overfitting.

| Model | Training R² | Testing R² |
|---|---:|---:|
| Linear Regression | 0.9579 | 0.9406 |
| Polynomial Regression | 0.9927 | 0.9944 |
| Decision Tree | 1.0000 | 0.9424 |
| Random Forest | 0.9968 | 0.9738 |

**Observations:**
- Linear Regression showed reasonably consistent training and testing performance.
- Polynomial Regression achieved strong performance on both datasets, without an obvious overfitting signal from this comparison.
- Decision Tree achieved a perfect training R² but a lower testing R², indicating likely overfitting.
- Random Forest showed a training-testing gap, but retained strong test performance.

### 6.2 Five-Fold Cross-Validation

Five-fold cross-validation was performed on the training dataset to assess model consistency.

| Model | Average CV R² | Standard Deviation |
|---|---:|---:|
| Linear Regression | 0.9529 | 0.00768 |
| Polynomial Regression | 0.9909 | 0.00223 |
| Decision Tree | 0.9401 | 0.00586 |
| Random Forest | 0.9710 | 0.00447 |

**Cross-Validation Findings:**
- Polynomial Regression achieved the highest average R² score of 0.9909.
- It also had the lowest standard deviation of 0.00223, indicating consistent performance across the five folds.
- Random Forest ranked second, with an average R² of 0.9710.
- Decision Tree achieved the lowest average cross-validation R².

### 6.3 Conclusion

Polynomial Regression was the strongest candidate based on both test-set evaluation and five-fold cross-validation.

However, these results come from a relatively small dataset of 300 records. Further validation on additional, representative housing data is recommended before real-world deployment.

## 7. Feature Importance Analysis

Feature importance was extracted from the trained Random Forest Regressor to understand which input variables contributed most to its predictions.

### 7.1 Feature Importance Results

| Feature | Importance |
|---|---:|
| Area | 0.687588 |
| Location_City Center | 0.155224 |
| Location_Rural | 0.097460 |
| Location_Suburb | 0.029165 |
| Bedrooms | 0.018998 |
| Age | 0.007601 |
| Bathrooms | 0.001709 |
| Property_Type_Villa | 0.000885 |
| Property_Type_Apartment | 0.000757 |
| Property_Type_House | 0.000613 |

### 7.2 Key Findings

- Area was the most influential feature, with an importance score of approximately 0.6876.
- Location was also important, particularly the City Center and Rural categories.
- Bedrooms had relatively low importance compared with area and location.
- Age and bathrooms had low importance in this model.
- Property-type indicators contributed very little to the Random Forest's predictions.

### 7.3 Business Insights

The analysis suggests that property area and location deserve particular attention when estimating house prices.

For potential home buyers:
- Compare the area and price of similar properties.
- Evaluate location, connectivity, and nearby facilities.
- Inspect the property's age, structural condition, and maintenance requirements.
- Consider bedrooms, bathrooms, and property type according to individual needs.

**Note:** Feature importance represents the model's relative reliance on each feature. It does not establish causation or measure the actual percentage contribution to a property's price.

## 8. Visualizations and Project Outputs

The following visualizations were created during the project to support data exploration and model evaluation.

| Visualization | Purpose |
|---|---|
| Price Distribution Histogram | Understand the distribution of house prices |
| Area vs Price Scatter Plot | Examine the relationship between area and price |
| Location vs Price Box Plot | Compare price distributions across locations |
| Correlation Heatmap | Identify relationships between numerical variables |
| Regression Line Plot | Visualize the relationship between area and predicted price |
| Predictions vs Actual Plot | Compare actual and predicted house prices |
| Model Comparison Chart | Compare R² scores across regression models |
| Feature Importance Chart | Identify influential features in the Random Forest model |

### Important Output Files

- `predictions_vs_actual.png`
- `model_comparison.png`
- `feature_importance.png`
- `regression_line.png`

These visualizations help communicate the model's performance and the insights obtained from the dataset.

## 9. Conclusion

The House Price Prediction project successfully demonstrated the application of machine learning regression techniques to estimate house prices using property characteristics.

Four regression models were developed and compared:

- Linear Regression
- Polynomial Regression
- Decision Tree Regression
- Random Forest Regression

Polynomial Regression achieved the strongest overall results in this experiment, with:

- MAE: 714,540.73
- RMSE: 896,287.75
- Test R²: 0.9944
- Five-fold Cross-Validation Average R²: 0.9909

The analysis also identified Area and Location as the most influential features in the Random Forest model.

The project provided practical experience in data preprocessing, feature engineering, regression modelling, model evaluation, cross-validation, visualization, and business interpretation.

## 10. Limitations and Future Improvements

### Limitations
- The dataset contains only 300 records.
- The dataset may not represent all real-world housing markets.
- Model performance on new locations or market conditions has not been established.
- The test set was used to compare multiple models, so its results may be optimistic as a final estimate.
- Random Forest feature importance does not establish causal relationships.

### Future Improvements
- Train and validate models using a larger, more diverse housing dataset.
- Use a preprocessing pipeline to perform categorical encoding after splitting the data.
- Tune model hyperparameters using cross-validation.
- Investigate additional features such as neighborhood quality, amenities, property condition, and distance to transport.
- Evaluate the selected model on a separate, untouched test dataset.
- Develop a simple web application for interactive house price predictions.

## 11. Final Recommendation

Polynomial Regression is the best-performing candidate among the four models evaluated in this project.

Its strong test-set and cross-validation results make it a promising candidate for further validation. It should not yet be considered a production-ready house price estimation system without testing on larger and more representative data.

