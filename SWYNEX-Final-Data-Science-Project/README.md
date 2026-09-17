# Smartphone Price Prediction — End-to-End Data Science Project

## Project Overview

This project combines the complete Data Science workflow performed across the previous tasks into one end-to-end project using the **Smartphone Dataset**.

The project starts with understanding the problem and preparing the raw dataset, followed by Exploratory Data Analysis (EDA), feature engineering, baseline machine learning modeling, model evaluation, error analysis, and final conclusions.

The main goal of this project is to understand smartphone specifications and their relationship with smartphone prices and build a baseline model to predict smartphone prices.

---

## Problem Statement

Smartphone prices can vary significantly depending on their specifications and features, including RAM, storage, battery capacity, camera specifications, display size, and ratings.

The objective of this project is to analyze the Smartphone Dataset, identify useful patterns and relationships between smartphone specifications and price, and build a baseline machine learning model for predicting smartphone prices.

### Key Questions

* What is the structure and quality of the Smartphone Dataset?
* Are there missing values or duplicate records?
* How are smartphone prices distributed?
* What are the distributions of RAM, storage, battery, camera, and display?
* How are smartphone specifications related to price?
* Can numerical smartphone specifications be used to predict smartphone price?
* How well does the baseline model perform?
* What are the limitations of the model?
* How can the model be improved in the future?

---

## Dataset

The project uses the same Smartphone Dataset throughout all four tasks.

### Dataset Files

* `smartphones_uncleaned.csv` — Original raw dataset
* `smartphones_prepared.csv` — Cleaned and prepared dataset used for EDA and modeling

The prepared dataset contains approximately:

* **2256 records**
* **14 original columns**

### Original Features

The dataset includes information such as:

* `model_name`
* `price`
* `expert_rating`
* `user_rating`
* `processor`
* `rear_cameras`
* `front_cameras`
* `display`
* `ram_internal_memory`
* `battery`
* `operating_system`
* `additional_features`
* `review`
* `review_link`

---

# Project Workflow

```text
Problem Statement
       ↓
Data Preparation
       ↓
Data Cleaning
       ↓
Exploratory Data Analysis
       ↓
Feature Engineering
       ↓
Feature Selection
       ↓
Train-Test Split
       ↓
Baseline Model
       ↓
Predictions
       ↓
Model Evaluation
       ↓
Error Analysis
       ↓
Limitations
       ↓
Final Conclusion
```

---

# 1. Problem Definition

The project treats smartphone price prediction as a **supervised regression problem**.

### Input

Selected smartphone specifications such as:

* Expert Rating
* User Rating
* RAM
* Storage
* Battery
* Rear Camera
* Front Camera
* Display Size

### Target

The target variable is:

```text
price_numeric
```

which represents the numerical smartphone price.

---

# 2. Data Preparation

The first stage of the project focused on cleaning and preparing the raw Smartphone Dataset.

### Data Preparation Steps

* Loaded the raw dataset using Pandas
* Inspected dataset structure
* Checked column names and data types
* Identified missing values
* Detected duplicate records
* Removed duplicate records
* Separated numerical and categorical columns
* Handled numerical missing values using the median
* Handled categorical missing values using the mode
* Performed basic statistical analysis
* Performed final data-quality checks
* Exported the cleaned dataset

The resulting prepared dataset was saved as:

```text
smartphones_prepared.csv
```

---

# 3. Exploratory Data Analysis

After preparing the dataset, Exploratory Data Analysis was performed to understand the data and identify patterns.

## Dataset Inspection

The dataset was inspected using:

```python
df.info()
```

and:

```python
df.describe()
```

Missing values and duplicate records were also checked.

---

## Price Analysis

The original `price` column was stored as text, so it was converted into a numerical feature:

```text
price_numeric
```

The distribution of smartphone prices was analyzed using:

* Histogram
* Box plot

These visualizations help understand the spread of smartphone prices and identify potential outliers.

---

## Rating Analysis

The following ratings were analyzed:

* Expert Rating
* User Rating

Histograms were used to understand the distribution of ratings across smartphones.

---

## Smartphone Specification Analysis

The following specifications were analyzed:

* RAM
* Storage
* Battery
* Rear Camera
* Front Camera
* Display Size

Histograms and other visualizations were used to understand their distributions.

---

## Categorical Feature Analysis

Categorical features such as:

* Operating System
* Processor
* Brand

were explored using appropriate count plots and bar plots.

The brand information was extracted from the smartphone model information where applicable.

---

# 4. Feature Engineering

Many important smartphone specifications were stored as text.

To use them in machine learning, numerical information was extracted from these columns.

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

### Unit Conversion

RAM and storage values were converted into consistent units.

Examples:

```text
1024 MB = 1 GB
1 TB = 1024 GB
```

This conversion made the features suitable for numerical analysis and machine learning.

---

# 5. Relationship Analysis

Scatter plots were created to investigate relationships between smartphone price and selected numerical features.

The following relationships were analyzed:

* RAM vs Price
* Storage vs Price
* Battery vs Price
* User Rating vs Price
* Display Size vs Price

A correlation matrix and heatmap were also created to examine linear relationships between numerical variables.

Correlation was used as an exploratory measure and does not by itself establish causation.

---

# 6. Baseline Machine Learning Model

The machine learning stage treats the problem as a **regression problem** because smartphone price is a continuous numerical value.

## Model Used

**Linear Regression**

Linear Regression was selected as the baseline model because it is simple, interpretable, and provides a reference point for future model improvements.

### Selected Features

The baseline model uses:

```text
expert_rating
user_rating_numeric
ram_gb
storage_gb
battery_mAh
rear_camera_mp
front_camera_mp
display_size
```

### Target Variable

```text
price_numeric
```

---

# 7. Data Splitting

The dataset was divided into:

* **80% Training Data**
* **20% Testing Data**

The training data was used to train the model, while the testing data was used to evaluate its performance on unseen observations.

A fixed `random_state` was used to make the train-test split reproducible.

---

# 8. Model Training

The Linear Regression model was trained using the selected numerical features.

The model learns the relationship between the smartphone specifications and price and then uses this relationship to generate predictions for the test dataset.

---

# 9. Model Evaluation

Because this is a regression problem, the following evaluation metrics were used.

## Mean Absolute Error (MAE)

MAE measures the average absolute difference between actual and predicted prices.

A lower MAE indicates smaller average prediction errors.

---

## Mean Squared Error (MSE)

MSE measures the average squared difference between actual and predicted prices.

Large prediction errors have a greater effect on this metric because the errors are squared.

A lower MSE indicates smaller squared prediction errors.

---

## Root Mean Squared Error (RMSE)

RMSE is calculated as:

```text
RMSE = √MSE
```

RMSE is expressed in the same unit as the target variable, making it easier to interpret than MSE.

A lower RMSE indicates smaller prediction errors.

---

## R² Score

R² Score measures the proportion of variation in smartphone price that is explained by the model.

A higher R² generally indicates that the model explains more of the variation in the target.

However, R² should be interpreted together with MAE, MSE, RMSE, and error analysis.

---

# 10. Actual vs Predicted Analysis

An Actual vs Predicted scatter plot was created to compare:

```text
Actual Smartphone Price
```

with:

```text
Predicted Smartphone Price
```

A reference line was also included.

Predictions closer to the reference relationship indicate smaller prediction errors.

---

# 11. Prediction Error Analysis

Prediction errors were calculated as:

```text
Error = Actual Price - Predicted Price
```

Absolute errors were also calculated.

The error distribution was visualized using a histogram to understand the overall behavior of the model's prediction errors.

The observations with the largest absolute errors were also examined.

---

# 12. Feature Coefficients

Since Linear Regression was used, coefficients were examined to understand the direction of the relationships learned by the model.

The coefficients represent the change in the model's predicted price associated with a one-unit change in a feature, while holding the other included features constant.

Because the features have different units and scales, the coefficients should not be interpreted as a direct feature-importance ranking.

---

# 13. Model Limitations

The baseline model has several limitations.

## 1. Linear Relationship Assumption

Linear Regression assumes a linear relationship between the selected features and smartphone price.

Real-world smartphone pricing may contain nonlinear relationships.

---

## 2. Limited Features

Only selected numerical specifications were used.

Other factors that can influence smartphone prices may include:

* Brand reputation
* Processor generation
* Display technology
* Build quality
* Launch date
* Market demand
* Product availability
* Discounts

These factors are not fully represented in the baseline model.

---

## 3. Categorical Features

Important categorical information such as:

* Brand
* Processor
* Operating System

was not directly included in the baseline numerical model.

These features may provide additional predictive information.

---

## 4. Text Information

The model does not directly use information from:

* Reviews
* Model Names
* Additional Features

Text-based information could potentially provide useful signals for price prediction.

---

## 5. Outliers

Smartphone prices can vary considerably between budget, mid-range, and premium devices.

Extreme values may influence Linear Regression and increase prediction errors.

---

## 6. Missing Specifications

Some smartphone specifications are incomplete or unavailable in the original dataset.

Median imputation provides a practical solution for the baseline model, but it does not recover the actual missing specification.

---

## 7. Baseline Model Simplicity

Linear Regression was selected intentionally as a baseline.

More advanced machine learning algorithms may be able to capture complex relationships that Linear Regression cannot.

---

# 14. Future Improvements

The project can be improved in several ways.

### Feature Engineering

* Create additional smartphone specification features
* Improve extraction of camera specifications
* Create processor-related features
* Create brand-related features
* Extract useful information from additional features

### Categorical Data

Categorical features can be included using techniques such as:

* One-Hot Encoding
* Label Encoding where appropriate

### Text Data

The review column could be analyzed using Natural Language Processing techniques.

Possible approaches include:

* Text preprocessing
* Sentiment analysis
* TF-IDF
* Text-based features

### Machine Learning

Additional models could be tested, such as:

* Decision Tree Regressor
* Random Forest Regressor
* Gradient Boosting Regressor

These models could then be compared with the Linear Regression baseline.

### Model Validation

Future versions can use:

* Cross-validation
* Hyperparameter tuning
* More detailed error analysis

---

# 15. Key Project Outcomes

This project demonstrates the complete Data Science workflow:

### Data Preparation

The raw Smartphone Dataset was cleaned and prepared for analysis.

### Exploratory Data Analysis

The dataset was explored using descriptive statistics and visualizations to understand smartphone characteristics and price relationships.

### Feature Engineering

Important numerical information was extracted from text-based smartphone specifications.

### Modeling

A Linear Regression model was developed as the baseline model.

### Evaluation

The model was evaluated using:

* MAE
* MSE
* RMSE
* R² Score

### Error Analysis

Actual vs predicted prices and prediction errors were analyzed to understand model behavior.

### Limitations

The assumptions, missing information, limited features, categorical variables, text data, and simplicity of the baseline model were documented.

---

# 16. Conclusion

This project combines **Data Preparation, Exploratory Data Analysis, Feature Engineering, Machine Learning, Model Evaluation, and Documentation** into one complete Data Science workflow.

The Smartphone Dataset was first cleaned and prepared, followed by EDA to understand the distributions and relationships among smartphone features.

Text-based smartphone specifications were converted into numerical features such as RAM, storage, battery capacity, camera specifications, display size, and user rating.

A **Linear Regression model** was then developed as a baseline model for predicting smartphone prices. The model was evaluated using MAE, MSE, RMSE, and R² Score, along with actual-vs-predicted visualization and prediction-error analysis.

The baseline model provides a starting point for smartphone price prediction. However, smartphone pricing can depend on many factors that are not fully represented by the selected numerical features. Therefore, categorical variables, text information, additional features, nonlinear models, and improved feature engineering can be explored in future work.

Overall, this project demonstrates an end-to-end approach to solving a Data Science problem, from **problem definition and data preparation to EDA, modeling, evaluation, and final conclusions**.

---

# 17. Project Structure

```text
Smartphone_Price_Prediction/
│
├── smartphones_uncleaned.csv
├── smartphones_prepared.csv
├── Task_4_End_to_End_Project.ipynb
├── smartphone_price_predictions.csv
└── README.md
```

---

# 18. How to Run the Project

## Step 1 — Install Required Libraries

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

## Step 2 — Open Jupyter Notebook

```bash
jupyter notebook
```

## Step 3 — Place the Dataset

Make sure the required dataset files are available in the project directory:

```text
smartphones_uncleaned.csv
smartphones_prepared.csv
```

## Step 4 — Open the Notebook

Open:

```text
Task_4_End_to_End_Project.ipynb
```

## Step 5 — Run the Notebook

Run the notebook cells sequentially from:

```text
Problem Statement
```

through:

```text
Final Conclusion
```

---

# 19. Output Files

The project generates the following important output:

```text
smartphones_prepared.csv
```

Cleaned dataset produced during data preparation.

```text
smartphone_price_predictions.csv
```

Contains actual and predicted smartphone prices along with prediction errors.

---

# 20. Author

**Mihir Prajapati**

## Project

**End-to-End Smartphone Price Prediction**

## Task

**Task 4 — Combine Problem Statement, Data Preparation, EDA, Modeling, and Conclusions**

## Domain

**Data Science / Machine Learning**

## Model

**Linear Regression**
