# Smartphone Dataset – Data Preparation

## Project Overview

This project performs **data preparation and cleaning** on the Smartphone Dataset using **Python, NumPy, and Pandas**.

The main goal is to prepare the raw dataset for further analysis by checking and handling:

- Missing values
- Duplicate records
- Numerical columns
- Categorical columns
- Basic data statistics
- Final data quality

No machine learning or data visualization techniques are used in this project.

---

## Technologies Used

- Python
- NumPy
- Pandas
- Jupyter Notebook / Google Colab

---

## Dataset

The project uses the raw/uncleaned Smartphone Dataset:

**File:** `smartphones_uncleaned.csv`

The dataset contains information about different smartphones and their specifications.

The raw dataset may contain missing values, duplicate records, and different types of columns, making it suitable for practicing data preparation.

---

# Data Preparation Process

## 1. Import Required Libraries

```python
import numpy as np
import pandas as pd
```

### Explanation

- **NumPy** is used for numerical operations and identifying numerical data types.
- **Pandas** is used for loading, inspecting, cleaning, and saving the dataset.

---

## 2. Load the Dataset

```python
df = pd.read_csv('smartphones_uncleaned.csv')
```

### Explanation

`pd.read_csv()` loads the CSV file into a Pandas DataFrame named `df`.

A DataFrame makes it easy to work with rows and columns of data.

---

## 3. Check Dataset Shape

```python
df.shape
```

### Explanation

The `shape` attribute returns:

```text
(number of rows, number of columns)
```

This helps us understand the size of the dataset.

---

## 4. View the First Few Records

```python
df.head()
```

### Explanation

`head()` displays the first five rows of the dataset by default.

It helps us understand:

- Column names
- Data values
- General structure of the dataset

---

## 5. Check Dataset Information

```python
df.info()
```

### Explanation

`info()` provides important information about the dataset, including:

- Number of rows
- Column names
- Data types
- Number of non-null values
- Memory usage

This is useful for identifying numerical and categorical columns and finding columns containing missing values.

---

## 6. Check Missing Values

```python
df.isnull().sum()
```

### Explanation

`isnull()` identifies missing values, while `sum()` counts the missing values in each column.

This helps us determine which columns require missing-value treatment.

---

## 7. Check Duplicate Records

```python
df.duplicated().sum()
```

### Explanation

`duplicated()` checks whether a row is a duplicate of an earlier row.

`sum()` gives the total number of duplicate records.

---

## 8. Remove Duplicate Records

```python
df = df.drop_duplicates()

print("Shape after removing duplicates:", df.shape)
```

### Explanation

`drop_duplicates()` removes duplicate rows from the dataset.

After removing duplicates, the shape of the dataset is printed to check how many rows remain.

---

## 9. Identify Numerical and Categorical Columns

```python
numric_cols = df.select_dtypes(include=np.number).columns
categorical_cols = df.select_dtypes(include='object').columns
```

### Explanation

The dataset contains different types of columns.

### Numerical columns

These contain numeric values such as:

- Price
- RAM
- Storage
- Display size
- Battery capacity

### Categorical columns

These generally contain text values such as:

- Brand
- Model
- Operating system
- Processor type

`select_dtypes()` is used to separate these columns based on their data types.

> Note: `numric_cols` works correctly, but `numeric_cols` would be a better spelling for the variable name.

---

## 10. Handle Missing Values in Numerical Columns

```python
for column in numric_cols:
    df[column] = df[column].fillna(df[column].median())
```

### Explanation

For every numerical column, missing values are replaced with the **median** of that column.

### Why use median?

Median is often useful for numerical data because it is less affected by extreme values compared with the mean.

For example:

```text
10, 20, 30, 40, 500
```

The median is `30`, while the mean is strongly affected by `500`.

---

## 11. Handle Missing Values in Categorical Columns

```python
for column in categorical_cols:
    if df[column].isnull().sum() > 0:
        df[column] = df[column].fillna(df[column].mode()[0])
```

### Explanation

For categorical columns, missing values are replaced using the **mode**.

The mode is the value that appears most frequently in a column.

For example:

```text
Brand
Samsung
Apple
Samsung
Samsung
Apple
```

The mode is:

```text
Samsung
```

Therefore, missing values can be replaced with `Samsung`.

---

## 12. Verify Missing Values After Cleaning

```python
print("Missing values after handling:")
print(df.isnull().sum().sum())
```

### Explanation

This checks the total number of missing values remaining in the entire DataFrame.

If the output is:

```text
0
```

it means there are no missing values remaining.

---

## 13. Check Categorical Value Distribution

```python
for column in categorical_cols:
    print(f'
{column}:')
    print(df[column].value_counts().head(10))
```

### Explanation

`value_counts()` counts how many times each category appears.

`head(10)` displays the top 10 most frequent values.

This helps identify the most common categories and provides a basic check of the categorical data.

---

## 14. Generate Statistical Summary

```python
df.describe()
```

### Explanation

`describe()` provides statistical information for numerical columns, such as:

- Count
- Mean
- Standard deviation
- Minimum
- 25th percentile
- Median
- 75th percentile
- Maximum

This gives a basic understanding of the numerical data after cleaning.

---

## 15. Final Duplicate Check

```python
print("\nDuplicates after cleaning:", df.duplicated().sum())
```

### Explanation

This confirms whether any duplicate records remain after the cleaning process.

The expected result is:

```text
Duplicates after cleaning: 0
```

---

## 16. Check Final Dataset Shape

```python
print("Final Dataset Shape:", df.shape)
```

### Explanation

This displays the final number of rows and columns after removing duplicates.

---

## 17. Check Final Missing Values

```python
print("Final Missing Values:", df.isnull().sum().sum())
```

### Explanation

This performs one final check to confirm that missing values have been handled.

Expected result:

```text
Final Missing Values: 0
```

---

## 18. Save the Prepared Dataset

```python
df.to_csv("smartphones_prepared.csv", index=False)

print("\nData preparation completed successfully!")
```

### Explanation

The cleaned DataFrame is saved as:

```text
smartphones_prepared.csv
```

`index=False` prevents Pandas from adding the DataFrame index as an extra column.

---

# Complete Data Preparation Workflow

The complete workflow followed in this project is:

```text
Load Raw Dataset
       ↓
Check Dataset Shape
       ↓
View First Records
       ↓
Check Dataset Information
       ↓
Check Missing Values
       ↓
Check Duplicate Records
       ↓
Remove Duplicates
       ↓
Identify Numerical & Categorical Columns
       ↓
Fill Numerical Missing Values Using Median
       ↓
Fill Categorical Missing Values Using Mode
       ↓
Verify Missing Values
       ↓
Check Categorical Values
       ↓
Generate Statistical Summary
       ↓
Final Data Quality Checks
       ↓
Save Prepared Dataset
```

---

# Complete Code

```python
import numpy as np
import pandas as pd

df = pd.read_csv('smartphones_uncleaned.csv')

df.shape

df.head()

df.info()

df.isnull().sum()

df.duplicated().sum()

df = df.drop_duplicates()

print("Shape after removing duplicates:", df.shape)

numric_cols = df.select_dtypes(include=np.number).columns
categorical_cols = df.select_dtypes(include='object').columns

for column in numric_cols:
    df[column] = df[column].fillna(df[column].median())

for column in categorical_cols:
    if df[column].isnull().sum() > 0:
        df[column] = df[column].fillna(df[column].mode()[0])

print("Missing values after handling:")
print(df.isnull().sum().sum())

for column in categorical_cols:
    print(f'\n{column}:')
    print(df[column].value_counts().head(10))

df.describe()

print("\nDuplicates after cleaning:", df.duplicated().sum())
print("Final Dataset Shape:", df.shape)
print("Final Missing Values:", df.isnull().sum().sum())

df.to_csv("smartphones_prepared.csv", index=False)

print("\nData preparation completed successfully!")
```

---

# Final Result

After completing the data preparation process:

- Duplicate records are removed.
- Missing numerical values are replaced with the median.
- Missing categorical values are replaced with the mode.
- Numerical and categorical columns are identified.
- The cleaned dataset is checked again for missing values and duplicates.
- Basic statistical information is generated.
- The prepared dataset is saved as `smartphones_prepared.csv`.

This produces a cleaner and more consistent dataset that can be used for further **data analysis, visualization, or machine learning tasks**.

---

## Conclusion

The Smartphone Dataset was successfully prepared using **NumPy and Pandas**.

The project demonstrates important data preparation techniques such as:

1. Loading a raw dataset
2. Understanding dataset structure
3. Detecting missing values
4. Detecting and removing duplicates
5. Separating numerical and categorical columns
6. Handling missing numerical values using median
7. Handling missing categorical values using mode
8. Performing final data quality checks
9. Saving the prepared dataset

These steps are important before performing further data analysis or building machine learning models.
