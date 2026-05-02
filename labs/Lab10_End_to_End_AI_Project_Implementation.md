# AI-216 – Programming for Artificial Intelligence
## Lab 10: End-to-End AI Project Implementation

### Week #: 17  
### Topic: End-to-End AI Systems & Deployment Mindset

## 1. Objective

The objective of this lab is to help students implement a **complete AI system using modular code structure**.

Students will:

- Organize code into multiple files
- Build a full ML pipeline
- Save and load models
- Simulate deployment through prediction functions

This lab emphasizes **real-world project structure and system thinking**.


## 2. Tools & Requirements

Required libraries:

- numpy
- pandas
- scikit-learn
- joblib


# 3. Project Structure

Students must follow this structure:

```text
project/
├── data/
├── preprocessing.py
├── train.py
├── evaluate.py
├── predict.py
└── main.py
```


# 4. Dataset

Use the **Wine Dataset** from scikit-learn.

```python
from sklearn.datasets import load_wine
```


# 5. Part A – Preprocessing Module

### Task 1

Create `preprocessing.py`:

Requirements:

1. Load dataset
2. Convert to Pandas DataFrame
3. Separate features (X) and target (y)
4. Return X and y


# 6. Part B – Training Module

### Task 2

Create `train.py`:

Requirements:

1. Split data into train/test sets
2. Train a model (choose any: Logistic Regression / KNN / Decision Tree)
3. Return:
   - trained model
   - X_test
   - y_test


# 7. Part C – Evaluation Module

### Task 3

Create `evaluate.py`:

Requirements:

1. Predict on test data
2. Print:
   - Accuracy
   - Confusion Matrix
   - Classification Report


# 8. Part D – Prediction Module

### Task 4

Create `predict.py`:

Requirements:

1. Save model using joblib
2. Load model from file
3. Create a function to predict a single sample


# 9. Part E – Main Execution File

### Task 5

Create `main.py`:

Requirements:

1. Call preprocessing function
2. Train model
3. Evaluate model
4. Save model
5. Load model again
6. Perform prediction on one sample


# 10. Part F – Experimentation

### Task 6

Modify your system:

1. Try a different model
2. Compare results
3. Observe changes in accuracy


# 11. Bonus Challenge (Optional)

- Add feature scaling using StandardScaler
- Save evaluation results to a text file


# 12. GitHub Submission

```text
AI-216-Programming-for-AI/
└── labs/
    └── week10/
        ├── preprocessing.py
        ├── train.py
        ├── evaluate.py
        ├── predict.py
        ├── main.py
        └── README.md
```

README must include:

- Project structure explanation
- Model used
- Evaluation results
- One improvement suggestion

**End of Lab 10**

