# AI-216 – Programming for Artificial Intelligence
## Lab 05: NumPy & Pandas – Data-Centric Programming

---

### Week #: 05  
### Topic: NumPy Arrays, Pandas DataFrames & Data Filtering

---

## 1. Objective

The objective of this lab is to transition from basic Python programming to **data-centric programming** using NumPy and Pandas.

Students will:

- Perform multi-dimensional array operations using NumPy
- Apply vectorized computation instead of loops
- Load, clean, and manipulate CSV data using Pandas
- Perform filtering, slicing, grouping, and aggregation
- Prepare structured data for machine learning workflows

---

## 2. Tools & Requirements

- Python 3.x
- NumPy
- Pandas
- Jupyter Notebook or VS Code
- GitHub (mandatory submission)

No external visualization libraries allowed.

---

# 3. Part A – NumPy Data Processing

---

### Task 1: Sensor Data Matrix Analysis

You are given simulated sensor readings from 4 machines over 5 time intervals.

```python
import numpy as np

sensor_data = np.array([
    [12, 15, 14, 10, 13],
    [20, 22, 19, 18, 21],
    [30, 28, 27, 29, 31],
    [25, 24, 26, 23, 22]
])
```

Each row represents a machine.
Each column represents a time interval.

#### Requirements

1. Compute average reading per machine (row-wise)
2. Compute maximum reading per time interval (column-wise)
3. Normalize the matrix using broadcasting:
   - Divide each value by the maximum value in its column
4. Identify machines where average reading > 20
5. Reshape the matrix into a 2D array of shape (2, 10)

Focus Concepts:
- axis operations
- broadcasting
- reshaping
- boolean indexing

---

### Task 2: Matrix Combination & Filtering

Create two 3×3 matrices with random integers between 1 and 50.

#### Requirements

1. Perform matrix multiplication
2. Perform element-wise multiplication
3. Extract elements greater than 100 from matrix multiplication result
4. Replace elements less than 10 in original matrices with 0
5. Vertically stack both matrices

Focus Concepts:
- @ operator
- element-wise vs matrix multiplication
- boolean masking
- stacking

---

# 4. Part B – Pandas Data Handling

You are provided a small e-commerce dataset below.

```python
import pandas as pd

sales_data = {
    "OrderID": [101, 102, 103, 104, 105, 106],
    "Customer": ["Ali", "Sara", "Ahmed", "Ali", "Zain", "Sara"],
    "City": ["Karachi", "Lahore", "Karachi", "Islamabad", "Lahore", "Karachi"],
    "Category": ["Electronics", "Clothing", "Electronics", "Groceries", "Clothing", "Electronics"],
    "Amount": [12000, 3500, None, 2400, 5200, 15000]
}


df = pd.DataFrame(sales_data)
```

---

### Task 3: Data Cleaning & Inspection

1. Display first 3 rows
2. Identify missing values
3. Fill missing Amount values using median
4. Convert Amount to integer type
5. Save cleaned dataset to CSV file

Focus Concepts:
- isnull()
- fillna()
- astype()
- to_csv()

---

### Task 4: Filtering & Derived Features

1. Create new column "HighValue" where Amount > 10000
2. Filter orders from Karachi
3. Filter orders where Category is Electronics and Amount > 10000
4. Sort data by Amount (descending)
5. Find top 2 customers by total spending

Focus Concepts:
- boolean filtering
- multiple conditions
- sorting
- groupby() and aggregation

---

### Task 5: Grouping & Aggregation Analysis

1. Compute total revenue per city
2. Compute average order amount per category
3. Count number of unique customers per city
4. Create a pivot table: City vs Category (total Amount)
5. Convert grouped result into a reset index DataFrame

Focus Concepts:
- groupby()
- agg()
- nunique()
- pivot_table()
- reset_index()

---

# 5. Advanced Challenge – Mini Preprocessing Pipeline

Using the same DataFrame:

1. Add a new column "TaxedAmount" = Amount × 1.15
2. Standardize City names to lowercase
3. Remove duplicate customers keeping highest purchase
4. Create a summary dictionary:

```python
{
    "total_orders": value,
    "total_revenue": value,
    "average_order": value,
    "top_city": "CityName"
}
```

5. Export final processed DataFrame to "final_sales_report.csv"

Focus Concepts:
- apply or vectorized operations
- sorting + drop_duplicates()
- summary statistics
- CSV export

---

# 6. GitHub Submission Checklist

Ensure:

- Code file saved as:
  `lab05_numpy_pandas.py` or notebook
- Folder structure:

```text
AI-216-Programming-for-AI/
└── labs/
    └── week05/
        ├── lab05.py or .ipynb
        └── README.md
```

README must explain:
- Difference between NumPy & Pandas usage in this lab
- Why vectorization is preferred over loops
- How missing data was handled

---
<!-- 
# 7. Evaluation Criteria

| Criterion | Weight |
|------------|--------|
| NumPy implementation | 25% |
| Pandas data cleaning | 20% |
| Filtering & grouping logic | 25% |
| Advanced pipeline | 20% |
| Code clarity & documentation | 10% |

---

**End of Lab 05**
 -->
