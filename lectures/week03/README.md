# AI-216: Programming for Artificial Intelligence
## Week 03 – Functions & Object-Oriented Programming (OOP)

---

### Lecture Overview

In Week 2, you learned how to **think logically and write step-by-step code**. In Week 3, we move to the next level: **structured programming**.

This lecture introduces:
- Functions for modular, reusable logic
- Object-Oriented Programming (OOP) concepts
- The idea that **AI systems and ML models are objects**, not scattered scripts

By the end of this lecture, you will start thinking like a **software engineer building AI systems**, not just someone writing Python code.

---

## Learning Objectives

After completing this lecture, students will be able to:
- Write and use functions to organize logic
- Explain why modular code is important in AI systems
- Define and use classes and objects
- Identify attributes and methods in a class
- Relate OOP concepts to machine learning models

---

## 1. Functions & Modular Code

### Why Functions Matter

A **function** is a reusable block of code that performs a specific task.

In AI systems, functions are commonly used to:
- Clean raw data
- Transform values
- Compute statistics
- Prepare inputs for models

Functions help convert **messy data → usable data**, which is a core responsibility of AI engineers.

---

### Basic Example: Simple Function

```python
def greet():
    print("Welcome to AI-216")

greet()
```

*Key Idea:* The function hides details and can be reused.

---

### Intermediate Example: Function for Simple Data Transformation

```python
def normalize_score(score):
    return score / 100

scores = [78, 85, 92]

for s in scores:
    print(normalize_score(s))
```

*Key Idea:* Functions are used to apply the same transformation to multiple data points.

---

### Intermediate Example: Cleaning Invalid Data

```python
def clean_marks(marks):
    cleaned = []
    for m in marks:
        if m >= 0 and m <= 100:
            cleaned.append(m)
    return cleaned

raw_marks = [78, -5, 110, 67, 90]
valid_marks = clean_marks(raw_marks)
print(valid_marks)
```

*Key Idea:* Data cleaning is rule-based and repetitive — perfect for functions.

---

### Advanced Example: Modular Data Analysis Workflow

```python
def calculate_average(values):
    return sum(values) / len(values)


def preprocess_and_average(marks):
    cleaned = clean_marks(marks)
    return calculate_average(cleaned)

marks = [45, 88, -10, 72, 101, 90]
avg = preprocess_and_average(marks)
print("Average:", avg)
```

*Key Idea:* Real programs are built by **combining small, well-defined functions**.

---

## 2. Introduction to Object-Oriented Programming (OOP)

### What is OOP?

Object-Oriented Programming is a way of organizing code by **grouping data and behavior together**.

In OOP:
- **Class** → blueprint
- **Object** → real instance
- **Attributes** → data
- **Methods** → behavior

---

## 3. Classes & Objects

### Basic Example: Creating a Class

```python
class Student:
    pass

s1 = Student()
print(s1)
```

*Key Idea:* A class defines a type; objects are created from it.

---

### Intermediate Example: Attributes

```python
class Student:
    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

s1 = Student("Ali", 78)
s2 = Student("Sara", 85)

print(s1.name, s1.marks)
print(s2.name, s2.marks)
```

*Key Idea:* Each object has its own data.

---

### Advanced Example: Attributes + Methods

```python
class Student:
    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def is_passed(self):
        return self.marks >= 50

s1 = Student("Ali", 45)
s2 = Student("Sara", 88)

print(s1.name, "Passed:", s1.is_passed())
print(s2.name, "Passed:", s2.is_passed())
```

*Key Idea:* Objects **know how to act on their own data**.

---

## 4. Why OOP Matters in AI Systems

### Conceptual Connection

In AI and ML:
- A dataset is an object
- A model is an object
- A trained model has state and behavior

This is why libraries like scikit-learn use OOP heavily.

---

### Intermediate AI-Inspired Example

```python
class SimpleModel:
    def __init__(self, threshold):
        self.threshold = threshold

    def predict(self, value):
        return value >= self.threshold

model = SimpleModel(50)
print(model.predict(40))
print(model.predict(75))
```

*Key Idea:* ML models behave like objects with rules.

---

### Advanced Example: Simulating an ML-Like Workflow

```python
class ThresholdClassifier:
    def __init__(self, threshold):
        self.threshold = threshold

    def predict(self, data):
        results = []
        for value in data:
            results.append(value >= self.threshold)
        return results

classifier = ThresholdClassifier(60)
data = [45, 70, 80, 30]

predictions = classifier.predict(data)
print(predictions)
```

*Key Idea:* This mirrors how real ML models process datasets.

---

## 5. Thinking Like an AI Engineer

Before writing code, ask:
1. What entities exist? (Student, Dataset, Model)
2. What data do they hold?
3. What actions should they perform?

This mindset makes large AI systems manageable.

---

## 6. Common Mistakes to Avoid

- Writing everything in one script
- Avoiding functions when logic repeats
- Treating classes as "advanced" or unnecessary
- Mixing data and logic without structure

---

## 7. ChatGPT Prompts for Learning (Allowed Use)

Use ChatGPT to **think, plan, and understand**, not to generate final solutions.

---

### A. Functions & Modular Thinking

**Typical Problems**
- Repeated logic
- Long scripts

**Prompts**
- "Can you help me break this program into functions?"
- "What should be the input and output of this function?"
- "How can I simplify this logic using reusable functions?"

---

### B. Understanding Classes & Objects

**Typical Problems**
- Confusion between class and object
- Forgetting `self`

**Prompts**
- "Explain classes and objects using a real-life example"
- "What attributes and methods should this class have?"
- "Why is `self` required in class methods?"

---

### C. OOP in AI Context

**Typical Problems**
- Understanding why OOP is needed

**Prompts**
- "How does this class relate to a machine learning model?"
- "Can you explain this OOP code in terms of data and behavior?"
- "How would this class scale to larger datasets?"

---

### D. Debugging & Code Clarity

**Typical Situations**
- Attribute errors
- Unexpected behavior

**Prompts**
- "Why am I getting an attribute error here?"
- "Can you explain this class method line by line?"
- "How can I improve readability without changing logic?"

---

<!-- ## 8. Looking Ahead

In **Week 4**, we will apply this structured thinking to **data structures** (lists, dictionaries, sets), which are essential for organizing datasets in AI systems.

---

**End of Week 03 Lecture**
 -->
