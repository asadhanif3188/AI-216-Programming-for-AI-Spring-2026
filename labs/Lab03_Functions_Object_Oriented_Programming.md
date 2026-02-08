# AI-216 – Programming for Artificial Intelligence
## Lab 03: Functions & Object-Oriented Programming (OOP)

---

### Week #: 03  
### Topic: Functions, Modular Code & Object-Oriented Programming

---

## 1. Objective

The objective of this lab is to help students transition from **linear scripts** to **structured programs** using:
- Functions for modular logic
- Classes and objects for organizing data and behavior

This lab reinforces the mindset that **AI systems are built from interacting components**, not single long scripts.

---

## 2. Background

Modern AI and machine learning systems are written using **structured and modular code**. Instead of writing everything in one file:
- Functions are used to break large problems into smaller steps
- Classes are used to represent real-world or AI-related entities (datasets, models, evaluators)

This lab focuses on:
- Designing meaningful functions
- Creating simple classes with attributes and methods
- Understanding how objects manage their own data

---

## 3. Tools & Libraries

- Python 3.x
- VS Code or Jupyter Notebook
- GitHub (mandatory for submission)

No external libraries are required.

---

## 4. Tasks


### Task 1: Data Cleaning Functions (Basic)

**Problem Statement**  
You are given raw numeric data collected from a sensor.

**Sample Data (for reference)**
```python
sensor_readings = [45, 78, -12, 90, 105, 66, 88]
```

Write Python functions to:
1. Remove invalid readings (values below 0 or above 100)
2. Calculate the average of the cleaned data

**Focus Concepts**
- Function definition
- Parameters and return values
- Modular data processing

---

### Task 2: Student Record Processor (Intermediate)

**Problem Statement**  
Each student has a name and a list of quiz marks.

**Sample Data (for reference)**
```python
students = {
    "Ali": [65, 70, 80],
    "Sara": [90, 85, 88],
    "Ahmed": [40, 55, 60]
}
```

Write a program using functions that:
1. Calculates the average marks of a student
2. Determines whether the student has passed (average ≥ 50)
3. Displays a clear summary for each student

**Focus Concepts**
- Functions calling other functions
- Logical separation of tasks
- Reusable code

---

### Task 3: Simple Dataset Class (Intermediate)

**Problem Statement**  
Create a class that represents a small numeric dataset.

**Sample Data (for reference)**
```python
data_values = [12, 18, 25, 30, 22, 27]
```

The class should:
1. Store a list of values as an attribute
2. Have a method to return the number of data points
3. Have a method to calculate and return the average

**Focus Concepts**
- Class definition
- Attributes and methods
- Object-based data handling

---

### Task 4: Rule-Based Classifier (Advanced)

**Problem Statement**  
You are required to simulate a very simple rule-based classifier.

**Sample Data (for reference)**
```python
threshold = 60
values = [45, 72, 88, 30, 65]
```

Create a class that:
1. Stores a threshold value
2. Has a method that classifies a single value as True/False based on the threshold
3. Has another method that classifies a list of values

**Focus Concepts**
- OOP design thinking
- Methods operating on internal state
- ML-inspired abstraction

---

### Task 5 (Optional Challenge): Modular Data Analysis Pipeline

**Problem Statement**  
Design a small program that:
1. Uses functions to clean numeric data
2. Uses a class to store cleaned data
3. Uses class methods to compute summary statistics

**Sample Data (for reference)**
```python
raw_data = [10, 55, -3, 78, 120, 66, 92]
```

**Focus Concepts**
- Combining functions and classes
- End-to-end structured program design
- AI-style workflow thinking

---

## 5. GitHub Submission Checklist

Before submitting, ensure:
- Code is pushed to:  
  `labs/week03/`
- Meaningful commit messages are used
- A `README.md` file explains:
  - Each task briefly
  - Design decisions
  - Challenges faced

---

## 6. LinkedIn / Written Reflection (Required)

Write a **3–5 line reflection** covering:
- What new concept (functions or OOP) felt most useful
- One difficulty you faced while structuring code
- How this lab relates to AI or machine learning systems

(Students who prefer privacy may submit a written reflection instead.)

---

## 7. Expected Learning Outcomes

After completing this lab, students should be able to:
- Break problems into reusable functions
- Design simple classes with clear responsibilities
- Understand how objects manage data and behavior
- Write cleaner, more maintainable Python programs

---
