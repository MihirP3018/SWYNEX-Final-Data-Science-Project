# Exploratory Data Analysis (EDA) - Smartphone Dataset

## Project Overview

This project performs **Exploratory Data Analysis (EDA)** on the prepared Smartphone Dataset `smartphones_prepared.csv`.

The purpose of this task is to understand the dataset, identify patterns, study distributions, compare smartphone features, and analyze relationships between price, ratings, and hardware specifications using Python.

This task uses the **same Smartphone Dataset from Task 1 (Data Preparation)**.

---

## Dataset

**Dataset File:** `smartphones_prepared.csv`

The dataset contains information about smartphones, including:

* Model Name
* Price
* Expert Rating
* User Rating
* Processor
* Rear Cameras
* Front Cameras
* Display
* RAM and Internal Storage
* Battery
* Operating System
* Additional Features
* Review
* Review Link

The prepared dataset contains **2256 records and 14 original columns**.

---

## Objectives

The main objectives of this EDA task are:

1. Load and inspect the Smartphone Dataset.
2. Understand the structure and data types of the dataset.
3. Check missing values and duplicate records.
4. Generate descriptive statistics.
5. Convert important text-based features into numerical values for analysis.
6. Analyze smartphone price distribution.
7. Analyze expert and user ratings.
8. Analyze RAM, storage, battery, camera, and display features.
9. Analyze categorical variables such as operating system, processor, and brand.
10. Study relationships between price and different smartphone features.
11. Perform correlation analysis using a correlation matrix and heatmap.
12. Understand overall patterns and trends in the smartphone dataset.

---

## Technologies Used

* **Python**
* **Pandas** - Data loading, cleaning and data manipulation
* **NumPy** - Numerical operations
* **Matplotlib** - Data visualization
* **Seaborn** - Statistical visualization
* **Jupyter Notebook** - Development environment

---

## Dataset Inspection

The dataset is loaded using Pandas:

```python
df = pd.read_csv("smartphones_prepared.csv")
```

The following functions are used to understand the dataset:

* `head()`
* `shape`
* `info()`
* `columns`
* `isnull().sum()`
* `duplicated().sum()`
* `describe()`

These checks provide information about the number of records, columns, data types, missing values, duplicate records, and statistical properties.

---

## Descriptive Statistics

Descriptive statistics are generated using:

```python
df.describe(include="all").T
```

This helps understand numerical and categorical variables.

For numerical variables, the analysis includes:

* Count
* Mean
* Standard deviation
* Minimum
* 25th percentile
* Median
* 75th percentile
* Maximum

---

# Feature Conversion for EDA

Some important smartphone attributes are stored as text. Therefore, numerical values are extracted from these columns before performing numerical analysis and visualization.

## Price

The price column contains values with the Indian Rupee symbol and commas.

Example:

```text
₹12,999
```

It is converted into:

```text
12999
```

A new column is created:

```text
price_numeric
```

---

## User Rating

The numerical rating is extracted from the `user_rating` column.

A new column is created:

```text
user_rating_numeric
```

This allows user ratings to be used in histograms and scatter plots.

---

## RAM

RAM information is available inside the `ram_internal_memory` column.

Examples:

```text
8 GB RAM | 128 GB Storage
6 GB RAM | 128 GB Storage
512 MB RAM | 4 GB Storage
```

RAM values are converted into GB.

For example:

```text
8 GB RAM → 8 GB
512 MB RAM → 0.5 GB
```

A new column is created:

```text
ram_gb
```

---

## Storage

Storage information is also extracted from the `ram_internal_memory` column.

Different units are converted into GB.

Examples:

```text
128 GB Storage → 128 GB
1 TB Storage → 1024 GB
256 MB Storage → 0.25 GB
```

A new column is created:

```text
storage_gb
```

---

## Battery

Battery capacity is extracted from the `battery` column.

The value is represented in:

```text
mAh
```

A new column is created:

```text
battery_mAh
```

---

## Rear Camera

The rear camera megapixel value is extracted from the `rear_cameras` column.

A new column is created:

```text
rear_camera_mp
```

---

## Front Camera

The front camera megapixel value is extracted from the `front_cameras` column.

A new column is created:

```text
front_camera_mp
```

---

## Display Size

The display size is extracted from the `display` column.

The value is represented in inches.

A new column is created:

```text
display_size
```

---

## Brand

The brand is extracted from the smartphone model name.

For example:

```text
Samsung Galaxy S24
```

The extracted brand is:

```text
Samsung
```

A new column is created:

```text
brand
```

---

# Exploratory Data Analysis

## 1. Price Analysis

Price is one of the main variables analyzed in the dataset.

### Histogram

A histogram is used to understand the distribution of smartphone prices.

```python
sns.histplot(df["price_numeric"].dropna(), bins=30, kde=True)
```

The histogram helps identify whether smartphone prices are concentrated in a particular range and whether the distribution contains high-priced values.

### Box Plot

A box plot is used to examine:

* Median price
* Spread of prices
* Possible outliers

---

# 2. Rating Analysis

Two types of ratings are analyzed:

* Expert Rating
* User Rating

### Expert Rating

A histogram is used to understand the distribution of expert ratings.

### User Rating

A histogram is used to understand how users have rated the smartphones.

These visualizations help compare the overall rating patterns in the dataset.

---

# 3. Hardware Feature Analysis

The following smartphone hardware features are analyzed:

* RAM
* Storage
* Battery
* Rear Camera
* Front Camera
* Display Size

## RAM Analysis

A count plot is used to identify commonly available RAM configurations.

Examples include different RAM capacities such as:

```text
4 GB
6 GB
8 GB
12 GB
```

## Storage Analysis

A count plot is used to identify common storage configurations.

## Battery Analysis

A histogram is used to understand the distribution of battery capacities.

## Camera Analysis

Histograms are used to analyze:

* Rear camera megapixels
* Front camera megapixels

## Display Analysis

A histogram is used to understand the distribution of smartphone display sizes.

---

# 4. Categorical Analysis

Categorical variables are also analyzed using bar plots.

The main categorical variables are:

* Operating System
* Processor
* Brand

## Operating System

A bar plot is used to identify the number of smartphones available for each operating system.

## Processor

The top 15 processors are displayed using a bar plot.

This helps identify the processors that appear most frequently in the dataset.

## Brand

The top 15 smartphone brands are displayed using a bar plot.

This provides an overview of the brands represented in the dataset.

---

# 5. Relationship Analysis

Scatter plots are used to study relationships between smartphone price and different features.

The following relationships are analyzed:

### Expert Rating vs Price

This plot helps examine the relationship between expert ratings and smartphone prices.

### User Rating vs Price

This plot helps examine whether user ratings vary with smartphone price.

### RAM vs Price

This plot helps understand how RAM capacity is distributed across different price levels.

### Storage vs Price

This plot helps examine the relationship between storage capacity and smartphone price.

### Battery vs Price

This plot helps analyze battery capacity across different smartphone prices.

### Display Size vs Price

This plot helps examine whether display size varies with smartphone price.

---

# 6. Correlation Analysis

Correlation analysis is performed on numerical features.

The following columns are included:

```text
price_numeric
expert_rating
user_rating_numeric
ram_gb
storage_gb
battery_mAh
rear_camera_mp
front_camera_mp
display_size
```

A correlation matrix is created using:

```python
df[correlation_columns].corr()
```

A heatmap is then used to visualize the correlations.

## Interpretation

Correlation values range from:

```text
-1 to +1
```

Generally:

* A value close to `+1` indicates a strong positive linear relationship.
* A value close to `0` indicates a weak or no linear relationship.
* A value close to `-1` indicates a strong negative linear relationship.

The heatmap makes it easier to identify relationships between smartphone features.

---

# Visualizations Used

The following visualizations are included in the notebook:

1. Price Histogram
2. Price Box Plot
3. Expert Rating Histogram
4. User Rating Histogram
5. RAM Count Plot
6. Storage Count Plot
7. Battery Histogram
8. Rear Camera Histogram
9. Front Camera Histogram
10. Display Size Histogram
11. Operating System Bar Plot
12. Top 15 Processor Bar Plot
13. Top 15 Brand Bar Plot
14. Expert Rating vs Price Scatter Plot
15. User Rating vs Price Scatter Plot
16. RAM vs Price Scatter Plot
17. Storage vs Price Scatter Plot
18. Battery vs Price Scatter Plot
19. Display Size vs Price Scatter Plot
20. Correlation Heatmap

---

# Project Structure

```text
Smartphone EDA/
│
├── smartphones_prepared.csv
├── smartphones_eda_only.ipynb
└── README.md
```

---

# How to Run the Project

## Step 1: Install Required Libraries

Install the required Python libraries if they are not already installed:

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

## Step 2: Keep the Dataset and Notebook Together

Make sure these files are in the same folder:

```text
smartphones_prepared.csv
smartphones_eda_only.ipynb
```

## Step 3: Open Jupyter Notebook

Run:

```bash
jupyter notebook
```

Then open:

```text
smartphones_eda_only.ipynb
```

## Step 4: Run the Notebook

Run the cells from top to bottom.

The notebook will load the dataset, perform the EDA, and generate the required tables and visualizations.

---

# Key EDA Observations

The EDA helps understand the following aspects of the Smartphone Dataset:

* Smartphone price distribution
* Distribution of expert ratings
* Distribution of user ratings
* Common RAM configurations
* Common storage capacities
* Battery capacity distribution
* Rear and front camera specifications
* Smartphone display sizes
* Common operating systems
* Frequently occurring processors
* Distribution of smartphone brands
* Relationship between price and ratings
* Relationship between price and hardware specifications
* Correlations between numerical smartphone features

The exact observations can be identified from the graphs and statistical outputs generated in the notebook.

---

# Conclusion

The Exploratory Data Analysis provides an overall understanding of the Smartphone Dataset.

The analysis covers both **numerical and categorical variables** and uses different visualization techniques such as:

* Histograms
* Box plots
* Bar plots
* Count plots
* Scatter plots
* Correlation matrix
* Heatmap

The EDA helps identify distributions, patterns, relationships, and possible outliers in the smartphone data.

This analysis can also be used as a foundation for future tasks such as statistical analysis or machine learning.

---

# Author

**Mihir Prajapati**

## Task

**Exploratory Data Analysis (EDA) - Smartphone Dataset**
