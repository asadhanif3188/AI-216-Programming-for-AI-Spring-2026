# AI-216 – Programming for Artificial Intelligence
## Assignment 02: Structured Programming & Data Modeling

---

### Coverage: Week 03 (Functions & OOP) + Week 04 (Data Structures)
### Difficulty Level: High
### Submission Mode: GitHub (Mandatory)

---

## 1. Assignment Purpose

This assignment evaluates your ability to:

- Design modular programs using functions
- Model structured data using appropriate data structures
- Implement Object-Oriented Programming concepts
- Combine lists, tuples, dictionaries, and sets effectively
- Think like an AI engineer organizing data before modeling

This is not a syntax exercise. It is a **design and reasoning assessment**.

---

## 2. Learning Outcomes Assessed

- Apply structured programming using reusable functions
- Design and implement classes with meaningful attributes and methods
- Select appropriate data structures for real-world problems
- Combine OOP with nested data structures

---

## 3. Academic Integrity Rules

- You may use AI tools for understanding concepts only.
- You must NOT generate full solutions using AI.
- You must be able to explain every design decision.
- Code similarity or copy-based solutions will be penalized.

Oral defense may be conducted if required.

---

# 4. Problem 1: Student Performance Analytics System

You are required to design a **Student Performance Analytics System**.

The system should simulate a small academic analytics tool using:

- Functions
- Classes
- Lists
- Tuples
- Dictionaries
- Sets

---

## Dataset (You Must Use This)

```python
students_data = [
    {"id": "S01", "name": "Ali", "scores": (78, 85, 90)},
    {"id": "S02", "name": "Sara", "scores": (88, 92, 79)},
    {"id": "S03", "name": "Ahmed", "scores": (45, 60, 55)},
    {"id": "S04", "name": "Zain", "scores": (95, 91, 89)}
]
```

Each student contains:
- id → string
- name → string
- scores → tuple of 3 subject marks

---

## Required Components (Problem 1)

### Part A – Functional Design (Modular Programming)

Create separate functions to:

1. Calculate average score of a student
2. Determine grade based on average:
   - ≥ 85 → A
   - 70–84 → B
   - 50–69 → C
   - Below 50 → Fail
3. Identify top-performing student
4. Return a list of students who passed all subjects (each subject ≥ 50)

Functions must return values (avoid printing inside functions unless necessary).

---

### Part B – Object-Oriented Design

Create a class called `StudentAnalytics` that:

#### Attributes:
- students_data (list of dictionaries)

#### Methods:
1. compute_results() → Adds average & grade to each student
2. get_top_student()
3. get_class_average()
4. get_unique_grades() → Return a set of distinct grades awarded
5. generate_report() → Return a dictionary structured as:

```python
{
    "class_average": value,
    "top_student": "Name",
    "grade_distribution": {"A": count, "B": count, ...}
}
```

---

### Advanced Requirement (Problem 1)

Extend the system with:

- A method that identifies students whose performance improved consistently (scores strictly increasing in tuple)
- A method that converts internal student data into a "tabular-like" structure:

```python
{
    "ids": [...],
    "names": [...],
    "averages": [...],
    "grades": [...]
}
```

---

# 5. Problem 2: Course Enrollment & Performance System

Design a second independent system that combines **data structures + OOP + modular functions**.

---

## Dataset (You Must Use This)

```python
courses_data = {
    "Python": {
        "instructor": "Dr. A",
        "students": {"S01", "S02", "S03"}
    },
    "Machine Learning": {
        "instructor": "Dr. B",
        "students": {"S02", "S04"}
    },
    "Data Science": {
        "instructor": "Dr. C",
        "students": {"S01", "S04"}
    }
}
```

---

## Required Components (Problem 2)

### Part A – Functional Requirements

Create functions to:

1. Find students enrolled in more than one course
2. Identify courses with more than 2 students
3. Generate a dictionary mapping each student → number of enrolled courses
4. Return a set of all unique students across all courses

---

### Part B – OOP Design

Create a class called `CourseAnalytics` that:

#### Attributes:
- courses_data (dictionary)

#### Methods:
1. get_multi_course_students()
2. get_student_course_count()
3. get_largest_course()
4. generate_course_report() → returns structured summary:

```python
{
    "total_courses": value,
    "total_unique_students": value,
    "largest_course": "Course Name",
    "student_course_distribution": {...}
}
```

---

### Advanced Requirement (Problem 2)

Add a method that:

- Converts course-centered data into student-centered structure:

```python
{
    "S01": ["Python", "Data Science"],
    "S02": ["Python", "Machine Learning"],
    ...
}
```

This transformation must be generated programmatically.

---

# 6. Data Structure Justification (Written in README)

For both problems, explain:

- Why sets are used for enrollment
- Why tuples are used for fixed scores
- Why dictionaries are suitable for structured mapping
- Why classes improve system organization

This explanation is graded.

---

# 7. Output Expectations

Your program should:

- Instantiate both classes
- Call major methods
- Print final structured reports clearly

Code must be modular and readable.

---

# 8. GitHub Submission Structure

```text
AI-216-Programming-for-AI/
└── assignments/
    └── assignment02/
        ├── assignment02.py or .ipynb
        └── README.md
```

---

# 9. Evaluation Criteria

| Criterion | Weight |
|-----------|--------|
| Problem 1 – Functional & OOP design | 30% |
| Problem 2 – Functional & OOP design | 30% |
| Advanced features (both problems) | 20% |
| Correct data structure usage | 10% |
| Code clarity & organization | 5% |
| README justification quality | 5% |

---

# 10. Important Notes

- Avoid writing everything inside one large function.
- Avoid global variables.
- Use meaningful variable names.
- Structure your logic clearly.

This assignment prepares you directly for:
- Structured data pipelines
- ML-style model APIs
- Pandas DataFrame conversion

---

**End of Assignment 02**

