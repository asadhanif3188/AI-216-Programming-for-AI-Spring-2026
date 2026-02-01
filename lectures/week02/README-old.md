# AI-216: Programming for Artificial Intelligence
## Week 02 – Python Basics for Problem Solving

---

### Lecture Overview
This lecture builds the **logical foundation of programming** required for Artificial Intelligence. The focus is not on memorizing Python syntax, but on learning how to **think in terms of problems, decisions, and repetition**, and then expressing that thinking using Python.

By the end of this lecture, you should feel confident reading a problem, breaking it into steps, and writing Python code that solves it.

---

## Learning Objectives
After completing this lecture, students will be able to:
- Use variables to store and manipulate data
- Identify and apply appropriate data types
- Implement decision-making using conditional statements
- Use loops to handle repeated logic
- Translate real-world problems into step-by-step logic

---

## 1. Variables & Data Types

### Concept
A **variable** is a named storage location that holds a value. A **data type** tells Python what kind of value it is dealing with.

Common data types:
- `int` – whole numbers
- `float` – decimal numbers
- `str` – text
- `bool` – True / False

Think of variables as *state holders* in a problem.

---

### Basic Example
```python
age = 20
name = "Ali"
is_registered = True
print(age, name, is_registered)
```

---

### Intermediate Example
```python
marks = 85
percentage = marks / 100
status = "Passed"
print("Percentage:", percentage)
print("Status:", status)
```

---

### Advanced / Difficult Example
```python
total_marks = 500
obtained_marks = 423
percentage = (obtained_marks / total_marks) * 100
is_distinction = percentage >= 85

print("Percentage:", percentage)
print("Distinction:", is_distinction)
```

*Key Thinking:* What values change? What values are derived?

---

## 2. Conditional Statements (Decision Making)

### Concept
Conditional statements allow a program to **choose** what to do based on conditions.

Core keywords:
- `if`
- `elif`
- `else`

This is the foundation of rule-based reasoning used later in AI models like Decision Trees.

---

### Basic Example
```python
marks = 60

if marks >= 50:
    print("Pass")
else:
    print("Fail")
```

---

### Intermediate Example
```python
marks = 78

if marks >= 85:
    grade = "A"
elif marks >= 70:
    grade = "B"
elif marks >= 50:
    grade = "C"
else:
    grade = "Fail"

print("Grade:", grade)
```

---

### Advanced / Difficult Example
```python
attendance = 82
marks = 74

if attendance >= 75 and marks >= 50:
    result = "Eligible"
elif attendance < 75:
    result = "Low Attendance"
else:
    result = "Fail"

print(result)
```

*Key Thinking:* Identify rules first, then encode them.

---

## 3. Loops (Repetition & Scale)

### Concept
Loops allow a program to **repeat logic**. AI systems work with large amounts of data — loops make this possible.

Main loop types:
- `for` loop
- `while` loop

---

### Basic Example
```python
for i in range(5):
    print(i)
```

---

### Intermediate Example
```python
marks = [65, 70, 80, 45, 90]

passed = 0
for m in marks:
    if m >= 50:
        passed += 1

print("Passed students:", passed)
```

---

### Advanced / Difficult Example
```python
marks = [45, 67, 89, 34, 76, 92]

high_achievers = 0
for m in marks:
    if m >= 85:
        high_achievers += 1

percentage = (high_achievers / len(marks)) * 100
print("High achiever percentage:", percentage)
```

*Key Thinking:* What logic needs to be repeated? What must be counted or accumulated?

---

## 4. Thinking in Logic, Not Syntax (Most Important Section)

### Problem-Solving Framework
Before writing code, always answer:
1. What is the input?
2. What decisions are needed?
3. What repeats?
4. What is the output?

---

### Integrated Example (Step-by-Step Thinking)

**Problem:** Given marks of students, count how many passed and failed.

```python
marks = [55, 32, 78, 40, 90]
pass_count = 0
fail_count = 0

for m in marks:
    if m >= 50:
        pass_count += 1
    else:
        fail_count += 1

print("Pass:", pass_count)
print("Fail:", fail_count)
```

This structure (input → logic → output) will appear again in:
- Data preprocessing
- Machine learning pipelines
- Model evaluation

---

## 5. Common Mistakes to Watch For
- Confusing `=` with `==`
- Forgetting indentation
- Writing logic without planning
- Hardcoding values instead of using variables

---

## 6. Practice Tasks (Self-Study)
- Modify examples to change rules
- Add new conditions
- Count different categories
- Rewrite logic using your own values

---

## 7. ChatGPT Prompts for Learning (Allowed Use)
Students may use ChatGPT **only for understanding and learning**, not copying final answers.

### Understanding Concepts
- "Explain Python variables using a real-life example"
- "Why are data types important in Python?"

### Logic Building
- "Help me break this problem into steps before coding"
- "What conditions should I check in this problem?"

### Code Improvement
- "How can I make this Python loop more readable?"
- "Explain this Python code line by line"

### Debugging Support
- "Why is my if-else not working as expected?"
- "What does this error message mean in simple terms?"

⚠️ **Reminder:** You must be able to explain your code in your own words.

---

<!-- ## 8. Looking Ahead
In **Week 3**, we will move from writing linear scripts to **structured programs** using functions and object-oriented programming.

Think of Week 2 as learning *how to think*, and Week 3 as learning *how to organize that thinking*.

---

**End of Week 02 Lecture** -->

