# AI-216: Programming for Artificial Intelligence
## Week 04 – Data Structures for AI

---

### Lecture Overview

In previous weeks, you learned:
- How to write logical programs (Week 2)
- How to structure programs using functions and classes (Week 3)

In Week 4, we focus on **organizing data properly**.

Artificial Intelligence is not just about models — it is about **managing data efficiently** before modeling.

This lecture introduces:
- Lists
- Tuples
- Dictionaries
- Sets
- How to choose the right structure for a problem

These structures form the **foundation for Pandas and NumPy**, which we will use later.

---

## Learning Objectives

After completing this lecture, students will be able to:
- Create and manipulate lists, tuples, dictionaries, and sets
- Choose appropriate data structures for different tasks
- Perform basic data manipulation operations
- Understand how data structures prepare us for Pandas

---

# 1. Lists – Ordered, Mutable Collections

Lists are ordered collections of elements that can be modified.

---

## Basic Example

```python
marks = [78, 85, 90, 67]
print(marks)
print(marks[0])
```

---

## Basic Example 2 – List Operations

```python
numbers = [10, 20, 30]

numbers.append(40)
numbers.insert(1, 15)
numbers.remove(30)

print(numbers)
```

---

## Intermediate Example – Updating & Iterating

```python
marks = [78, 85, 90, 67]
marks.append(88)

for m in marks:
    print(m)
```

---

## Intermediate Example 2 – Aggregation & Filtering

```python
scores = [45, 82, 91, 38, 76]

passed = []
for s in scores:
    if s >= 50:
        passed.append(s)

average = sum(passed) / len(passed)

print("Passed Scores:", passed)
print("Average of Passed:", average)
```

---

## Advanced Example – Data Cleaning with Lists

```python
raw_scores = [95, -5, 102, 88, 76]

cleaned_scores = []
for score in raw_scores:
    if 0 <= score <= 100:
        cleaned_scores.append(score)

print(cleaned_scores)
```

---

## Advanced Example 2 – List of Records (Preparing for Pandas)

```python
students = [
    {"name": "Ali", "marks": 78},
    {"name": "Sara", "marks": 92},
    {"name": "Ahmed", "marks": 45}
]

for student in students:
    if student["marks"] >= 50:
        print(student["name"], "Passed")
```

*AI Connection:* Lists often represent rows of data before using DataFrames.

---

---

# 2. Tuples – Ordered, Immutable Collections

Tuples are like lists, but they cannot be changed after creation.

---

## Basic Example

```python
coordinates = (24.86, 67.01)
print(coordinates)
```

---

## Intermediate Example – Fixed Records

```python
student_record = ("Ali", 78, 85, 90)
name = student_record[0]
print(name)
```

---

## Advanced Example – Returning Multiple Values

```python
def get_min_max(values):
    return min(values), max(values)

result = get_min_max([45, 78, 12, 90])
print(result)
```

*AI Connection:* Many ML functions return tuples (e.g., metrics).

---

# 3. Dictionaries – Key-Value Mapping

Dictionaries store data as key-value pairs.

---

## Basic Example

```python
student = {
    "name": "Ali",
    "age": 20,
    "marks": 85
}

print(student["name"])
```

---

## Basic Example 2 – Adding & Updating Values

```python
student = {"name": "Ali", "marks": 78}

student["marks"] = 85
student["grade"] = "A"

print(student)
```

---

## Intermediate Example – Iterating Over Dictionary

```python
student = {
    "Ali": 78,
    "Sara": 90,
    "Ahmed": 67
}

for name, mark in student.items():
    print(name, mark)
```

---

## Intermediate Example 2 – Aggregation from Dictionary

```python
marks = {
    "Ali": 78,
    "Sara": 90,
    "Ahmed": 67
}

total = 0
for value in marks.values():
    total += value

average = total / len(marks)
print("Class Average:", average)
```

---

## Advanced Example – Nested Data

```python
class_data = {
    "Ali": {"math": 78, "english": 85},
    "Sara": {"math": 90, "english": 88}
}

print(class_data["Ali"]["math"])
```

---

## Advanced Example 2 – Dictionary of Lists (Feature Representation)

```python
dataset = {
    "names": ["Ali", "Sara", "Ahmed"],
    "marks": [78, 92, 45]
}

for i in range(len(dataset["names"])):
    print(dataset["names"][i], dataset["marks"][i])
```

*AI Connection:* JSON data, API responses, and tabular datasets are dictionary-based.

---

---

# 4. Sets – Unique, Unordered Collections

Sets automatically remove duplicates.

---

## Basic Example

```python
numbers = {1, 2, 3, 3, 4}
print(numbers)
```

---

## Intermediate Example – Removing Duplicates from Data

```python
emails = ["a@gmail.com", "b@gmail.com", "a@gmail.com"]
unique_emails = set(emails)
print(unique_emails)
```

---

## Advanced Example – Set Operations

```python
students_A = {"Ali", "Sara", "Ahmed"}
students_B = {"Sara", "Zain"}

common = students_A.intersection(students_B)
print(common)
```

*AI Connection:* Feature selection and category comparison use set logic.

---

# 5. Choosing the Right Data Structure

Before writing code, ask:

| Need | Use |
|------|------|
| Ordered data | List |
| Fixed record | Tuple |
| Key-based access | Dictionary |
| Unique elements | Set |

---

## Advanced Comparison Example

Problem: Store student marks and quickly retrieve marks by name.

- List → Not efficient
- Dictionary → Best choice

---

# 6. Data Structures & Pandas Connection

Pandas DataFrame:
- Columns → Similar to dictionaries
- Rows → Similar to list of records

Understanding native Python structures makes Pandas easier.

---

# 7. ChatGPT Prompts for Learning (Allowed Use)

Use ChatGPT to understand concepts, not to generate full solutions.

---

### A. Choosing Data Structures

- "Which data structure should I use for this problem and why?"
- "What is the difference between list and tuple in practical terms?"

---

### B. Dictionaries & Nested Data

- "How can I access nested dictionary values step by step?"
- "Why is a dictionary better than a list for key-based access?"

---

### C. Sets & Data Cleaning

- "How do sets help remove duplicates?"
- "When should I use set intersection?"

---

### D. Debugging & Understanding

- "Explain this data structure code line by line"
- "Why am I getting a KeyError?"

---

<!-- # 8. Looking Ahead

In Week 5, we will use NumPy and Pandas — tools built on these concepts.

Understanding data structures today makes data science easier tomorrow.

---

**End of Week 04 Lecture** -->

