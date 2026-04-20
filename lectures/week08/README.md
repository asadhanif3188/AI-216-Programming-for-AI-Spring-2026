# AI-216: Programming for Artificial Intelligence
## Week 08 – Machine Learning Pipeline & Model Evaluation

---

## Lecture Overview

By Week 08, students have learned:
- Data handling (NumPy, Pandas)
- Data collection (scraping, databases)

Now we complete the journey:

> **From data → to trained model → to evaluation**

This lecture focuses on:
- Training vs Testing
- Model evaluation
- scikit-learn workflow

---

## Learning Objectives

After this lecture, students will be able to:

- Split datasets into training and testing sets
- Train machine learning models using scikit-learn
- Evaluate model performance using metrics
- Build a complete ML pipeline

---

# 1. Training vs Testing Data

Machine learning models learn patterns from data.

We divide data into:

- **Training data** → used to train the model
- **Testing data** → used to evaluate the model

---

## Why Split Data?

If we train and test on the same data:

- Model may memorize instead of learning
- Results become misleading

---

## Basic Example – Manual Split

```python
X = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

X_train = X[:3]
X_test = X[3:]

print(X_train, X_test)
```

---

## Intermediate Example – Using scikit-learn

```python
from sklearn.model_selection import train_test_split

X = [[1], [2], [3], [4], [5]]
y = [2, 4, 6, 8, 10]

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.4, random_state=42
)

print(X_train, X_test)
```

---

## Advanced Insight – Overfitting

If model performs:

- Very well on training data
- Poorly on testing data

→ This is called **overfitting**

---

# 2. Introduction to scikit-learn (Basics)

Before using machine learning models, we need to understand what **scikit-learn** is.

## What is scikit-learn?

scikit-learn is a Python library used for:

- Machine learning algorithms
- Data preprocessing
- Model evaluation

It provides ready-to-use implementations of common ML models.

---

## Installation

```python
pip install scikit-learn
```

---

## Basic Terminology

- **Feature (X)** → input data
- **Target (y)** → output/label
- **Model** → algorithm that learns from data

Example:

```python
X = [[1], [2], [3], [4]]   # Hours studied
y = [50, 55, 65, 70]      # Scores
```

---

## Basic Workflow in scikit-learn

All models follow the same structure:

```text
1. Import model
2. Create model object
3. Fit (train) the model
4. Predict
```

---

## Basic Example – First Model

```python
from sklearn.linear_model import LinearRegression

# Data
X = [[1], [2], [3], [4]]
y = [50, 55, 65, 70]

# Step 1: Create model
model = LinearRegression()

# Step 2: Train model
model.fit(X, y)

# Step 3: Predict
prediction = model.predict([[5]])

print(prediction)
```

---

## Intermediate Example – Using Pandas with scikit-learn

```python
import pandas as pd
from sklearn.linear_model import LinearRegression

# Dataset
data = {
    "Hours": [1, 2, 3, 4, 5],
    "Score": [50, 55, 65, 70, 80]
}

df = pd.DataFrame(data)

X = df[["Hours"]]
y = df["Score"]

model = LinearRegression()
model.fit(X, y)

print(model.predict([[6]]))
```

---

## Advanced Insight – Why scikit-learn is Powerful

- Same API for all models
- Works with NumPy & Pandas
- Scalable to large datasets

This consistency allows easy switching between models like:

```python
LinearRegression()
KNeighborsClassifier()
DecisionTreeClassifier()
```

---

# 3. scikit-learn Workflow

Typical ML workflow:

```text
Data → Split → Train → Predict → Evaluate
```

---

## Basic Example – Linear Regression

```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()

model.fit(X_train, y_train)
predictions = model.predict(X_test)

print(predictions)
```

---

## Intermediate Example – Using Pandas Dataset

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression

# Sample dataset
data = {
    "Hours": [1, 2, 3, 4, 5],
    "Score": [50, 55, 65, 70, 80]
}

df = pd.DataFrame(data)

X = df[["Hours"]]
y = df["Score"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

model = LinearRegression()
model.fit(X_train, y_train)

pred = model.predict(X_test)
print(pred)
```

---

## Advanced Example – KNN Classifier

```python
from sklearn.neighbors import KNeighborsClassifier

X = [[1], [2], [3], [4]]
y = [0, 0, 1, 1]

model = KNeighborsClassifier(n_neighbors=3)
model.fit(X, y)

print(model.predict([[2.5]]))
```

---

# 3. Model Evaluation

After training a model, we must evaluate how well it performs.

Evaluation helps us answer:

- Is the model accurate?
- Where does it make mistakes?
- Can it generalize to new data?

---

## Basic Metric – Accuracy

Accuracy measures how many predictions are correct.

```python
from sklearn.metrics import accuracy_score

y_true = [1, 0, 1, 1]
y_pred = [1, 0, 0, 1]

print(accuracy_score(y_true, y_pred))
```

Formula:

```text
Accuracy = Correct Predictions / Total Predictions
```

---

## Limitation of Accuracy (Important Insight)

Accuracy can be misleading when data is imbalanced.

Example:

```text
If 95% data = class 0
Model predicts always 0 → Accuracy = 95%
```

But the model is actually useless.

---

## Confusion Matrix (Core Concept)

A confusion matrix shows how predictions compare with actual values.

For binary classification:

```text
                Predicted
              |  0   |  1
        -------------------
Actual   0   | TN   | FP
         1   | FN   | TP
```

Where:

- TP (True Positive): Model predicted **positive**, and the actual value is also **positive**
- TN (True Negative): Model predicted **negative**, and the actual value is also **negative**
- FP (False Positive): Model predicted **positive**, but the actual value is **negative** (also called *Type I error*)
- FN (False Negative): Model predicted **negative**, but the actual value is **positive** (also called *Type II error*)

---

## Intuitive Example (Very Important)

Consider a **spam email classifier**:

- Positive = Spam
- Negative = Not Spam

| Case | Actual | Predicted | Type |
|------|--------|-----------|------|
| Email is spam, predicted spam | Spam | Spam | TP |
| Email is not spam, predicted not spam | Not Spam | Not Spam | TN |
| Email is not spam, predicted spam | Not Spam | Spam | FP |
| Email is spam, predicted not spam | Spam | Not Spam | FN |

---

## Another Example – Medical Diagnosis

- Positive = Disease present
- Negative = No disease

| Case | Meaning | Type |
|------|--------|------|
| Sick patient correctly detected | Correct detection | TP |
| Healthy patient correctly identified | Correct rejection | TN |
| Healthy patient wrongly diagnosed as sick | False alarm | FP |
| Sick patient missed by model | Dangerous miss | FN |

---

## Key Insight for Students

- **FP (False Positive)** → Model raises a *false alarm*
- **FN (False Negative)** → Model *misses an important case*

In many real-world systems:

- Medical diagnosis → FN is very dangerous
- Spam detection → FP is annoying

Understanding this helps choose the right evaluation metric.


---

## Basic Example – Confusion Matrix

```python
from sklearn.metrics import confusion_matrix

y_true = [1, 0, 1, 1]
y_pred = [1, 0, 0, 1]

print(confusion_matrix(y_true, y_pred))
```

Output format:

```text
[[TN FP]
 [FN TP]]
```

---

## Intermediate Example – Understanding Errors

```python
from sklearn.metrics import confusion_matrix

cm = confusion_matrix(y_test, predictions)
print(cm)
```

Students should interpret:

- How many predictions are correct
- What type of errors are made (FP vs FN)

---

## Precision, Recall, and F1 Score

These metrics provide deeper insight than accuracy.

### Precision

```text
Precision = TP / (TP + FP)
```

Meaning:

> Out of all predicted positives, how many were correct?

---

### Recall

```text
Recall = TP / (TP + FN)
```

Meaning:

> Out of all actual positives, how many did we correctly identify?

---

### F1 Score

```text
F1 = 2 * (Precision * Recall) / (Precision + Recall)
```

Balances precision and recall.

---

## Advanced Example – Classification Report

```python
from sklearn.metrics import classification_report

print(classification_report(y_test, predictions))
```

This provides:

- Precision
- Recall
- F1-score
- Support (number of samples)

---

## When to Use Which Metric

- Accuracy → balanced datasets
- Precision → when false positives are costly
- Recall → when missing positives is dangerous
- F1-score → when both precision & recall matter

---

# 4. Complete ML Pipeline Example

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

# Dataset

data = {
    "Hours": [1,2,3,4,5,6,7,8],
    "Pass": [0,0,0,1,1,1,1,1]
}

df = pd.DataFrame(data)

X = df[["Hours"]]
y = df["Pass"]

# Split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25)

# Train
model = LogisticRegression()
model.fit(X_train, y_train)

# Predict
pred = model.predict(X_test)

# Evaluate
print("Accuracy:", accuracy_score(y_test, pred))
```

---

# 5. Common Mistakes

- Training and testing on same data
- Ignoring evaluation metrics
- Not scaling data (future topic)
- Using very small datasets

---

# 6. ChatGPT Prompts for Learning (Allowed Use)

---

## A. Understanding ML Workflow

- "Explain the machine learning pipeline step by step"
- "Why do we split data into train and test sets?"

---

## B. Debugging Models

- "Why is my model accuracy very low?"
- "Explain this scikit-learn code line by line"

---

## C. Evaluation Understanding

- "What is the difference between accuracy and precision?"
- "How does a confusion matrix work?"

---

## D. Conceptual Clarity

- "What is overfitting with a simple example?"
- "When should I use classification vs regression?"

---

# 7. Looking Ahead

You now have a complete understanding of:

- Data collection
- Data processing
- Model training
- Model evaluation

This forms the foundation of real-world AI systems.

---

**End of Week 08 Lecture**

