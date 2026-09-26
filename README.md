# Rossmann Store Sales Prediction

## 📌 Project Overview

This project focuses on predicting **daily sales for 1,115 Rossmann stores across Germany** using historical sales data and store-level information.

The main goal is to build a robust machine learning pipeline that can accurately forecast sales and provide useful predictions for **store planning, staffing, and operational decision-making**.

---

## 🎯 Problem Statement

### Objective

Develop a unified predictive model for daily store sales that can:

* Forecast sales across **1,115 stores**
* Capture store-specific sales patterns
* Identify temporal trends and seasonality
* Improve prediction accuracy using historical sales behavior
* Support effective staff scheduling and store planning

### Evaluation Metric

The original competition evaluates predictions using **Root Mean Square Percentage Error (RMSPE)**.

> Days with zero sales are excluded from the RMSPE calculation.

For this project, model performance was additionally evaluated using:

* **MAE — Mean Absolute Error**
* **RMSE — Root Mean Squared Error**

---

## 📊 Dataset

**Source:** Rossmann Store Sales — Kaggle Competition

The dataset contains historical information about Rossmann stores, including sales, customers, promotions, store characteristics, and dates.

🔗 https://www.kaggle.com/competitions/rossmann-store-sales/overview

---

## 🔎 Data Preparation

The dataset was prepared through several preprocessing and feature engineering steps.

### Date Features

The original `Date` column was transformed into multiple time-based features:

* `Year`
* `Month`
* `Day`
* `Week`

The original `Date` column was then removed after extracting the required temporal information.

### Feature Types

Features were separated into:

* **Numerical Features**
* **Categorical Features**

Categorical variables were transformed using **One-Hot Encoding** before model training.

### Removed Features

The following columns were removed during preprocessing:

* `Date`
* `Customers`

`Customers` was excluded because it can introduce information that is not available when making a genuine future sales prediction.

---

## ⚙️ Feature Engineering

Because sales behavior differs significantly between the **1,115 individual stores**, store-level time-series features were created.

### Lag Features

Historical sales values were used to create lag-based features within each store.

This allows the model to learn from previous sales behavior rather than relying only on static store and calendar information.

### Window Features

Rolling/window-based features were also generated using sales grouped by `Store`.

These features help capture:

* Recent sales trends
* Local fluctuations
* Short-term sales behavior
* Store-specific patterns

### Store-Level Grouping

Lag and rolling features were calculated separately for each store:

```text
Store → Historical Sales → Lag Features → Rolling Features
```

This prevents sales history from different stores from being mixed together.

---

## 🤖 Modeling

### XGBoost

The final predictive model was built using **XGBoost**, a gradient boosting algorithm well suited for structured/tabular data.

The modeling pipeline included:

```text
Raw Data
   ↓
Data Cleaning
   ↓
Date Feature Extraction
   ↓
Store-Level Lag Features
   ↓
Rolling/Window Features
   ↓
Numerical & Categorical Features
   ↓
One-Hot Encoding
   ↓
XGBoost
   ↓
Sales Prediction
   ↓
Model Evaluation
```

---

## 📈 Model Performance

### XGBoost Results

| Metric   |      Score |
| -------- | ---------: |
| **MAE**  |  **19.60** |
| **RMSE** | **116.22** |

```text
MAE  : 19.5980
RMSE : 116.2237
```

The relatively low MAE indicates that the model can capture the general sales patterns across stores, while RMSE provides additional insight into larger prediction errors.

---

## 🛠️ Technologies

* Python
* Pandas
* NumPy
* Scikit-learn
* XGBoost
* Matplotlib
* Jupyter Notebook
* One-Hot Encoding
* Feature Engineering
* Time-Series / Lag Features

---

## 📂 Project Workflow

### Stage 1 — Data Understanding

* Load Rossmann sales data
* Inspect data types and distributions
* Identify numerical and categorical variables

### Stage 2 — Data Preprocessing

* Handle missing values
* Extract date-related features
* Remove unnecessary columns
* Separate numerical and categorical features

### Stage 3 — Feature Engineering

* Create `Year`, `Month`, `Day`, and `Week`
* Generate store-level lag features
* Generate rolling/window features
* Group historical sales by `Store`

### Stage 4 — Encoding

* Apply One-Hot Encoding to categorical variables
* Prepare the final training matrix

### Stage 5 — Modeling

* Train an XGBoost regression model
* Generate sales predictions

### Stage 6 — Evaluation

Evaluate model performance using:

* MAE
* RMSE

---

## 📌 Key Takeaways

* **Store-level grouping** is essential because sales behavior varies significantly across the 1,115 stores.
* **Lag features** allow the model to use historical sales information.
* **Rolling features** help capture recent trends and short-term fluctuations.
* Combining **calendar, store, and historical sales features** provides a stronger representation of sales behavior.
* XGBoost provides an effective approach for modeling this structured sales prediction problem.

---

## 🚀 Future Improvements

Potential improvements include:

* Hyperparameter tuning for XGBoost
* More extensive lag periods
* Additional rolling statistics such as mean, median, standard deviation, minimum, and maximum
* Store-specific models or hierarchical approaches
* More advanced time-series validation
* Target encoding for high-cardinality categorical features
* Evaluation using the original competition metric, **RMSPE**

---

## 👩‍💻 Author

**Newsha Sadat Raisi**
Data Analyst | Machine Learning & AI Developer

GitHub: https://github.com/Newshasadat
