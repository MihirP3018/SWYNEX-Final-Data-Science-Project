# Task 3 — Baseline Machine Learning Model

## Project Overview

This project is the third task of the Data Science project series. The objective of this task is to **build a baseline machine learning model, evaluate its performance using suitable metrics, and discuss its limitations**.

The same prepared **Smartphone Dataset** used in Task 1 (Data Preparation) and Task 2 (Exploratory Data Analysis) is used for this task.

For the baseline model, **Linear Regression** is used to predict smartphone prices based on numerical smartphone specifications.

---

## Dataset

The dataset used in this project is:

**`smartphones_prepared.csv`**

The dataset was prepared during Task 1 by:

* Removing duplicate records
* Handling missing values
* Checking data types
* Cleaning categorical values
* Preparing the dataset for further analysis

The prepared dataset contains approximately:

* **2256 records**
* **14 original columns**

Additional numerical features were created during the EDA/model preparation stage from text-based smartphone specifications.

---

## Objective

The main objectives of this task are:

1. Load the prepared Smartphone Dataset.
2. Prepare the target variable (`price`).
3. Convert text-based smartphone specifications into numerical features.
4. Select suitable numerical features for modeling.
5. Split the dataset into training and testing sets.
6. Build a baseline Linear Regression model.
7. Generate price predictions.
8. Evaluate the model using suitable regression metrics.
9. Visualize actual and predicted prices.
10. Analyze prediction errors.
11. Discuss the limitations of the baseline model.

---

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook

---

## Machine Learning Problem

This project is treated as a **Supervised Regression Problem**.

### Input Features

The model uses numerical smartphone features such as:

* Expert Rating
* User Rating
* RAM
* Storage
* Battery Capacity
* Rear Camera
* Front Camera
* Display Size

### Target Variable

The target variable is:

**`price_numeric`**

The original `price` column contains text-based values, so it is converted into a numerical format before training the model.

---

## Feature Preparation

Several columns in the dataset are stored as text even though they contain numerical information.

For example:

* `ram_internal_memory`
* `battery`
* `rear_cameras`
* `front_cameras`
* `display`
* `user_rating`
* `price`

Numerical values are extracted from these columns to create model-ready features.

### Created Features

| Feature               | Description                  |
| --------------------- | ---------------------------- |
| `price_numeric`       | Numerical smartphone price   |
| `user_rating_numeric` | Numerical user rating        |
| `ram_gb`              | RAM converted into GB        |
| `storage_gb`          | Storage converted into GB    |
| `battery_mAh`         | Battery capacity in mAh      |
| `rear_camera_mp`      | Rear camera megapixel value  |
| `front_camera_mp`     | Front camera megapixel value |
| `display_size`        | Display size in inches       |

RAM and storage values containing MB, GB, and TB are converted into consistent units.

For example:

* 1024 MB = 1 GB
* 1 TB = 1024 GB

---

## Data Splitting

The dataset is divided into two parts:

* **80% Training Data**
* **20% Testing Data**

The training data is used to train the Linear Regression model, while the testing data is used to evaluate how well the model performs on unseen data.

A `random_state` is used so that the same train-test split can be reproduced.

---

## Baseline Model

### Linear Regression

**Linear Regression** is selected as the baseline model.

The purpose of using a baseline model is to establish a simple reference point for prediction performance before trying more advanced machine learning algorithms.

The model learns the relationship between the selected smartphone features and their prices.

The general idea is:

```text
Smartphone Features → Linear Regression → Predicted Price
```

---

## Model Training

The Linear Regression model is trained using the training dataset.

The model learns coefficients for the selected features and uses them to estimate smartphone prices for unseen records.

---

## Model Evaluation

Since smartphone price prediction is a **regression problem**, the following metrics are used:

### 1. Mean Absolute Error (MAE)

MAE measures the average absolute difference between the actual and predicted prices.

A lower MAE indicates smaller prediction errors.

For example, if the MAE is ₹5,000, the model's predictions differ from the actual prices by approximately ₹5,000 on average in absolute terms.

---

### 2. Mean Squared Error (MSE)

MSE calculates the average squared difference between actual and predicted values.

Large errors have a greater effect on MSE because the errors are squared.

A lower MSE indicates better performance.

---

### 3. Root Mean Squared Error (RMSE)

RMSE is calculated as:

```text
RMSE = √MSE
```

RMSE is useful because it is expressed in the same unit as the target variable.

For this project, RMSE is expressed in the same price units as the smartphone prices.

A lower RMSE indicates smaller prediction errors.

---

### 4. R² Score

R² Score measures how much of the variation in smartphone prices is explained by the model.

A higher R² generally indicates that the model explains more of the variation in the target variable.

However, R² should not be considered alone. MAE, RMSE, and the prediction-error distribution should also be examined.

---

## Actual vs Predicted Prices

An **Actual vs Predicted Price** scatter plot is created to visually evaluate model performance.

The x-axis represents:

```text
Actual Price
```

The y-axis represents:

```text
Predicted Price
```

Predictions closer to the reference relationship between actual and predicted prices indicate smaller prediction errors.

---

## Prediction Error Analysis

Prediction errors are calculated using:

```text
Error = Actual Price − Predicted Price
```

The distribution of errors is visualized using a histogram.

This helps identify:

* Whether errors are centered around zero
* Whether the model systematically overpredicts or underpredicts
* Whether there are unusually large prediction errors

The largest prediction errors are also inspected to identify smartphones for which the baseline model performs poorly.

---

## Feature Coefficients

Because Linear Regression is used, the model provides coefficients for each numerical feature.

These coefficients show how each feature contributes to the model's linear prediction while holding the other included features constant.

However, the coefficients should be interpreted carefully because the features have different units and scales.

---

## Limitations of the Baseline Model

The baseline model has several limitations.

### 1. Linear Relationship Assumption

Linear Regression assumes a linear relationship between the input features and smartphone price.

In reality, smartphone pricing may involve complex and nonlinear relationships.

---

### 2. Categorical Features Are Not Fully Utilized

Important categorical features such as:

* Brand
* Processor
* Operating System

are not directly included in the baseline numerical model.

These features may contain useful information for predicting smartphone prices.

---

### 3. Text Information Is Not Used

The dataset contains text-based information such as:

* Model Name
* Reviews
* Additional Features

The baseline model does not use the information contained in these text fields.

---

### 4. Missing Information

Some smartphone specifications may not be available in the original dataset.

Although missing numerical values are handled using median imputation, this replaces unavailable information with an estimated value rather than the actual specification.

---

### 5. Outliers

Smartphone prices can vary significantly between budget and premium devices.

Extreme price values can influence Linear Regression and increase prediction errors.

---

### 6. Limited Features

The model uses only selected numerical smartphone specifications.

Other factors that may influence smartphone prices include:

* Brand reputation
* Processor generation
* Display technology
* Build quality
* Launch date
* Market demand
* Discounts
* Product availability

These factors are not fully represented in the baseline model.

---

### 7. Baseline Model Simplicity

Linear Regression is intentionally used as a simple baseline.

It may not capture complex relationships between smartphone specifications and price.

More advanced models can be tested in future work.

---

## Future Improvements

The model can potentially be improved by:

* Including categorical features such as brand and processor
* Using one-hot encoding for categorical variables
* Performing better feature engineering
* Handling outliers carefully
* Using additional smartphone specifications
* Applying feature scaling where appropriate
* Comparing multiple machine learning algorithms
* Using models such as Decision Tree, Random Forest, or Gradient Boosting
* Performing hyperparameter tuning
* Using cross-validation
* Extracting useful information from review text

---

## Project Workflow

```text
Prepared Smartphone Dataset
            ↓
      Data Inspection
            ↓
   Feature Preparation
            ↓
 Convert Price to Numeric
            ↓
    Select Features
            ↓
    Handle Missing Values
            ↓
     Train-Test Split
            ↓
    Linear Regression
            ↓
      Make Predictions
            ↓
     Model Evaluation
            ↓
 Actual vs Predicted Plot
            ↓
   Error Analysis
            ↓
     Discuss Limitations
```

---

## Project Structure

```text
Task_3/
│
├── smartphones_prepared.csv
├── Task_3_Baseline_Model.ipynb
├── smartphone_price_predictions.csv
└── README.md
```

---

## How to Run

### 1. Install Required Libraries

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### 2. Open Jupyter Notebook

```bash
jupyter notebook
```

### 3. Place the Dataset

Make sure the following file is in the same folder as the notebook:

```text
smartphones_prepared.csv
```

### 4. Run the Notebook

Run the notebook cells sequentially from data loading through model evaluation and limitations.

---

## Expected Outputs

The notebook produces:

* Dataset information
* Missing-value analysis
* Prepared numerical features
* Training and testing dataset sizes
* Trained Linear Regression model
* MAE
* MSE
* RMSE
* R² Score
* Actual vs Predicted Price plot
* Prediction error distribution
* Feature coefficient analysis
* Saved prediction results

---

## Conclusion

In this task, a **Linear Regression model** was developed as a baseline model for predicting smartphone prices using numerical smartphone specifications.

The model was evaluated using **MAE, MSE, RMSE, and R² Score**. These metrics provide a quantitative understanding of the baseline model's prediction performance.

The Actual vs Predicted visualization and prediction-error analysis were also used to understand the model's behavior.

Although Linear Regression provides a useful starting point, smartphone prices can depend on nonlinear relationships, categorical information, text information, brand effects, and other market-related factors. Therefore, the baseline model provides a foundation for experimenting with more advanced machine learning approaches in future tasks.

---

## Author

**Mihir Prajapati**

### Project

**Data Science — Task 3: Build a Baseline Model**

### Dataset

**Smartphone Dataset**

### Model

**Linear Regression**
