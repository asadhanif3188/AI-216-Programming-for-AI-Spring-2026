# AI-216 – Programming for Artificial Intelligence
## Lab 04: Data Structures for AI

---

### Week #: 04  
### Topic: Lists, Tuples, Dictionaries & Sets for Data Organization

---

## 1. Objective

The objective of this lab is to develop strong **data organization skills** using Python’s built-in data structures. Students will:

- Select appropriate data structures for different scenarios
- Manipulate structured data effectively
- Combine multiple data structures in a single program

This lab builds the foundation required for working with **Pandas DataFrames** in upcoming weeks.

---

## 2. Background

As introduced in Week 4 lecture, different problems require different data structures:

- Lists → ordered, mutable collections
- Tuples → fixed, immutable records
- Dictionaries → key-value mappings
- Sets → uniqueness & membership checks

This lab is inspired by the general structure of the previous data structures lab fileciteturn3file0, but contains **new problem scenarios** and requires independent implementation.

No solutions are provided. You must design the logic yourself.

---

## 3. Tools & Libraries

- Python 3.x
- VS Code or Jupyter Notebook
- GitHub (mandatory submission)

No external libraries allowed.

---

## 4. Tasks

### Task 1: Product Price Analyzer (Lists)

**Sample Data**
```python
prices = [1200, 850, 4300, 2999, 1500, 850]
```

**Requirements**
1. Print the total number of products
2. Calculate the average price
3. Create a new list containing only products above 2000
4. Sort the prices in descending order

**Focus Concepts**
- List operations
- Iteration
- Aggregation
- Filtering

---

### Task 2: Geographic Coordinates Manager (Tuples)

**Sample Data**
```python
locations = [
    (24.8607, 67.0011),
    (31.5204, 74.3587),
    (33.6844, 73.0479)
]
```

**Requirements**
1. Print each coordinate pair
2. Extract latitude values into a separate list
3. Attempt to modify a tuple element and explain (in comment) what happens
4. Count how many coordinate pairs exist

**Focus Concepts**
- Tuple immutability
- Indexing
- Looping through tuple collections

---

### Task 3: Course Enrollment System (Sets)

**Sample Data**
```python
python_students = {"Ali", "Sara", "Ahmed", "Zain"}
ml_students = {"Sara", "Hassan", "Ali", "Fatima"}
```

**Requirements**
1. Find students enrolled in both courses
2. Find students enrolled only in Python
3. Combine both groups into a master student set
4. Add a new student to the ML course

**Focus Concepts**
- Set operations (intersection, difference, union)
- Membership checking
- Uniqueness handling

---

### Task 4: Employee Records Organizer (Dictionaries)

**Sample Data**
```python
employees = {
    "E01": {"name": "Ali", "salary": 60000},
    "E02": {"name": "Sara", "salary": 75000},
    "E03": {"name": "Ahmed", "salary": 50000}
}
```

**Requirements**
1. Print all employee IDs
2. Calculate total payroll (sum of salaries)
3. Identify employees earning above 60000
4. Add a new employee record

**Focus Concepts**
- Nested dictionaries
- Key-based access
- Aggregation from values

---

### Task 5 (Advanced Challenge): Structured Sales Summary

**Sample Data**
```python
sales_data = {
    "electronics": [
        ("Laptop", 120000, 3),
        ("Mouse", 1500, 10)
    ],
    "clothing": [
        ("Shirt", 2500, 5),
        ("Shoes", 5000, 2)
    ]
}
```

Each tuple represents:
(product_name, price, quantity_sold)

**Requirements**
1. Calculate total revenue for each category
2. Store results in a new dictionary
3. Use a set to track unique product names across all categories
4. Print a structured revenue report

**Focus Concepts**
- Dictionary of lists
- Tuples inside lists
- Combining multiple data structures
- Real-world data modeling

---

## 5. Extra Question (Comprehensive Challenge)

### Inventory Management System

Develop a simple inventory management system for a small retail store.

You must use:

- A **dictionary** where keys are category names (e.g., "electronics", "clothing")
- Values as **lists of tuples**, where each tuple contains:
  `(product_name, price, quantity)`

---

### Requirements

Implement functions to:

1. **Add a new product to a category**  
   - If the category does not exist, create it.
   - Ensure no duplicate product names within a category (use a set).

2. **Update the quantity of an existing product**  
   - Modify the appropriate tuple logically (remember tuples are immutable).

3. **Remove sold-out products**  
   - Remove products where `quantity == 0`
   - Use a **set** to track unique product names across categories

4. **Generate a report**  
   - Create a dictionary mapping each category to its total inventory value
   - Total value = `sum(price × quantity)` for each product in that category

---

### Testing Requirements

- Use at least **3 categories**
- Include at least **5 products in total**
- Print:
  - Final inventory structure
  - Generated report dictionary

---

### Focus Concepts

- Dictionary of lists
- Tuples inside lists
- Set for uniqueness handling
- Nested iteration
- Data modeling for real-world systems
- Combining multiple data structures

This challenge integrates everything learned in Week 4 and prepares you for structured tabular data processing in future weeks.

---

## 6. GitHub Submission Checklist ✅

Before submitting, ensure:

- Code is pushed to:
  `labs/week04/`
- Meaningful commit messages are used
- A `README.md` file includes:
  - Explanation of chosen data structures
  - Why they were appropriate
  - Challenges faced

---

## 7. LinkedIn / Written Reflection (Required)

Write a 3–5 line reflection covering:

- Which data structure was most useful and why
- One difficulty you faced
- How this lab prepares you for working with Pandas

(Private written submission allowed if preferred.)

---

## 8. Expected Learning Outcomes

After completing this lab, students should be able to:

- Select appropriate data structures for given problems
- Combine lists, tuples, sets, and dictionaries effectively
- Organize structured data clearly
- Prepare for tabular data manipulation in future weeks

---

<!-- ## 9. Evaluation Criteria

| Criterion | Weight |
|----------|--------|
| Task completion | 40% |
| Correct data structure usage | 30% |
| Code clarity & organization | 15% |
| GitHub structure & documentation | 10% |
| Reflection quality | 5% |

---

---



**End of Lab 04**
 -->
