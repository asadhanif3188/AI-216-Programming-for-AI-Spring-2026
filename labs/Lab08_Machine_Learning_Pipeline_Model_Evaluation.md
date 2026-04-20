# AI-216 – Programming for Artificial Intelligence
## Lab 15: Machine Learning Pipeline & Model Evaluation

---

### Week #: 15  
### Topic: Training vs Testing, Model Evaluation & scikit-learn Workflow

---

## 1. Objective

The objective of this lab is to help students build a **complete machine learning pipeline** from data preparation to model evaluation.

Students will:

- Split data into training and testing sets
- Train multiple machine learning models
- Evaluate models using different metrics
- Compare model performance
- Understand real-world ML workflow

This lab is inspired by earlier scikit-learn practices fileciteturn7file0 but introduces **new datasets and structured tasks aligned with Week 15 lecture**.

---

## 2. Tools & Requirements

Required libraries:

- numpy
- pandas
- scikit-learn

Optional:

- matplotlib (for optional visualization)

---

# 3. Part A – Dataset Preparation

In this lab, you will work with a **real-world dataset** using scikit-learn.

Dataset: **Wine Classification Dataset** (built into scikit-learn)

This dataset is commonly used for multi-class classification:

- Features: chemical properties of wines (e.g., alcohol, malic acid, ash)
- Target: wine class (0, 1, 2)

---

### Task 1 – Load and Explore Dataset

```python
from sklearn.datasets import load_wine
import pandas as pd

wine = load_wine()
X = wine.data
y = wine.target
```

Tasks:

1. Convert dataset into a Pandas DataFrame
2. Assign feature names as column names
3. Add target column to DataFrame
4. Display first 5 rows
5. Print dataset shape
6. Inspect class distribution (value counts of target)

---

### Task 2 – Feature and Target Separation

1. Separate input features (X) and target variable (y)
2. Use all features for training
3. Print shapes of X and y

---

### Task 3 – Train-Test Split

1. Split dataset into training and testing sets
2. Use 25–30% data for testing
3. Use a fixed random_state

Focus Concepts:
- Generalization
- Reproducibility

1. Split dataset into training and testing sets
2. Use 25–30% data for testing
3. Use a fixed random_state

Focus Concepts:
- Generalization
- Reproducibility

---

# 4. Part B – Model Training

Train at least **two different classification models**.

---

### Task 3 – Logistic Regression Model

1. Train a Logistic Regression model
2. Predict results on test data
3. Store predictions

---

### Task 4 – KNN Classifier

1. Train a KNN model (choose k value yourself)
2. Predict results on test data
3. Compare predictions with Logistic Regression

Focus Concepts:
- Model comparison
- Different learning strategies

---

# 5. Part C – Model Evaluation

---

### Task 5 – Accuracy Evaluation

1. Compute accuracy for both models
2. Compare which model performs better

---

### Task 6 – Confusion Matrix Analysis

1. Compute confusion matrix for one model
2. Identify TP, TN, FP, FN from the result
3. Explain what type of errors the model makes

---

### Task 7 – Classification Report

1. Generate classification report
2. Analyze:
   - Precision
   - Recall
   - F1-score

Focus Concepts:
- Error analysis
- Metric interpretation

---

# 6. Part D – Model Improvement

---

### Task 8 – Feature Experimentation

1. Train the model using only one feature (Hours)
2. Train again using both features (Hours + Sleep)
3. Compare accuracy

---

### Task 9 – Changing Train-Test Ratio

1. Change test_size to 0.5
2. Retrain model
3. Observe impact on performance

Focus Concepts:
- Data impact on model
- Overfitting awareness

---

# 7. Part E – Mini ML Pipeline

Build a complete pipeline:

1. Load dataset
2. Split data
3. Train model
4. Predict
5. Evaluate

Your program should print:

- Model used
- Accuracy score
- Confusion matrix

---

# 8. Bonus Challenge (Optional)

Try using a third model (e.g., Decision Tree).

Compare all three models and identify:

- Which performs best
- Why performance differs

---

# 9. GitHub Submission

```text
AI-216-Programming-for-AI/
└── labs/
    └── week15/
        ├── lab15.py or .ipynb
        └── README.md
```

README must include:

- Explanation of models used
- Comparison of results
- One observation about model performance

---

# 10. Evaluation Criteria

| Criterion | Weight |
|----------|--------|
| Data preparation & splitting | 15% |
| Model implementation | 25% |
| Evaluation metrics usage | 25% |
| Analysis & comparison | 20% |
| Code clarity & documentation | 15% |

---

**End of Lab 15**

