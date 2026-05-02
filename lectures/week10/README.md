# AI-216: Programming for Artificial Intelligence
## Week 10 – End-to-End AI Project & Deployment Mindset

---

## Lecture Overview

So far, you have learned how to:

- Work with data (NumPy, Pandas)
- Train machine learning models
- Evaluate and improve models

Now, we take the final step:

> **How do we turn a machine learning model into a real AI solution?**

This lecture focuses on building a **complete AI system mindset**.

---

## Learning Objectives

After this lecture, students will be able to:

- Understand the full AI project lifecycle
- Structure a complete AI project
- Save and reuse trained models
- Understand basic deployment concepts
- Identify real-world challenges in AI systems

---

# 1. End-to-End AI Workflow

A real AI system is more than just a model.

## Complete Pipeline

```text
Problem → Data → Cleaning → Feature Engineering → Model → Evaluation → Improvement → Deployment
```

---

## Basic Example – Student Performance Prediction

Problem:

> Predict whether a student will pass based on study hours and sleep.

---

## Implementation (Basic Pipeline)

```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression

# Data
X = [[2,7], [3,6], [5,5], [7,4]]
y = [0, 0, 1, 1]

# Split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3)

# Model
model = LogisticRegression()
model.fit(X_train, y_train)

# Predict
print(model.predict([[6,5]]))
```

---

# 2. Structuring an AI Project

Real projects are organized into modules.

## Suggested Structure

```text
project/
├── data/
├── preprocessing.py
├── train.py
├── evaluate.py
├── predict.py
└── main.py
```

---

## Intermediate Example – Modular Code

### preprocessing.py

```python
def preprocess(data):
    # clean and prepare data
    return data
```

### train.py

```python
from sklearn.linear_model import LogisticRegression

def train_model(X, y):
    model = LogisticRegression()
    model.fit(X, y)
    return model
```

---

## Advanced Insight

Benefits of modular design:

- Reusability
- Maintainability
- Scalability

---

# 3. Saving and Loading Models

## Why Save Models?

- Avoid retraining every time
- Use model in applications

---

## Basic Example

```python
import joblib

# Save model
joblib.dump(model, "model.pkl")

# Load model
model = joblib.load("model.pkl")
```

---

## Intermediate Example – Using Saved Model

```python
model = joblib.load("model.pkl")

prediction = model.predict([[6,5]])
print(prediction)
```

---

# 4. Deployment Mindset (Intro)

## What is Deployment?

Deployment means making the model available for real-world use.

---

## Simple Deployment Simulation

```python
def predict_pass(hours, sleep):
    model = joblib.load("model.pkl")
    return model.predict([[hours, sleep]])

print(predict_pass(6,5))
```

---

## Real-World Examples

- Spam detection in email systems
- Recommendation systems
- Fraud detection

---

# 5. Common Challenges in Real AI Systems

---

## Data Issues

- Missing values
- Noisy data
- Changing data (data drift)

---

## Model Issues

- Overfitting in production
- Performance degradation

---

## System Issues

- Slow predictions
- Scaling problems

---

# 6. Complete End-to-End Project (File-Based Structure)

In real-world AI systems, code is organized across multiple files. Below is a simplified but realistic project structure:

```text
project/
├── data/
├── preprocessing.py
├── train.py
├── evaluate.py
├── predict.py
└── main.py
```

---

## Step 1: preprocessing.py

```python
import pandas as pd
from sklearn.datasets import load_wine


def load_and_preprocess():
    wine = load_wine()
    X = pd.DataFrame(wine.data, columns=wine.feature_names)
    y = wine.target
    return X, y
```

---

## Step 2: train.py

```python
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier


def train_model(X, y):
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

    model = KNeighborsClassifier(n_neighbors=5)
    model.fit(X_train, y_train)

    return model, X_test, y_test
```

---

## Step 3: evaluate.py

```python
from sklearn.metrics import accuracy_score, classification_report


def evaluate_model(model, X_test, y_test):
    predictions = model.predict(X_test)

    print("Accuracy:", accuracy_score(y_test, predictions))
    print(classification_report(y_test, predictions))
```

---

## Step 4: predict.py

```python
import joblib


def save_model(model):
    joblib.dump(model, "model.pkl")


def load_model():
    return joblib.load("model.pkl")


def predict_sample(model, sample):
    return model.predict([sample])
```

---

## Step 5: main.py

```python
from preprocessing import load_and_preprocess
from train import train_model
from evaluate import evaluate_model
from predict import save_model, load_model, predict_sample

# Load data
X, y = load_and_preprocess()

# Train model
model, X_test, y_test = train_model(X, y)

# Evaluate model
evaluate_model(model, X_test, y_test)

# Save model
save_model(model)

# Load and test prediction
loaded_model = load_model()
print(predict_sample(loaded_model, X_test.iloc[0]))
```

---

## Key Learning Outcome

Students should understand:

- How ML code is split across modules
- How data flows between files
- How a complete AI system is built and executed

---

# 7. ChatGPT Prompts for Learning (Allowed Use)

---

## A. Project Understanding

- "Explain end-to-end machine learning pipeline"
- "How do I structure a machine learning project in Python?"

---

## B. Model Saving & Deployment

- "How to save and load models using joblib?"
- "Explain model deployment in simple terms"

---

## C. Debugging

- "Why is my saved model not working?"
- "Explain this ML pipeline step by step"

---

## D. Conceptual Thinking

- "What problems occur when deploying ML models?"

---

# 8. Final Takeaway

You can now:

- Build machine learning models
- Evaluate and improve them
- Structure AI projects
- Think about real-world deployment

---

## Course Completion Insight

```text
Data → Model → Evaluation → Improvement → Deployment
```

This is the **complete AI workflow**.

---

**End of Week 10 Lecture**

