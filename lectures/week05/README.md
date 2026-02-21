# AI-216: Programming for Artificial Intelligence
## Week 05 – NumPy & Pandas: Data-Centric Programming

---

### Lecture Overview

In Weeks 1–4, you learned:
- Python fundamentals and logical thinking
- Functions and Object-Oriented Programming
- Data structures (lists, tuples, dictionaries, sets)

In Week 5, we transition to **data-centric programming**.

We now move from:
- Writing programs about data

To:
- Writing programs that operate on structured datasets efficiently

This week introduces:
- NumPy arrays vs Python lists
- Pandas DataFrames
- Data slicing and filtering

These tools are foundational for machine learning workflows.

---

## Learning Objectives

After this lecture, students will be able to:
- Explain the difference between Python lists and NumPy arrays
- Perform vectorized operations using NumPy
- Create and manipulate Pandas DataFrames
- Slice and filter datasets using conditions
- Understand how data preprocessing prepares for ML models

---

# 1. Python Lists vs NumPy Arrays

NumPy is designed for numerical computing and efficient array operations.

Import NumPy:

```python
import numpy as np
```

NumPy arrays:
- Store homogeneous data
- Support vectorized operations
- Are memory efficient
- Enable multi-dimensional data representation

---

## Basic Comparison

### Python List

```python
numbers = [1, 2, 3, 4]
print(numbers * 2)
```

### NumPy Array

```python
arr = np.array([1, 2, 3, 4])
print(arr * 2)
```

Key Idea:
- List → repetition
- NumPy array → element-wise multiplication

---

## Intermediate Example – Vectorized Computation

```python
scores = np.array([78, 85, 90, 67])
normalized = scores / 100
print(normalized)
```

Vectorization avoids explicit loops and is significantly faster.

---

## Intermediate Example – Boolean Indexing

```python
scores = np.array([78, 85, 90, 67, 45])
passed = scores[scores >= 50]
print(passed)
```

This is similar to filtering rows in datasets.

---

## Advanced Example – 2D Arrays (Matrix Representation)

```python
marks_matrix = np.array([
    [78, 85, 90],
    [88, 92, 79],
    [45, 60, 55]
])

print(marks_matrix)
```

Accessing elements:

```python
print(marks_matrix[0, 1])   # First row, second column
print(marks_matrix[:, 0])   # All rows, first column
```

---

## Advanced Example – Axis-based Operations

```python
print("Mean per student:", np.mean(marks_matrix, axis=1))
print("Mean per subject:", np.mean(marks_matrix, axis=0))
```

Axis explanation:
- axis=0 → column-wise
- axis=1 → row-wise

---

## Advanced Example – Reshaping & Broadcasting

```python
arr = np.array([1, 2, 3, 4, 5, 6])
reshaped = arr.reshape(2, 3)
print(reshaped)
```

Broadcasting example:

```python
matrix = np.array([[1, 2, 3],
                   [4, 5, 6]])

print(matrix + 10)
```

AI Connection:
NumPy arrays represent feature matrices used in machine learning.

---

# 2. Introduction to Pandas DataFrames

Import Pandas:

```python
import pandas as pd
```

A DataFrame is a table-like data structure built on top of NumPy.

It provides:
- Column-based operations
- Labeled indexing
- Grouping and aggregation
- Data cleaning tools
- File I/O (reading and writing datasets)

---

## Basic Example – Creating a DataFrame

```python
data = {
    "Name": ["Ali", "Sara", "Ahmed"],
    "Marks": [78, 92, 65]
}

df = pd.DataFrame(data)
print(df)
```

---

## Reading Data from CSV

In real-world data science, datasets are rarely typed manually. They are loaded from files.

```python
df_csv = pd.read_csv("students.csv")
print(df_csv.head())
```

Common parameters:

```python
df_csv = pd.read_csv("students.csv", sep=",", header=0)
```

---

## Writing Data to CSV

After processing data, we often export results.

```python
df.to_csv("processed_students.csv", index=False)
```

Exporting filtered data:

```python
high_scorers = df[df["Marks"] > 80]
high_scorers.to_csv("high_scorers.csv", index=False)
```

This is common in ML pipelines when saving cleaned datasets.

---

## Basic Inspection Methods

```python
print(df.head())
print(df.tail())
print(df.info())
print(df.describe())
```

These are essential for dataset understanding.

---

## Intermediate Example – Selecting Data

```python
print(df.loc[0])
print(df.loc[:, "Marks"])
print(df.iloc[0:2, 0:2])
```

Difference:
- loc → label-based
- iloc → position-based

---

## Intermediate Example – Creating Derived Columns

```python
df["Passed"] = df["Marks"] >= 50
df["Percentage"] = df["Marks"] / 100
print(df)
```

---

## Intermediate Example – Sorting

```python
sorted_df = df.sort_values(by="Marks", ascending=False)
print(sorted_df)
```

---

## Advanced Example – Multiple Conditions Filtering

```python
filtered = df[(df["Marks"] > 60) & (df["Marks"] < 90)]
print(filtered)
```

---

## Advanced Example – Applying Custom Functions

```python
def grade_function(mark):
    if mark >= 85:
        return "A"
    elif mark >= 70:
        return "B"
    elif mark >= 50:
        return "C"
    else:
        return "Fail"


df["Grade"] = df["Marks"].apply(grade_function)
print(df)
```

---

## Advanced Example – Working with Larger Structured Data

```python
sales_data = {
    "Category": ["Electronics", "Clothing", "Electronics", "Clothing", "Groceries"],
    "Revenue": [5000, 3000, 7000, 2000, 4000],
    "Units": [5, 10, 7, 8, 15]
}

sales_df = pd.DataFrame(sales_data)

summary = sales_df.groupby("Category").agg({
    "Revenue": "sum",
    "Units": "mean"
})

print(summary)
```

AI Connection:
DataFrames are the primary structure for feature engineering and ML preprocessing.

---

Import Pandas:

```python
import pandas as pd
```

A DataFrame is a table-like data structure.

---

## Basic Example – Creating a DataFrame

```python
data = {
    "Name": ["Ali", "Sara", "Ahmed"],
    "Marks": [78, 92, 65]
}

df = pd.DataFrame(data)
print(df)
```

---

## Basic Operations

```python
print(df.head())
print(df.columns)
print(df.shape)
```

---

## Intermediate Example – Adding Columns

```python
df["Passed"] = df["Marks"] >= 50
print(df)
```

---

## Intermediate Example – Column Operations

```python
df["Percentage"] = df["Marks"] / 100
print(df)
```

---

## Advanced Example – Multiple Calculations

```python
df["Grade"] = pd.cut(
    df["Marks"],
    bins=[0, 50, 70, 85, 100],
    labels=["Fail", "C", "B", "A"]
)

print(df)
```

This mimics rule-based classification.

---

# 3. Data Slicing

---

## Basic Row Selection

```python
print(df.iloc[0])
print(df.iloc[0:2])
```

---

## Basic Column Selection

```python
print(df["Marks"])
print(df[["Name", "Grade"]])
```

---

## Intermediate – Conditional Filtering

```python
high_scorers = df[df["Marks"] > 80]
print(high_scorers)
```

---

## Advanced – Multiple Conditions

```python
filtered = df[(df["Marks"] > 60) & (df["Marks"] < 90)]
print(filtered)
```

---

# 4. Grouping & Aggregation (Pandas Focus)

Grouping is fundamental in analytics.

---

## Intermediate Example – Grouping

```python
sales_data = {
    "Category": ["Electronics", "Clothing", "Electronics", "Clothing"],
    "Revenue": [5000, 3000, 7000, 2000]
}

sales_df = pd.DataFrame(sales_data)

summary = sales_df.groupby("Category")["Revenue"].sum()
print(summary)
```

---

## Advanced Example – Multi-level Aggregation

```python
sales_df["Discounted"] = sales_df["Revenue"] * 0.9

agg = sales_df.groupby("Category").agg({
    "Revenue": "mean",
    "Discounted": "sum"
})

print(agg)
```

AI Connection:
Aggregation prepares features for machine learning models.

---

# 5. Handling Missing Data

Missing data is extremely common in real-world datasets.

---

## Basic Example – Detecting Missing Values

```python
data = {
    "Name": ["Ali", "Sara", "Ahmed"],
    "Marks": [78, None, 65]
}

df_missing = pd.DataFrame(data)

print(df_missing.isnull())
print(df_missing.isnull().sum())
```

---

## Basic Example – Dropping Missing Values

```python
print(df_missing.dropna())
```

Dropping rows with missing values.

---

## Intermediate Example – Filling Missing Values with Mean

```python
filled_mean = df_missing.fillna(df_missing["Marks"].mean())
print(filled_mean)
```

---

## Intermediate Example – Filling with Specific Value

```python
filled_zero = df_missing.fillna(0)
print(filled_zero)
```

---

## Advanced Example – Column-Specific Filling

```python
data = {
    "Marks": [78, None, 65, None],
    "Attendance": [80, 90, None, 70]
}

df2 = pd.DataFrame(data)

# Fill Marks with mean, Attendance with median

df2["Marks"] = df2["Marks"].fillna(df2["Marks"].mean())
df2["Attendance"] = df2["Attendance"].fillna(df2["Attendance"].median())

print(df2)
```

---

## Advanced Example – Conditional Filling

```python
# Fill missing Marks only if Attendance > 75

mask = (df2["Marks"].isnull()) & (df2["Attendance"] > 75)
df2.loc[mask, "Marks"] = df2["Marks"].mean()

print(df2)
```

---

## Advanced Example – Dropping Based on Threshold

```python
# Drop rows where more than 1 value is missing

df3 = df2.dropna(thresh=1)
print(df3)
```

Missing data handling is critical before training ML models.

---

# 6. From Python Structures to DataFrames

Example: Converting list of dictionaries to DataFrame

```python
students = [
    {"Name": "Ali", "Marks": 78},
    {"Name": "Sara", "Marks": 92}
]

converted_df = pd.DataFrame(students)
print(converted_df)
```

This connects Week 4 structures to Pandas.

---

# 7. ChatGPT Prompts for Learning (Allowed Use)

Use AI tools for understanding, debugging, and reasoning.

---

## A. NumPy Understanding

- "Why does NumPy array multiplication behave differently from lists?"
- "Explain vectorization with a simple example"
- "When should I prefer NumPy over lists?"

---

## B. Pandas DataFrames

- "How do I convert a dictionary into a DataFrame?"
- "What is the difference between iloc and loc?"
- "How do I add a computed column?"

---

## C. Filtering & Slicing

- "How does boolean indexing work in Pandas?"
- "Why do I need parentheses in multiple conditions?"

---

## D. Debugging & Data Thinking

- "Why is my filtered DataFrame empty?"
- "How can I check for missing values in a dataset?"
- "Explain this Pandas code step by step"

---

<!-- # 8. Looking Ahead

In Week 6, we will explore:
- Exploratory Data Analysis (EDA)
- Data visualization
- Feature preparation

NumPy and Pandas will become the backbone of your ML workflow.

---

**End of Week 05 Lecture**
 -->
