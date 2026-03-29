# AI-216 – Programming for Artificial Intelligence
## Week 7 Lecture: File Handling & Data Preprocessing

---

## 1. Lecture Overview

Week: 7  
Phase: Data Handling for AI  
Lecture Duration: ~2 hours  

### Topics Covered
- Reading data from files (CSV, JSON)
- Handling missing values
- Data normalization basics

---

## 2. What You Will Learn

By the end of this lecture, you will be able to:

- Load structured data from external files (CSV, JSON)
- Identify and handle missing or inconsistent data
- Apply basic normalization techniques
- Explain why preprocessing is critical before ML

---

## 3. Let's Start With a Real Question

**Think about this before we begin:**

> "If your dataset has missing values, inconsistent formats, and noise — will your ML model still work?"

Here are three versions of the same problem, from simple to complex:

**Basic:**
- A dataset with just one missing value in a column

**Intermediate:**
- A dataset where gender is recorded as "Male", "M", and "male" — all meaning the same thing

**Advanced:**
- A dataset with missing values + inconsistent categories + outliers — all at the same time

---

> ### 🔥 Run This First — See the Problem Yourself
>
> Before any theory, run this code in Jupyter and look at the output carefully.
>
> ```python
> import pandas as pd
>
> # A real-world messy dataset — no file needed, just run it
> data = {
>     "name":   ["Ali", "Sara", "Ahmed", "Fatima", None],
>     "age":    [22, None, 19, 25, 21],
>     "gender": ["Male", "female", "M", "Female", "MALE"],
>     "score":  [85, 90, None, 78, 95]
> }
>
> df = pd.DataFrame(data)
> print(df)
> print("\nData types:\n", df.dtypes)
> print("\nMissing values:\n", df.isnull().sum())
> ```
>
> **Think about it:** Would you trust a model trained on this data? What specific problems do you notice?  
> We will fix all of these issues step by step throughout this lecture.

---

## 4. Reading Data from Files

### 4.1 Why File Handling Matters in AI

In real AI projects, data almost never comes pre-loaded. It comes from:
- CSV exports from hospital systems, school databases, or HR tools
- JSON responses from APIs (weather, e-commerce, social media)
- Excel files sent by clients or departments

Your first job as an AI engineer is to **get the data into Python reliably** — before any analysis or model training can happen.

### Example Levels

**Basic:**
- Small CSV file with 5–10 rows

```python
# Step 1: Create a small CSV file
import pandas as pd

sample_data = {
    "student_name": ["Ali", "Sara", "Ahmed", "Bilal", "Zainab"],
    "marks": [78, 92, 65, 85, 71]
}
df = pd.DataFrame(sample_data)
df.to_csv("students.csv", index=False)

# Step 2: Read it back
print("File created! Now reading it back:")
df_loaded = pd.read_csv("students.csv")
print(df_loaded)
```

> **Expected Output:**
> ```
>   student_name  marks
> 0          Ali     78
> 1         Sara     92
> 2        Ahmed     65
> 3        Bilal     85
> 4       Zainab     71
> ```

**Intermediate:**
- CSV with multiple columns (numeric + categorical)

```python
import pandas as pd

# A richer employee dataset
data = {
    "name":       ["Ali", "Sara", "Ahmed", "Bilal", "Zainab", "Hassan"],
    "age":        [22, 25, 19, 30, 28, 21],
    "city":       ["Islamabad", "Lahore", "Karachi", "Peshawar", "Islamabad", "Quetta"],
    "salary":     [45000, 70000, 38000, 90000, 65000, 42000],
    "department": ["IT", "HR", "IT", "Finance", "IT", "HR"]
}
df = pd.DataFrame(data)
df.to_csv("employees.csv", index=False)

# Load only the columns you actually need
df_subset = pd.read_csv("employees.csv", usecols=["name", "age", "salary"])
print(df_subset)
print("\nShape:", df_subset.shape)
print("\nData types:\n", df_subset.dtypes)
```

> **Why use `usecols`?** In production datasets with 50+ columns, loading everything wastes memory. Only load what you need — it's a good habit to build early.

**Advanced:**
- CSV with dirty values — using `na_values` to catch non-standard nulls

```python
import pandas as pd

# In many real exported files, missing values are written as "?" or "N/A" or "-"
# This is very common in legacy hospital systems, NADRA exports, and HR tools
dirty_data = """name,age,salary,city
Ali,22,45000,Islamabad
Sara,?,70000,Lahore
Ahmed,19,N/A,Karachi
Bilal,-,90000,-
Zainab,28,65000,Islamabad
"""

with open("dirty_employees.csv", "w") as f:
    f.write(dirty_data)

# Without na_values — "?" and "N/A" are treated as regular strings, not NaN
df_bad = pd.read_csv("dirty_employees.csv")
print("Without na_values fix:")
print(df_bad)
print("\nMissing values detected:", df_bad.isnull().sum().to_dict())

# With na_values — Python now correctly identifies them as missing
df_good = pd.read_csv("dirty_employees.csv", na_values=["?", "N/A", "-"])
print("\nWith na_values fix:")
print(df_good)
print("\nMissing values detected:", df_good.isnull().sum().to_dict())
```

> **Key Insight:** If you skip `na_values`, then `df.isnull()` will not catch those rows — a silent bug that corrupts your entire analysis without throwing any error.

---

### 4.2 Reading CSV Files (Pandas)

```python
import pandas as pd

df = pd.read_csv("data.csv")
print(df.head())
```

### Example Levels

**Basic:**
```python
pd.read_csv("students.csv")
```

**Intermediate:**
```python
pd.read_csv("data.csv", usecols=["age", "salary"])
```

**Advanced:**
```python
pd.read_csv("data.csv", na_values=["?", "NA"])
```

---

### 4.3 Reading JSON Files

```python
df = pd.read_json("data.json")
```

### Example Levels

**Basic:**
- Flat JSON file with simple key-value pairs

```python
import json
import pandas as pd

# Create a flat JSON file
students = [
    {"name": "Ali",    "marks": 78},
    {"name": "Sara",   "marks": 92},
    {"name": "Ahmed",  "marks": 65}
]

with open("students.json", "w") as f:
    json.dump(students, f)

# Read it back
df = pd.read_json("students.json")
print(df)
```

> **Expected Output:**
> ```
>     name  marks
> 0    Ali     78
> 1   Sara     92
> 2  Ahmed     65
> ```

**Intermediate:**
- JSON with list of records (typical REST API response)

```python
import json
import pandas as pd

# This is what a real API response looks like
api_response = {
    "status": "success",
    "total": 3,
    "records": [
        {"id": 1, "name": "Ali",   "city": "Islamabad", "score": 88},
        {"id": 2, "name": "Sara",  "city": "Lahore",    "score": 91},
        {"id": 3, "name": "Ahmed", "city": "Karachi",   "score": 74}
    ]
}

# You cannot read the whole response directly — you need to extract the records list
df = pd.DataFrame(api_response["records"])
print(df)
```

> **Why extract `["records"]`?** APIs wrap actual data inside metadata fields like `status` and `total`. You need to navigate to the data list first, then convert it to a DataFrame.

**Advanced:**
- Nested JSON — flatten with `json_normalize`

```python
import json
import pandas as pd
from pandas import json_normalize

# Each student has a nested "address" object inside the JSON
nested_data = [
    {"name": "Ali",   "score": 88, "address": {"city": "Islamabad", "area": "F-10"}},
    {"name": "Sara",  "score": 91, "address": {"city": "Lahore",    "area": "DHA"}},
    {"name": "Ahmed", "score": 74, "address": {"city": "Karachi",   "area": "Clifton"}}
]

# Without normalization — the address column stays as a dict (unusable for ML)
df_raw = pd.DataFrame(nested_data)
print("Before normalization:")
print(df_raw)
print("\nType of address column:", type(df_raw["address"][0]))

# With json_normalize — nested keys become dot-notation columns
df_flat = json_normalize(nested_data)
print("\nAfter normalization:")
print(df_flat)
```

> **Output after normalization:**
> ```
>     name  score address.city address.area
> 0    Ali     88   Islamabad         F-10
> 1   Sara     91      Lahore          DHA
> 2  Ahmed     74     Karachi      Clifton
> ```
>
> **Key Insight:** ML models need flat, tabular data. Nested JSON must always be flattened first. `json_normalize` does this in one line.

---

## 5. Missing Values

### 5.1 What Are Missing Values?

Missing values occur when a data entry is absent, skipped, or undefined. In Python/Pandas they appear as `NaN` (Not a Number).

**Why do they happen in real life?**
- A survey respondent skipped a question
- A sensor stopped recording for a few minutes
- A database column was added later, so older rows have nothing in it
- A data export bug from a legacy system

### Example Levels

**Basic:**
- Empty cell in a single column

```python
import pandas as pd

# None in a list becomes NaN inside a DataFrame
data = {"name": ["Ali", "Sara", "Ahmed"],
        "age":  [22, None, 19]}

df = pd.DataFrame(data)
print(df)
print("\nData types:\n", df.dtypes)
```

> **Notice:** The `age` column becomes `float64` even though ages are whole numbers. This happens because `NaN` is a float concept in Python — a column cannot be `int` if it contains any `NaN`. This is expected behavior, not a bug.

**Intermediate:**
- Multiple missing entries across several columns

```python
import pandas as pd
import numpy as np

data = {
    "name":   ["Ali", "Sara", "Ahmed", "Bilal", "Zainab"],
    "age":    [22, np.nan, 19, np.nan, 28],
    "salary": [45000, 70000, np.nan, 90000, np.nan],
    "city":   ["Islamabad", np.nan, "Karachi", "Peshawar", np.nan]
}

df = pd.DataFrame(data)
print(df)

# isnull() returns True/False for every cell
print("\nWhich cells are missing?")
print(df.isnull())
```

**Advanced:**
- Identify which columns are worst — visualize the missing percentage

```python
import pandas as pd
import numpy as np

data = {
    "name":       ["Ali", "Sara", "Ahmed", "Bilal", "Zainab", "Hassan", "Ayesha", "Usman", "Hira", "Kamran"],
    "age":        [22, np.nan, 19, np.nan, 28, 31, np.nan, 24, 26, np.nan],
    "salary":     [45000, 70000, np.nan, 90000, np.nan, np.nan, 55000, np.nan, 67000, 48000],
    "city":       ["Islamabad", np.nan, "Karachi", "Peshawar", np.nan, "Lahore", np.nan, "Islamabad", np.nan, "Quetta"],
    "department": ["IT", "HR", "IT", np.nan, "IT", np.nan, "Finance", "IT", np.nan, "HR"]
}

df = pd.DataFrame(data)

# The most useful diagnostic: missing percentage per column
missing_pct = df.isnull().mean() * 100
print("Missing percentage per column:")
print(missing_pct.round(1).astype(str) + "%")

# Flag columns that are too empty to be useful
critical_cols = missing_pct[missing_pct > 30].index.tolist()
print(f"\nColumns with >30% missing: {critical_cols}")
print("Recommendation: Consider dropping these columns entirely")
```

---

### 5.2 Detecting Missing Values

```python
df.isnull().sum()
```

### Example Levels

**Basic:**
```python
df.isnull()
```

**Intermediate:**
```python
df.isnull().sum()
```

**Advanced:**
```python
df.isnull().mean() * 100
```

---

### 5.3 Handling Missing Values

#### Option 1: Remove Rows

```python
df.dropna()
```

#### Option 2: Fill Values

```python
df.fillna(df.mean())
```

### Example Levels

**Basic:**
```python
df.dropna()
```

**Intermediate:**
```python
df.fillna(df["age"].mean())
```

**Advanced:**
```python
df.fillna({"age": df["age"].median(), "city": "Unknown"})
```

---

### 5.4 Discussion: When Do You Drop vs Fill?

**Scenario — think through this:**

> You have a dataset of 500 student records. The `cgpa` column has 12 missing values. The `phone_number` column has 210 missing values. What do you do with each?

### Example Levels

**Basic:**
- Drop rows with just 1–2 missing values

```python
import pandas as pd
import numpy as np

data = {
    "name":  ["Ali", "Sara", "Ahmed", "Bilal", "Zainab"],
    "cgpa":  [3.5, np.nan, 2.9, 3.8, 3.1],
    "marks": [85, 90, 78, 92, 88]
}
df = pd.DataFrame(data)

print("Before:", df.shape)
df_clean = df.dropna()   # removes any row that has at least one missing value
print("After dropna():", df_clean.shape)
print(df_clean)
```

> **Caution:** `dropna()` removes the entire row. If you have 500 rows and only 2 are missing, this is fine. But if 100 rows are missing, you are throwing away 20% of your data — and your model suffers.

**Intermediate:**
- Fill numeric columns with mean, drop rows with missing categorical values

```python
import pandas as pd
import numpy as np

data = {
    "name":   ["Ali", "Sara", "Ahmed", "Bilal", "Zainab"],
    "age":    [22, np.nan, 19, np.nan, 28],
    "salary": [45000, 70000, np.nan, 90000, 65000],
    "city":   ["Islamabad", np.nan, "Karachi", "Peshawar", "Islamabad"]
}
df = pd.DataFrame(data)
print("Original:\n", df)

# Fill numeric columns with their column mean
df["age"]    = df["age"].fillna(df["age"].mean())
df["salary"] = df["salary"].fillna(df["salary"].mean())

# Drop rows where a categorical column is missing — we cannot guess a city
df = df.dropna(subset=["city"])

print("\nCleaned:\n", df)
```

> **The rule of thumb:** For numbers, filling with mean or median is generally safe. For categories like city, gender, or department — guessing is risky. Either drop those rows or fill with "Unknown" and treat it as a separate category.

**Advanced:**
- Programmatically drop columns above a missing threshold, then fill the rest

```python
import pandas as pd
import numpy as np

data = {
    "name":         ["Ali", "Sara", "Ahmed", "Bilal", "Zainab", "Hassan", "Ayesha", "Usman", "Hira", "Kamran"],
    "age":          [22, np.nan, 19, np.nan, 28, 31, np.nan, 24, 26, np.nan],
    "salary":       [45000, 70000, np.nan, 90000, np.nan, np.nan, 55000, np.nan, 67000, 48000],
    "phone_number": [np.nan, np.nan, np.nan, np.nan, np.nan, "0300-1234567", np.nan, np.nan, np.nan, np.nan]
}

df = pd.DataFrame(data)
print("Missing % before:\n", (df.isnull().mean() * 100).round(1))

DROP_THRESHOLD = 40  # drop any column with more than 40% missing values

cols_to_drop = [col for col in df.columns if df[col].isnull().mean() * 100 > DROP_THRESHOLD]
print(f"\nDropping columns (>{DROP_THRESHOLD}% missing): {cols_to_drop}")
df = df.drop(columns=cols_to_drop)

# Fill remaining numeric columns with median
numeric_cols = df.select_dtypes(include="number").columns
df[numeric_cols] = df[numeric_cols].fillna(df[numeric_cols].median())

print("\nFinal cleaned dataframe:\n", df)
print("\nMissing values remaining:", df.isnull().sum().sum())
```

> **Why median instead of mean for salary?** Salary data often has outliers — one person earning 5x everyone else pulls the mean up significantly. The median is more resistant to that. This is a real-world best practice used in production systems.

---

## 6. Data Normalization

### 6.1 Why Normalization?

Without normalization, features with large numeric ranges dominate the model and features with small ranges get ignored — even if the small-range features are actually the more important ones.

### Example Levels

**Basic:**
- See the scale difference between age and salary directly

```python
import pandas as pd

data = {
    "name":   ["Ali", "Sara", "Ahmed", "Bilal", "Zainab"],
    "age":    [22, 25, 19, 30, 28],
    "salary": [45000, 70000, 38000, 90000, 65000]
}
df = pd.DataFrame(data)

print("Raw data:")
print(df[["age", "salary"]])

print("\nMin values:  ", df[["age", "salary"]].min().to_dict())
print("Max values:  ", df[["age", "salary"]].max().to_dict())
print("Range:       ", (df[["age", "salary"]].max() - df[["age", "salary"]].min()).to_dict())
```

> **Think about it:** If we calculate the distance between two people using age and salary, which feature dominates — and why is that a problem?

**Intermediate:**
- See how large-scale features dominate distance calculations

```python
import pandas as pd
import numpy as np

data = {
    "age":        [22, 25, 19, 30, 28],
    "salary":     [45000, 70000, 38000, 90000, 65000],
    "experience": [1, 3, 0, 7, 5]   # in years
}
df = pd.DataFrame(data)

# Distance between Person 0 (Ali) and Person 1 (Sara)
p0 = df.iloc[0]
p1 = df.iloc[1]

distance_raw = np.sqrt(sum((p0 - p1) ** 2))
print(f"Raw distance between Person 0 and Person 1: {distance_raw:.2f}")
print("Notice: the salary difference dominates entirely because the numbers are huge!")

# Now normalize and recalculate
df_norm = (df - df.min()) / (df.max() - df.min())
p0_norm = df_norm.iloc[0]
p1_norm = df_norm.iloc[1]

distance_norm = np.sqrt(sum((p0_norm - p1_norm) ** 2))
print(f"\nNormalized distance: {distance_norm:.4f}")
print("Now all three features contribute fairly to the distance.")
```

**Advanced:**
- Prove it with actual model accuracy: KNN with and without normalization

```python
import pandas as pd
import numpy as np
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# Synthetic dataset: age (small scale) + salary (large scale) -> hired (1/0)
np.random.seed(42)
n = 100
age    = np.random.randint(22, 45, n)
salary = np.random.randint(30000, 100000, n)
hired  = ((age > 30) & (salary > 60000)).astype(int)

df = pd.DataFrame({"age": age, "salary": salary, "hired": hired})
X = df[["age", "salary"]]
y = df["hired"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# KNN WITHOUT normalization
knn = KNeighborsClassifier(n_neighbors=3)
knn.fit(X_train, y_train)
acc_raw = accuracy_score(y_test, knn.predict(X_test))

# KNN WITH normalization
X_norm = (X - X.min()) / (X.max() - X.min())
X_train_n, X_test_n, y_train_n, y_test_n = train_test_split(X_norm, y, test_size=0.2, random_state=42)
knn2 = KNeighborsClassifier(n_neighbors=3)
knn2.fit(X_train_n, y_train_n)
acc_norm = accuracy_score(y_test_n, knn2.predict(X_test_n))

print(f"KNN Accuracy WITHOUT normalization: {acc_raw:.2%}")
print(f"KNN Accuracy WITH normalization:    {acc_norm:.2%}")
print("\nNormalization improved accuracy because KNN relies entirely on distance calculations.")
```

> **This is the most important demo in this section.** Normalization is not just theory — it has a measurable impact on model accuracy. Run this code and see the difference yourself.

---

### 6.2 Min-Max Normalization

```python
(df - df.min()) / (df.max() - df.min())
```

### Example Levels

**Basic:**
```python
import pandas as pd

data = {"age": [22, 25, 19, 30, 28]}
df = pd.DataFrame(data)

df["age_normalized"] = (df["age"] - df["age"].min()) / (df["age"].max() - df["age"].min())
print(df)
# The minimum age becomes 0.0, the maximum becomes 1.0, everything else scales in between
```

**Intermediate:**
```python
import pandas as pd

data = {
    "age":    [22, 25, 19, 30, 28],
    "salary": [45000, 70000, 38000, 90000, 65000]
}
df = pd.DataFrame(data)

print("Before normalization:")
print(df)

df_norm = (df - df.min()) / (df.max() - df.min())
print("\nAfter Min-Max normalization:")
print(df_norm.round(4))
```

**Advanced:**
- Apply normalization safely on a DataFrame that has both numbers and strings

```python
import pandas as pd

data = {
    "name":   ["Ali", "Sara", "Ahmed", "Bilal", "Zainab"],
    "age":    [22, 25, 19, 30, 28],
    "salary": [45000, 70000, 38000, 90000, 65000],
    "city":   ["Islamabad", "Lahore", "Karachi", "Peshawar", "Islamabad"]
}
df = pd.DataFrame(data)

print("Original:\n", df)

# Select only numeric columns before normalizing — never apply math to string columns
numeric_cols = df.select_dtypes(include="number").columns
print(f"\nNumeric columns found: {list(numeric_cols)}")

df[numeric_cols] = (df[numeric_cols] - df[numeric_cols].min()) / \
                   (df[numeric_cols].max() - df[numeric_cols].min())

print("\nAfter normalization (string columns untouched):\n", df)
```

> **Common mistake to avoid:** Running `(df - df.min()) / (df.max() - df.min())` on a DataFrame that contains string columns will throw a `TypeError`. Always filter to numeric columns first using `select_dtypes(include="number")`.

---

### 6.3 Standardization (Concept Only)

### Example Levels

**Basic:**
- Understand what mean centering means

```python
import pandas as pd

data = {"salary": [45000, 70000, 38000, 90000, 65000]}
df = pd.DataFrame(data)

mean = df["salary"].mean()
std  = df["salary"].std()

print(f"Mean salary:   {mean:.0f}")
print(f"Std deviation: {std:.0f}")
print("\nFormula: standardized = (value - mean) / std")
print("Result: values cluster around 0, with most falling between -2 and +2")

df["salary_standardized"] = (df["salary"] - mean) / std
print("\n", df.round(3))
```

**Intermediate:**
- Compare the distribution before and after standardization

```python
import pandas as pd
import numpy as np

np.random.seed(42)
salaries = np.random.normal(loc=60000, scale=15000, size=20).astype(int)
df = pd.DataFrame({"salary": salaries})

df["standardized"] = (df["salary"] - df["salary"].mean()) / df["salary"].std()

print("Before standardization:")
print(f"  Mean: {df['salary'].mean():.0f}  |  Std: {df['salary'].std():.0f}  |  Min: {df['salary'].min()}  |  Max: {df['salary'].max()}")

print("\nAfter standardization:")
print(f"  Mean: {df['standardized'].mean():.4f}  |  Std: {df['standardized'].std():.4f}  |  Min: {df['standardized'].min():.2f}  |  Max: {df['standardized'].max():.2f}")
print("\nThe shape of the data is preserved. Only the scale changes.")
```

**Advanced:**
```python
from sklearn.preprocessing import StandardScaler
import pandas as pd

data = {
    "age":    [22, 25, 19, 30, 28],
    "salary": [45000, 70000, 38000, 90000, 65000]
}
df = pd.DataFrame(data)

scaler = StandardScaler()
df_scaled = pd.DataFrame(
    scaler.fit_transform(df),
    columns=df.columns
)

print("Standardized with sklearn:")
print(df_scaled.round(3))
```

> **Min-Max vs Standardization — When to use which?**
> | Situation | Recommended |
> |---|---|
> | Neural networks, image pixel values, bounded output needed | Min-Max (scales to 0–1) |
> | Linear regression, logistic regression, SVM, PCA | Standardization (mean=0, std=1) |
> | Data contains heavy outliers | Standardization (less sensitive to extremes) |
> | You need values confined to a fixed range | Min-Max |

---

## 7. Integrated Example (Mini Pipeline)

```python
import pandas as pd

df = pd.read_csv("data.csv")
df = df.fillna(df.mean())
df = (df - df.min()) / (df.max() - df.min())
```

### Example Levels

**Basic:**
- Apply the full pipeline on a small dataset step by step

```python
import pandas as pd
import numpy as np

# Small dataset — no file needed
data = {
    "age":    [22, np.nan, 19, 30, 28],
    "salary": [45000, 70000, np.nan, 90000, 65000]
}
df = pd.DataFrame(data)
print("Step 0 — Raw data:\n", df)

# Step 1: Fill missing values with column mean
df = df.fillna(df.mean())
print("\nStep 1 — After fillna:\n", df)

# Step 2: Normalize everything to 0–1
df = (df - df.min()) / (df.max() - df.min())
print("\nStep 2 — After normalization:\n", df.round(4))
```

**Intermediate:**
- Apply the pipeline on a dataset with both strings and numbers

```python
import pandas as pd
import numpy as np

data = {
    "name":   ["Ali", "Sara", "Ahmed", "Bilal", "Zainab"],
    "age":    [22, np.nan, 19, 30, 28],
    "salary": [45000, 70000, np.nan, 90000, 65000],
    "city":   ["Islamabad", np.nan, "Karachi", "Peshawar", "Islamabad"]
}
df = pd.DataFrame(data)
print("Step 0 — Raw data:\n", df)

# Step 1: Handle missing values differently depending on column type
numeric_cols     = df.select_dtypes(include="number").columns
categorical_cols = df.select_dtypes(include="object").columns

df[numeric_cols]     = df[numeric_cols].fillna(df[numeric_cols].mean())
df[categorical_cols] = df[categorical_cols].fillna("Unknown")
print("\nStep 1 — After filling:\n", df)

# Step 2: Normalize only the numeric columns
df[numeric_cols] = (df[numeric_cols] - df[numeric_cols].min()) / \
                   (df[numeric_cols].max() - df[numeric_cols].min())
print("\nStep 2 — After normalization:\n", df.round(4))
```

**Advanced:**
- Build a reusable preprocessing function

```python
import pandas as pd
import numpy as np

def preprocess(df, drop_threshold=0.4):
    """
    A reusable preprocessing pipeline.

    Steps:
      1. Drop columns with too many missing values
      2. Fill numeric columns with median
      3. Fill categorical columns with 'Unknown'
      4. Normalize numeric columns using Min-Max

    Args:
        df (pd.DataFrame): Raw input data
        drop_threshold (float): Drop column if missing % exceeds this. Default: 40%

    Returns:
        pd.DataFrame: Cleaned and normalized DataFrame
    """
    df = df.copy()  # never modify the original dataframe

    # Step 1: Drop high-missing columns
    missing_pct  = df.isnull().mean()
    cols_to_drop = missing_pct[missing_pct > drop_threshold].index.tolist()
    if cols_to_drop:
        print(f"[preprocess] Dropping columns (>{drop_threshold*100:.0f}% missing): {cols_to_drop}")
    df = df.drop(columns=cols_to_drop)

    # Step 2 & 3: Fill missing values based on column type
    numeric_cols     = df.select_dtypes(include="number").columns
    categorical_cols = df.select_dtypes(include="object").columns

    df[numeric_cols]     = df[numeric_cols].fillna(df[numeric_cols].median())
    df[categorical_cols] = df[categorical_cols].fillna("Unknown")

    # Step 4: Min-Max normalize numeric columns
    df[numeric_cols] = (df[numeric_cols] - df[numeric_cols].min()) / \
                       (df[numeric_cols].max() - df[numeric_cols].min())

    print(f"[preprocess] Done. Shape: {df.shape} | Missing remaining: {df.isnull().sum().sum()}")
    return df


# ---- Test the pipeline ----
data = {
    "name":         ["Ali", "Sara", "Ahmed", "Bilal", "Zainab", "Hassan"],
    "age":          [22, np.nan, 19, 30, 28, np.nan],
    "salary":       [45000, 70000, np.nan, 90000, 65000, 50000],
    "phone_number": [np.nan, np.nan, np.nan, np.nan, np.nan, "0300-1234567"],  # >80% missing
    "city":         ["Islamabad", np.nan, "Karachi", "Peshawar", "Islamabad", "Lahore"]
}
df_raw = pd.DataFrame(data)

print("Raw input:\n", df_raw, "\n")
df_clean = preprocess(df_raw)
print("\nOutput:\n", df_clean.round(4))
```

> **Why write preprocessing as a function?** In real projects you apply the same preprocessing to both your training data and any new incoming data. If your steps are scattered across 10 notebook cells, you will inevitably miss one when processing new data — and your model will receive inconsistent input. A function enforces consistency every time.

---

## 8. Common Mistakes to Avoid

### Example Levels

**Basic:**
- Forgetting to handle missing values before passing data to a model

```python
import pandas as pd
import numpy as np
from sklearn.linear_model import LinearRegression

data = {
    "age":    [22, np.nan, 19, 30, 28],
    "salary": [45000, 70000, 38000, 90000, 65000]
}
df = pd.DataFrame(data)

X = df[["age"]]
y = df["salary"]

model = LinearRegression()

# ❌ WRONG — this will crash with a ValueError because of NaN
try:
    model.fit(X, y)
    print("Trained successfully (this should NOT print)")
except ValueError as e:
    print(f"❌ Error: {e}")

# ✅ CORRECT — fill missing values first, then train
X_clean = X.fillna(X.mean())
model.fit(X_clean, y)
print("✅ Model trained successfully after handling missing values")
```

**Intermediate:**
- Normalizing the target column `y` by mistake

```python
import pandas as pd
import numpy as np

data = {
    "age":    [22, 25, 19, 30, 28],
    "salary": [45000, 70000, 38000, 90000, 65000]
}
df = pd.DataFrame(data)

# ❌ WRONG — this normalizes ALL columns including salary (your target)
df_wrong = (df - df.min()) / (df.max() - df.min())
print("❌ Wrong — target column 'salary' was also normalized:")
print(df_wrong)
print("Your model now predicts values between 0 and 1, not actual salaries!")

# ✅ CORRECT — normalize only the input features, never the target
features = ["age"]   # only the columns you feed into the model
df_correct = df.copy()
df_correct[features] = (df[features] - df[features].min()) / \
                        (df[features].max() - df[features].min())
print("\n✅ Correct — only input features normalized, salary preserved:")
print(df_correct)
```

**Advanced:**
- Data leakage: normalizing before the train/test split

```python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split

np.random.seed(42)
data = {
    "age":    np.random.randint(18, 60, 20),
    "salary": np.random.randint(30000, 120000, 20)
}
df = pd.DataFrame(data)
y  = np.random.randint(0, 2, 20)

# ❌ WRONG — normalizing before the split means the min/max was computed using test rows too
df_leaked = (df - df.min()) / (df.max() - df.min())
X_train_bad, X_test_bad = train_test_split(df_leaked, test_size=0.2, random_state=42)
print("❌ Data leakage: normalization used min/max from the ENTIRE dataset.")
print("   The model has indirectly 'seen' test data during training.")

# ✅ CORRECT — split first, then normalize using only training data statistics
X_train, X_test = train_test_split(df, test_size=0.2, random_state=42)

train_min = X_train.min()
train_max = X_train.max()

X_train_norm = (X_train - train_min) / (train_max - train_min)
X_test_norm  = (X_test  - train_min) / (train_max - train_min)  # apply TRAIN stats to test

print("\n✅ Correct: split first, normalize using only training statistics.")
print("   The test set is normalized with the same scale as training — no leakage.")
```

> **Data leakage is one of the most common and damaging bugs in ML.** It makes your model look better during development than it actually performs in production. The rule is simple: always split first, then normalize.

---

## 9. Wrap-Up Discussion

**Consider this scenario and think through your answer:**

> You receive a CSV with 1,000 rows of job applicant data: name, age, CGPA, city, experience, and a "hired" column. Before feeding it to a model, what steps do you take?

### Example Levels

**Basic:**
- Start with a health check on any new dataset

```python
import pandas as pd
import numpy as np

# Run these four things immediately on any new dataset you receive
def dataset_health_check(df):
    print(f"Shape:          {df.shape}")
    print(f"Missing values:\n{df.isnull().sum()}")
    print(f"\nData types:\n{df.dtypes}")
    print(f"\nFirst 5 rows:\n{df.head()}")

# Try it
data = {
    "name": ["Ali", "Sara", None], "age": [22, None, 19],
    "cgpa": [3.5, 3.8, 2.9], "hired": [1, 0, 1]
}
dataset_health_check(pd.DataFrame(data))
```

**Intermediate:**
- Decide a strategy for each column before writing any code

```python
# Think through each column before touching the data
strategy = {
    "name":       "Drop — it is not a feature, it adds no predictive value",
    "age":        "Fill with median (numeric, may have outliers)",
    "cgpa":       "Fill with mean (bounded 0–4, likely normal distribution)",
    "city":       "Fill with 'Unknown' (categorical — cannot guess a city)",
    "experience": "Fill with 0 (a fresh graduate has zero experience — logical default)",
    "hired":      "Do NOT touch — this is your target column (y)"
}

for col, decision in strategy.items():
    print(f"  {col:12} → {decision}")
```

**Advanced:**
- Put it all together in a complete, correct pipeline

```python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split

def build_pipeline(df, target_col):
    """Full preprocessing pipeline: handles missing values, normalizes, splits correctly."""

    df = df.copy()

    # 1. Separate features and target BEFORE any processing
    y = df[target_col]
    X = df.drop(columns=[target_col])

    # 2. Drop non-feature columns (names, IDs — no predictive value)
    X = X.drop(columns=["name"], errors="ignore")

    # 3. Train/test split BEFORE normalization (critical — prevents data leakage)
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

    # 4. Handle missing values using TRAINING set statistics only
    num_cols = X_train.select_dtypes(include="number").columns
    cat_cols = X_train.select_dtypes(include="object").columns

    train_medians = X_train[num_cols].median()
    X_train[num_cols] = X_train[num_cols].fillna(train_medians)
    X_test[num_cols]  = X_test[num_cols].fillna(train_medians)  # use same stats as training!

    X_train[cat_cols] = X_train[cat_cols].fillna("Unknown")
    X_test[cat_cols]  = X_test[cat_cols].fillna("Unknown")

    # 5. Normalize using TRAINING set min/max only
    train_min = X_train[num_cols].min()
    train_max = X_train[num_cols].max()

    X_train[num_cols] = (X_train[num_cols] - train_min) / (train_max - train_min)
    X_test[num_cols]  = (X_test[num_cols]  - train_min) / (train_max - train_min)

    print("Pipeline complete.")
    print(f"X_train: {X_train.shape} | X_test: {X_test.shape}")
    return X_train, X_test, y_train, y_test


# Test it
data = {
    "name": ["Ali","Sara","Ahmed","Bilal","Zainab","Hassan","Ayesha","Usman","Hira","Kamran"],
    "age":  [22, np.nan, 19, 30, 28, 31, np.nan, 24, 26, np.nan],
    "cgpa": [3.5, 3.8, 2.9, 3.2, 3.6, 3.0, 3.9, np.nan, 3.3, 3.7],
    "hired":[1, 1, 0, 1, 1, 0, 1, 0, 1, 1]
}
df = pd.DataFrame(data)
X_train, X_test, y_train, y_test = build_pipeline(df, target_col="hired")
print("\nX_train sample:\n", X_train.round(3))
```

---

## 10. Key Takeaways

1. Real-world data is messy — expect it, plan for it
2. Load data from files using `pd.read_csv()` and `pd.read_json()`
3. Always detect and handle missing values before any analysis or training
4. Normalize your input features before training ML models
5. Think in pipelines — not in scattered one-off steps

---

## 11. Bonus: sklearn Preprocessing (If Time Allows)

### Example Levels

**Basic:**
- Use `MinMaxScaler` from sklearn

```python
from sklearn.preprocessing import MinMaxScaler
import pandas as pd

data = {"age": [22, 25, 19, 30, 28], "salary": [45000, 70000, 38000, 90000, 65000]}
df = pd.DataFrame(data)

scaler = MinMaxScaler()
df_scaled = pd.DataFrame(scaler.fit_transform(df), columns=df.columns)
print(df_scaled.round(4))
```

**Intermediate:**
- Use `StandardScaler` and verify the output

```python
from sklearn.preprocessing import StandardScaler
import pandas as pd

data = {"age": [22, 25, 19, 30, 28], "salary": [45000, 70000, 38000, 90000, 65000]}
df = pd.DataFrame(data)

scaler = StandardScaler()
df_scaled = pd.DataFrame(scaler.fit_transform(df), columns=df.columns)
print("StandardScaler output:")
print(df_scaled.round(4))
print(f"\nMean (should be ~0): {df_scaled.mean().round(4).to_dict()}")
print(f"Std  (should be ~1): {df_scaled.std().round(4).to_dict()}")
```

**Advanced:**
- Compare `MinMaxScaler` vs `StandardScaler` on a dataset with an outlier

```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import MinMaxScaler, StandardScaler

# Age = 200 is a clear data entry error (outlier)
data = {
    "age":    [22, 25, 19, 30, 28, 200],
    "salary": [45000, 70000, 38000, 90000, 65000, 68000]
}
df = pd.DataFrame(data)
print("Raw data (note the outlier: age=200):")
print(df)

mm_scaler  = MinMaxScaler()
std_scaler = StandardScaler()

df_minmax = pd.DataFrame(mm_scaler.fit_transform(df),  columns=df.columns)
df_std    = pd.DataFrame(std_scaler.fit_transform(df), columns=df.columns)

print("\nMin-Max Scaled (sensitive to outliers):")
print(df_minmax.round(4))
print("Notice: all normal age values are compressed near 0 because of the single outlier!")

print("\nStandardized (more robust to outliers):")
print(df_std.round(4))
print("Notice: normal values still have a reasonable spread. Outlier gets a large z-score.")

print("""
Summary:
  MinMaxScaler   → Scales to [0,1], fast and intuitive, but one outlier can collapse everything
  StandardScaler → More robust, unbounded output, better choice when outliers are present
""")
```

---

## 12. How This Fits Into the Course

This lecture bridges raw data collection and the modeling phase. After this week, you have the tools to take any messy real-world dataset and prepare it for a machine learning model — which is what the rest of the course builds on.

---

> ### 🏠 Take-Home Practice (Optional but Recommended)
>
> Download any small CSV from [Kaggle](https://www.kaggle.com/datasets) — the Titanic dataset or a student performance dataset work well. Then apply the full pipeline on your own:
> 1. Load it with `pd.read_csv()`
> 2. Run a health check (`shape`, `isnull().sum()`, `dtypes`)
> 3. Handle missing values — justify your strategy for each column
> 4. Normalize the numeric features
> 5. Package everything into a reusable `preprocess()` function
>
> Bring your Jupyter notebook to next week's session.

---

End of Lecture Document
