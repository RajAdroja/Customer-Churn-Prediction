# Customer-Churn-Prediction


## Overview

This project focuses on building a **Customer Churn Prediction System** for a telecommunications company. The system uses machine learning to identify customers likely to stop using the company's services. By predicting churn, businesses can implement proactive retention strategies and improve customer satisfaction and profitability.

The best-performing model in this project is **LightGBM**, which was fine-tuned for optimal performance.

---

## Table of Contents

1. [Dataset](#dataset)
2. [Preprocessing Steps](#preprocessing-steps)
3. [Feature Engineering](#feature-engineering)
4. [Model Selection and Evaluation](#model-selection-and-evaluation)
5. [Pipeline for New Data](#pipeline-for-new-data)
6. [Usage Instructions](#usage-instructions)
7. [Results](#results)
8. [Dependencies](#dependencies)

---

## Dataset

The dataset contains **3,333 customer records** with 21 features, including:
- **Numerical Features**: `account length`, `total day minutes`, `total eve minutes`, etc.
- **Categorical Features**: `state`, `area code`, `international plan`, etc.
- **Target Variable**: `churn` (True for churned customers, False otherwise).

### Key Observations:
- No missing or duplicate values.
- Highly imbalanced dataset: ~85% non-churners and ~15% churners.
- Outliers exist in several numerical columns.

---

## Preprocessing Steps

The following preprocessing steps were applied:

1. **Data Cleaning**:
   - Corrected data types (e.g., converted `area code` to categorical).
   - Dropped irrelevant columns (`phone number`).

2. **Handling Imbalanced Data**:
   - Used the ADASYN oversampling technique to balance the dataset.

3. **Encoding Categorical Features**:
   - Direct mapping for binary features (`international plan`, `voice mail plan`).
   - Frequency encoding for high-cardinality features (`area code`).
   - Target encoding for features like `state`.

4. **Scaling**:
   - Applied RobustScaler to numerical features to handle outliers effectively.

5. **Feature Selection**:
   - Removed highly correlated features to avoid multicollinearity (e.g., dropped `total day minutes` since it was perfectly correlated with `total day charge`).

---

## Feature Engineering

1. **Transformations**:
   - Log transformation on skewed features like `total intl calls`.
   - Binning of features like `customer service calls`.

2. **Derived Features**:
   - Created new features such as charge-per-minute metrics (e.g., `total_day_charge_per_minute`).

3. **Dropped Features**:
   - Irrelevant or redundant features identified during correlation analysis and feature importance evaluation.

---

## Model Selection and Evaluation

### Models Evaluated:
- Logistic Regression
- Random Forest
- Support Vector Classifier
- Decision Tree
- K-Nearest Neighbors
- Gradient Boosting
- LightGBM
- Naive Bayes

### Best Model: LightGBM
The LightGBM model achieved the best performance after hyperparameter tuning with the following metrics on the test set:
- **Accuracy**: 93.85%
- **Precision**: 87.84%
- **Recall**: 67.01%
- **F1 Score**: 76.02%
- **ROC AUC**: 90.10%

---

## Pipeline for New Data

A preprocessing pipeline was created to automate the steps for new data predictions:

1. Map binary categorical variables (`international plan`, `voice mail plan`) to integers.
2. Apply target encoding for features like `state`.
3. Bin and encode specific columns (e.g., `customer service calls`).
4. Apply log transformation on skewed features (e.g., `total intl calls`).
5. Drop irrelevant columns.
6. Scale numerical features using RobustScaler.
7. Use the trained LightGBM model to predict churn.

---

## Usage Instructions

### Prerequisites
Ensure you have Python installed along with the required libraries.

### Steps:

1. Clone this repository and navigate to the project directory.
2. Load your new customer data into a Pandas DataFrame.
3. Run the provided script or use the function below: