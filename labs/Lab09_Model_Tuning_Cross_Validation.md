# AI-216 – Programming for Artificial Intelligence
## Lab 16: Model Tuning & Cross-Validation



### Week #: 16  
### Topic: Model Improvement, Cross-Validation & Hyperparameter Tuning



## 1. Objective

The objective of this lab is to help students **improve machine learning models** using systematic techniques.

Students will:

- Apply cross-validation for reliable evaluation
- Perform hyperparameter tuning
- Compare multiple models
- Understand the impact of tuning on performance

This lab builds directly on Week 15 and Week 16 lectures, focusing on **model improvement and selection**.



## 2. Tools & Requirements

Required libraries:

- numpy
- pandas
- scikit-learn



# 3. Part A – Dataset Preparation

Use the **Wine Dataset** from scikit-learn.

```python
from sklearn.datasets import load_wine
import pandas as pd

wine = load_wine()
X = wine.data
y = wine.target
```



### Task 1 – Convert to DataFrame

1. Convert dataset into a Pandas DataFrame
2. Assign feature names
3. Add target column
4. Display basic information (`head`, `shape`)



### Task 2 – Train-Test Split

1. Split dataset into training and testing sets
2. Use 30% test data
3. Set random_state



# 4. Part B – Baseline Model



### Task 3 – Train Baseline Model

1. Train a Logistic Regression model
2. Evaluate using accuracy
3. Store baseline accuracy



# 5. Part C – Cross-Validation



### Task 4 – Apply Cross-Validation

1. Use 5-fold cross-validation
2. Print all scores
3. Compute mean accuracy



### Task 5 – Compare with Train-Test Split

1. Compare cross-validation mean with baseline accuracy
2. Comment on differences



# 6. Part D – Hyperparameter Tuning



### Task 6 – Manual Tuning (KNN)

1. Train KNN with different values of k (e.g., 3, 5, 7, 9)
2. Record accuracy for each value
3. Identify best k



### Task 7 – GridSearchCV

1. Use GridSearchCV on KNN
2. Define parameter grid for n_neighbors
3. Use 5-fold cross-validation
4. Print best parameters and best score



# 7. Part E – Model Comparison



### Task 8 – Compare Multiple Models

Train and compare:

- Logistic Regression
- KNN (best tuned version)
- Decision Tree

Requirements:

1. Use cross-validation for comparison
2. Store results in a dictionary
3. Print model performance



# 8. Part F – Final Model Selection



### Task 9 – Select Best Model

1. Identify best-performing model
2. Train it on full training data
3. Evaluate on test data



### Task 10 – Analysis

Answer the following:

- Which model performed best?
- Did tuning improve performance?
- Was cross-validation more reliable than single split?



# 9. Bonus Challenge (Optional)

- Apply feature scaling using StandardScaler
- Compare performance before and after scaling



# 10. GitHub Submission

```text
AI-216-Programming-for-AI/
└── labs/
    └── week09/
        ├── lab09.py or .ipynb
        └── README.md
```

README must include:

- Explanation of tuning process
- Comparison of models
- Final model selection reasoning



<!-- # 11. Evaluation Criteria

| Criterion | Weight |
|-|--|
| Cross-validation implementation | 20% |
| Hyperparameter tuning | 25% |
| Model comparison | 20% |
| Analysis & reasoning | 20% |
| Code clarity & structure | 15% |



**End of Lab 09**
 -->
