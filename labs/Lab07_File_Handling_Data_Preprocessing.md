# AI-216 – Programming for Artificial Intelligence
## Week 7 Lab: File Handling & Data Preprocessing

---

## 1. Objective

This lab develops practical skills in preparing real-world datasets for machine learning by:

- Loading data from CSV and JSON files
- Identifying and handling missing values
- Cleaning inconsistent categorical data
- Applying normalization techniques
- Building a structured preprocessing workflow

This lab reinforces the transition from raw data to ML-ready datasets.

---

## 2. Background

In real AI workflows, data is rarely clean. Before any model training, datasets must be:

- Loaded correctly
- Cleaned (missing + inconsistent values)
- Transformed into a usable numeric format

This lab simulates a **real hiring dataset scenario** — you are a junior data engineer at a recruitment company. A hiring manager wants to build a model to predict which applicants are likely to succeed. Your job is to take the raw data handed to you and make it model-ready.

The catch: nobody told you how messy the data is. You have to find the problems yourself, decide how to fix each one, and be able to justify every decision you make.

> **Remember from the lecture:** There is no single "correct" way to handle every preprocessing problem. What matters is that your decision is logical, consistent, and documented.

---

## 3. Tools & Libraries

- Python 3.x
- Pandas
- NumPy
- GitHub (for submission)

---

## 4. Dataset Description

You are given two data sources. **Read both carefully before writing any code.**

### Dataset 1: applicants.csv

| id | name | age | experience | city | expected_salary |
|----|------|-----|------------|------|-----------------|
| 1  | Ali  | 22  | 1          | Islamabad | 40000 |
| 2  | Sara | NaN | 3          | Lahore    | 60000 |
| 3  | Ahmed| 19  | NaN        | Karachi   | ?     |
| 4  | Bilal| 30  | 7          | Peshawar  | 90000 |
| 5  | Hira | 28  | 5          | isl       | 65000 |
| 6  | None | 26  | 4          | Lahore    | 70000 |

### Dataset 2: applicants_extra.json

```json
[
  {"id": 1, "skills": ["python", "sql"], "education": "bachelors"},
  {"id": 2, "skills": ["excel", "communication"], "education": "masters"},
  {"id": 3, "skills": null, "education": "bachelors"},
  {"id": 4, "skills": ["management"], "education": "phd"},
  {"id": 5, "skills": ["python", "ml"], "education": null}
]
```

> ⚠️ **Notice Before You Start:**  
> Look at both datasets carefully. Without writing any code yet, count how many problems you can spot — missing values, inconsistent entries, non-standard nulls, columns that don't match between files. Write them down. You will revisit this list at the end of Task 1.

---

## 5. Tasks

> **Difficulty Guide:** 🟢 Basic &nbsp;|&nbsp; 🟡 Intermediate &nbsp;|&nbsp; 🔴 Advanced

---

### Task 1 — Load and Inspect Data 🟢

**Why this matters:** Before touching any data, your first job is always to understand what you actually have. Jumping into cleaning without inspection is one of the most common and costly mistakes in real projects.

**Steps:**
- Create both datasets as files on disk (CSV and JSON) using the data from Section 4
- Load both into separate DataFrames
- For each DataFrame, display:
  - First 5 rows (`.head()`)
  - Data types (`.dtypes`)
  - Missing value count per column (`.isnull().sum()`)
  - Shape (`.shape`)

**Expected Output Hint:** After loading `applicants.csv`, your missing value count should show at least 3 columns with issues. If you see fewer, re-check how you created the file.

> 🤔 **Reflect:** Compare what you found in code with the list you wrote before starting. Did Pandas catch every problem you spotted manually? Was there anything Pandas flagged that you missed — or anything you caught that Pandas did not? Why might that happen?

---

### Task 2 — Merge Datasets 🟢

**Why this matters:** Real data is almost never in one file. In production, you will regularly join multiple tables or API responses. Understanding what happens at the join is critical — a wrong merge can silently drop rows or duplicate them.

**Steps:**
- Merge `applicants.csv` and `applicants_extra.json` on the `id` column
- Display the merged DataFrame
- Verify the shape — does the row count match what you expected?

**Hint:** Use `pd.merge()`. Think about which type of join is appropriate here: `inner`, `left`, `right`, or `outer`?

**Expected Output Hint:** The merged DataFrame should have 6 rows and 8 columns. If you get more or fewer rows, your join type may be wrong.

> 🤔 **Reflect:** Notice that `applicants_extra.json` only has 5 records (ids 1–5), while `applicants.csv` has 6 (ids 1–6). What happens to Row 6 (id=6) depending on which join type you use? Which join type preserves all applicants, and which one drops the unmatched one? Which choice is correct for this scenario — and why?

---

### Task 3 — Handle Missing Values 🟡

**Why this matters:** How you fill missing values directly affects what your model learns. A wrong fill strategy can introduce bias or mask real patterns in the data.

**Steps:**

1. Fill missing `age` with the column **median**
2. Fill missing `experience` with `0` *(a reasonable assumption — if no experience was recorded, the applicant likely has none)*
3. The `expected_salary` column contains `"?"` for row 3. This is a non-standard null — Pandas will not detect it automatically.
   - First, replace `"?"` with `NaN`
   - Then fill the resulting `NaN` with the column **median**
4. Fill missing `education` with `"Unknown"`
5. For the `name` column: row 6 has no name. Decide how to handle it and document your reasoning.

**Constraint:** After completing this task, run `df.isnull().sum()` again. The total missing count across all columns should be 0 (or you should be able to explain why any remaining nulls are intentional).

> 🤔 **Reflect:**
> - Why did we use **median** for `age` and `salary` instead of **mean**? Under what condition would mean be a better choice?
> - Why did we fill missing `experience` with `0` instead of the median? Could this assumption ever be wrong?
> - Row 6 is missing a `name`. Is `name` a feature you would pass to a model? Does that change how you handle it?

---

### Task 4 — Clean Inconsistent Data 🟡

**Why this matters:** "isl", "Islamabad", and "islamabad" are three different strings to a machine learning model. Inconsistent labels create phantom categories that corrupt your model's understanding of the data.

**Steps:**

1. In the `city` column, replace the abbreviation `"isl"` with `"Islamabad"`
2. Check whether there are any other inconsistencies in the `city` column (look carefully — are all values truly consistent in spelling and casing after step 1?)
3. Convert all city names to **lowercase** for uniformity
4. Print the unique values of `city` after cleaning to confirm

**Expected Output Hint:** After cleaning, `df["city"].unique()` should return exactly 4 unique city names with no duplicates or near-duplicates.

> 🤔 **Reflect:**
> - Why is it better to standardize to lowercase rather than to Title Case or UPPERCASE?
> - In a dataset with hundreds of unique city names, doing this manually would not be practical. What would a smarter, scalable approach look like?

---

### Task 5 — Feature Engineering 🟡

**Why this matters:** Raw numeric values are not always the most useful representation for a model. Creating derived features — like binning continuous experience into categories — can make patterns easier for a model to learn.

**Steps:**

Create a new column called `experience_level` based on the following rules:

| Experience (years) | Label |
|--------------------|-------|
| 0–1 | `"junior"` |
| 2–5 | `"mid"` |
| 6 or more | `"senior"` |

**Hint:** Use `pd.cut()` or a custom function with `apply()`. Both approaches work — try to understand the difference.

**Expected Output Hint:** After this task, your DataFrame should have a new `experience_level` column. With the cleaned data from Tasks 3 and 4, you should see a mix of all three labels across the 6 rows.

> 🤔 **Reflect:**
> - The `experience_level` column is a text label ("junior", "mid", "senior"). Can a machine learning model use it directly as-is? If not, what would you need to do to it before training?
> - Why might a hiring model benefit from having both `experience` (raw number) **and** `experience_level` (binned category) as separate features?

---

### Task 6 — Normalize Numeric Features 🟡

**Why this matters:** Without normalization, a feature like `expected_salary` (range: 40,000–90,000) would dominate distance-based models and overshadow features like `age` (range: 19–30) or `experience` (range: 0–7).

**Steps:**

Apply **Min-Max normalization** to the following columns:
- `age`
- `experience`
- `expected_salary`

**Constraint:** Do not apply normalization to string/categorical columns. Use `select_dtypes()` or normalize only the listed columns explicitly.

**Expected Output Hint:** After normalization, all three columns should contain values strictly between 0.0 and 1.0 (inclusive). The smallest value in each column should be exactly 0.0, and the largest should be exactly 1.0.

> 🤔 **Reflect:**
> - We normalized `age` and `experience` — but should we also normalize `experience_level`? Why or why not?
> - At what point in the pipeline should normalization happen — before or after the train/test split? Why does the order matter? *(This was covered in the lecture — refer back if needed.)*

---

### Task 7 — Build a Preprocessing Function 🔴

**Why this matters:** In any real project, preprocessing is not a one-time operation. You run it on training data today, and you will run it on new incoming applicants tomorrow. A function ensures every piece of data goes through exactly the same steps every time — no exceptions.

**Steps:**

Wrap all preprocessing logic from Tasks 3–6 into a single reusable function:

```python
def preprocess_applicants(df):
    # Your pipeline here
    return df_clean
```

The function must:
- Accept a raw DataFrame as input
- Handle missing values (with the same strategies you chose in Task 3)
- Clean inconsistent categorical data (Task 4)
- Create the `experience_level` feature (Task 5)
- Normalize numeric features (Task 6)
- Return the fully cleaned DataFrame

**Test your function** by passing the original raw DataFrame into it and verifying the output matches what you produced step-by-step in the earlier tasks.

**Constraint:** The function should not hardcode specific values from the current dataset. For example, instead of `df["age"].fillna(22.5)`, use `df["age"].fillna(df["age"].median())` so the function works correctly on any new batch of data.

> 🤔 **Reflect:**
> - What would happen if someone passed a DataFrame with a completely different set of city abbreviations into your function? Would it still work correctly? How would you make it more robust?
> - Your function currently computes the median from whatever data is passed in. In a real deployment, should the median be recomputed every time, or should it be calculated once from the training data and stored? Why?

---

### Task 8 (Optional – Advanced) — Skills Analysis 🔴

**Why this matters:** The `skills` column contains Python lists — not a format any ML model can use directly. Before a model can learn from skills data, you need to convert it into numeric form. This is a simplified version of a real technique called feature extraction from text.

**Steps:**

**Part A — Skill Count Feature**
- Create a new column `skill_count` that contains the number of skills each applicant has
- For applicants with `null` skills (row 3), decide what value is most appropriate and justify it

**Part B — Skill Presence Features**
- Identify all unique skills that appear across the entire dataset
- For each unique skill, create a new binary column (0 or 1) that indicates whether that applicant has that skill
- Example: a column called `has_python` with value 1 if the applicant lists "python" in their skills, 0 otherwise

**Expected Output Hint:** After Part B, your DataFrame should have one new column for each unique skill found in the dataset. Count how many unique skills there are first, then verify your DataFrame gained that many new columns.

> 🤔 **Reflect:**
> - In this dataset we have 6 applicants and a small number of skills. In a real dataset with 10,000 applicants and 500 unique skills, this approach would create 500 new columns. What problems could that cause for a model? What is the term for this problem?
> - After converting skills to binary columns, do those columns need to be normalized? Why or why not?

---

## 6. GitHub Submission Checklist

Before submitting, verify all of the following:

**Code:**
- [ ] All code is in a single Jupyter notebook (`.ipynb`) inside `labs/week07/`
- [ ] Notebook runs from top to bottom without errors
- [ ] Each task starts with a markdown cell clearly labeling the task number and title
- [ ] Code is clean — no unused variables, no redundant print statements, no commented-out blocks

**README.md** (inside `labs/week07/`):
- [ ] Brief description of what each task does
- [ ] At least two decisions you made during preprocessing — and your reasoning for each
- [ ] One thing that surprised you or was harder than expected
- [ ] Answer to this question: *"If 100 new applicants were submitted tomorrow, what would you need to change in your pipeline?"*

**Data Quality:**
- [ ] No missing values remain in the final DataFrame (run `df.isnull().sum()` and include the output)
- [ ] All numeric columns are normalized to [0, 1]
- [ ] City names are consistent and lowercase

---

## 7. Expected Learning Outcomes

After completing this lab, you should be able to:

- Load and merge datasets from multiple file formats
- Detect and handle missing values using appropriate strategies per column
- Identify and fix inconsistent data that `isnull()` alone will not catch
- Apply normalization correctly and only to the right columns
- Build a reusable preprocessing function that works on new data
- Think critically about the reasoning behind each preprocessing decision

---

## 8. Evaluation Criteria

| Criteria | Weight |
|---|---|
| Task completion (Tasks 1–7 fully working) | 50% |
| Code clarity and structure | 15% |
| Quality of reasoning in README (decisions justified) | 20% |
| Correct preprocessing logic and order | 10% |
| GitHub structure and submission format | 5% |

> **Note:** A correct answer with no explanation is worth less than a reasonable answer with clear reasoning. The goal is to develop judgment, not just code that runs.

---

End of Lab Document
