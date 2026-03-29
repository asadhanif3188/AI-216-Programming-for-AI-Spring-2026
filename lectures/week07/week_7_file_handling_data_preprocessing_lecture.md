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

### Teaching Intent
- Emphasize the reality of dirty, inconsistent, real-world data
- Prepare students for machine learning readiness

---

## 2. Learning Outcomes (Aligned with CLOs)

By the end of this lecture, students should be able to:

- Load structured data from external files (CSV, JSON)
- Identify and handle missing or inconsistent data
- Apply basic normalization techniques
- Explain why preprocessing is critical before ML

---

## 3. Lecture Opening (Hook)

Start with a Question:

"If your dataset has missing values, inconsistent formats, and noise, will your ML model still work?"

### Example Levels

**Basic:**
- Dataset with one missing value in a column

**Intermediate:**
- Dataset with mixed gender labels ("Male", "M", "male")

**Advanced:**
- Dataset with missing values + inconsistent categories + outliers

---

## 4. Reading Data from Files

### 4.1 Why File Handling Matters in AI

### Example Levels

**Basic:**
- Small CSV file with 5–10 rows

**Intermediate:**
- CSV with multiple columns (numeric + categorical)

**Advanced:**
- JSON dataset from API with nested structure

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

**Intermediate:**
- JSON with list of records

**Advanced:**
```python
from pandas import json_normalize
json_normalize(data)
```

---

## 5. Missing Values

### 5.1 What Are Missing Values?

### Example Levels

**Basic:**
- Empty cell in a column

**Intermediate:**
- Multiple missing entries across columns

**Advanced:**
- Missing data patterns (entire column partially empty)

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

### 5.4 Discussion Prompt

### Example Levels

**Basic:**
- Drop rows with 1–2 missing values

**Intermediate:**
- Fill numeric, drop categorical

**Advanced:**
- Decide threshold (e.g., drop column if >40% missing)

---

## 6. Data Normalization

### 6.1 Why Normalization?

### Example Levels

**Basic:**
- Age vs Salary comparison

**Intermediate:**
- Dataset with 3–4 numerical features

**Advanced:**
- Dataset affecting model performance (e.g., KNN distance bias)

---

### 6.2 Min-Max Normalization

```python
(df - df.min()) / (df.max() - df.min())
```

### Example Levels

**Basic:**
```python
(df["age"] - df["age"].min()) / (df["age"].max() - df["age"].min())
```

**Intermediate:**
```python
df_norm = (df - df.min()) / (df.max() - df.min())
```

**Advanced:**
- Apply normalization only to numeric columns using selection

---

### 6.3 Standardization (Concept Only)

### Example Levels

**Basic:**
- Understand mean centering

**Intermediate:**
- Compare before/after distribution

**Advanced:**
```python
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
scaler.fit_transform(df)
```

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
- Apply steps on small dataset

**Intermediate:**
- Apply on dataset with mixed types

**Advanced:**
- Build reusable preprocessing function

---

## 8. Common Student Mistakes

### Example Levels

**Basic:**
- Forgetting to handle missing values

**Intermediate:**
- Applying normalization incorrectly

**Advanced:**
- Data leakage (normalizing before train/test split)

---

## 9. Wrap-Up Discussion

### Example Levels

**Basic:**
- Identify clean vs dirty dataset

**Intermediate:**
- Choose preprocessing strategy

**Advanced:**
- Justify preprocessing pipeline decisions

---

## 10. Suggested Board or Slide Summary

1. Real-world data is messy
2. Load data from files (CSV, JSON)
3. Handle missing values carefully
4. Normalize before ML
5. Think in pipelines

---

## 11. Optional Extension (If Time Allows)

### Example Levels

**Basic:**
- Introduce sklearn preprocessing

**Intermediate:**
- Apply StandardScaler

**Advanced:**
- Compare MinMaxScaler vs StandardScaler

---

## 12. Alignment with Course Design

- Supports transition from data collection to exploratory data analysis
- Reinforces practical AI workflow development

---

End of Lecture Document

