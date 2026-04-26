# AI-216: Programming for Artificial Intelligence
## Week 09 – Model Improvement, Cross-Validation & Hyperparameter Tuning

---

## Lecture Overview

In Week 08, you learned how to:

- Train machine learning models
- Evaluate model performance

Now we take the next critical step:

> **How do we improve a model after evaluating it?**

This lecture focuses on:

- Improving model performance
- Cross-validation for reliable evaluation
- Hyperparameter tuning

---

## Learning Objectives

After this lecture, students will be able to:

- Identify overfitting and underfitting
- Improve model performance using better strategies
- Apply cross-validation
- Perform basic hyperparameter tuning
- Compare multiple models effectively

---

# 1. Model Improvement: Why It Matters

After evaluation, models are rarely perfect.

Common problems:

- Low accuracy
- Overfitting
- Underfitting

Goal:

```text
Build a model that generalizes well to new data
```

---

# 2. Overfitting vs Underfitting

## Basic Understanding

- **Underfitting** → Model is too simple
- **Overfitting** → Model is too complex

---

## Example

```python
from sklearn.tree import DecisionTreeClassifier

model = DecisionTreeClassifier(max_depth=1)  # Underfitting
model = DecisionTreeClassifier(max_depth=10) # Potential overfitting
```

---

## Intermediate Example – Observing Behavior

```python
model = DecisionTreeClassifier(max_depth=2)
model.fit(X_train, y_train)

print("Train Accuracy:", model.score(X_train, y_train))
print("Test Accuracy:", model.score(X_test, y_test))
```

---

## Advanced Insight

| Scenario | Interpretation |
|--------|---------------|
| Low train, low test | Underfitting |
| High train, low test | Overfitting |
| High train, high test | Good model |

---

# 3. Improving Models (Practical Strategies)

---

## Basic Strategies (with Code)

### Example 1 – Using More Data (Conceptual)

```python
# Assume df is a larger dataset
X = df.drop("target", axis=1)
y = df["target"]

# More data generally improves generalization
```

---

### Example 2 – Feature Selection

```python
# Using only selected features
X_small = df[["feature1", "feature2"]]
X_full = df.drop("target", axis=1)

from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression

X_train, X_test, y_train, y_test = train_test_split(X_small, y, test_size=0.3)

model = LogisticRegression()
model.fit(X_train, y_train)

print("Accuracy (selected features):", model.score(X_test, y_test))
```

---

## Intermediate Strategies (with Code)

### Example 3 – Trying Different Models

```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.neighbors import KNeighborsClassifier

models = [
    DecisionTreeClassifier(),
    KNeighborsClassifier(n_neighbors=5)
]

for model in models:
    model.fit(X_train, y_train)
    print(type(model).__name__, model.score(X_test, y_test))
```

---

## Advanced Strategy – Feature Scaling (Important)

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

model = KNeighborsClassifier()
model.fit(X_train_scaled, y_train)

print("Accuracy after scaling:", model.score(X_test_scaled, y_test))
```

---

# 4. Cross-Validation

## Basic Example

```python
from sklearn.model_selection import cross_val_score
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(max_iter=1000)

scores = cross_val_score(model, X, y, cv=5)

print(scores)
```

---

## Intermediate Example – Comparing CV vs Train-Test

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3)

model.fit(X_train, y_train)

print("Train-Test Accuracy:", model.score(X_test, y_test))
print("Cross-Val Mean:", scores.mean())
```

---

## Advanced Example – Visualizing Stability

```python
import numpy as np

print("Mean Accuracy:", np.mean(scores))
print("Std Dev:", np.std(scores))
```

Interpretation:

- Low std → stable model
- High std → unstable model

---

# 6. Model Comparison

## Basic Example

```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.neighbors import KNeighborsClassifier
from sklearn.linear_model import LogisticRegression

models = {
    "Decision Tree": DecisionTreeClassifier(),
    "KNN": KNeighborsClassifier(),
    "Logistic Regression": LogisticRegression(max_iter=1000)
}

for name, model in models.items():
    model.fit(X_train, y_train)
    print(name, model.score(X_test, y_test))
```

---

## Intermediate Example – Using Cross-Validation for Comparison

```python
for name, model in models.items():
    scores = cross_val_score(model, X, y, cv=5)
    print(name, scores.mean())
```

---

## Advanced Example – Structured Comparison

```python
results = {}

for name, model in models.items():
    scores = cross_val_score(model, X, y, cv=5)
    results[name] = scores.mean()

for model_name, score in results.items():
    print(f"{model_name}: {score:.3f}")
```

This helps in selecting the best model systematically.

---

## Why Not Single Train-Test Split?

Single split can be unreliable:

```text
Model performance depends on how data is split
```

---

## K-Fold Cross-Validation

```text
Data split into K parts
Train on K-1 parts, test on 1
Repeat K times
Average results
```

---

## Basic Example

```python
from sklearn.model_selection import cross_val_score
from sklearn.linear_model import LogisticRegression

model = LogisticRegression()

scores = cross_val_score(model, X, y, cv=5)

print(scores)
```

---

## Intermediate Example

```python
print("Mean Accuracy:", scores.mean())
print("Standard Deviation:", scores.std())
```

---

## Advanced Insight

- High variance → unstable model
- Low variance → stable model

---

# 5. Hyperparameter Tuning

## What Are Hyperparameters?

Hyperparameters are settings we choose before training.

Examples:

- K in KNN
- Depth of decision tree

---

## Basic Example

```python
from sklearn.neighbors import KNeighborsClassifier

model = KNeighborsClassifier(n_neighbors=3)
```

---

## Intermediate Example – Trying Different Values

```python
for k in [3, 5, 7]:
    model = KNeighborsClassifier(n_neighbors=k)
    model.fit(X_train, y_train)
    print(k, model.score(X_test, y_test))
```

---

## Advanced Example – GridSearchCV

```python
from sklearn.model_selection import GridSearchCV
from sklearn.neighbors import KNeighborsClassifier

param_grid = {
    'n_neighbors': [3, 5, 7, 9]
}

model = KNeighborsClassifier()

grid = GridSearchCV(model, param_grid, cv=5)
grid.fit(X, y)

print(grid.best_params_)
print(grid.best_score_)
```

---

# 6. Model Comparison

Compare multiple models to select the best one.

---

## Example

```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.neighbors import KNeighborsClassifier

models = {
    "Decision Tree": DecisionTreeClassifier(),
    "KNN": KNeighborsClassifier()
}

for name, model in models.items():
    model.fit(X_train, y_train)
    print(name, model.score(X_test, y_test))
```

---

# 7. Complete Improved ML Pipeline

```python
# Step 1: Load data
# Step 2: Split data
# Step 3: Train model
# Step 4: Evaluate
# Step 5: Cross-validation
# Step 6: Hyperparameter tuning
# Step 7: Final model selection
```

---

# 8. ChatGPT Prompts for Learning (Allowed Use)

---

## A. Model Improvement

- "Why is my model overfitting?"
- "How can I improve model performance?"

---

## B. Cross-Validation

- "Explain cross-validation with example"
- "Why is cross-validation better than train-test split?"

---

## C. Hyperparameter Tuning

- "What are hyperparameters in machine learning?"
- "How does GridSearchCV work?"

---

## D. Debugging

- "Why are my results different every time?"
- "Explain this sklearn code step by step"

---

# 9. Looking Ahead

You now understand:

- Model building
- Model evaluation
- Model improvement

This completes the **full machine learning workflow**.

---
<!-- 
**End of Week 09 Lecture** -->

