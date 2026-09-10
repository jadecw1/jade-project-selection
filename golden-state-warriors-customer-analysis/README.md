# Golden State Warriors Customer Analysis

**DAEN 400 Case Study 2 — Texas A&M University**  
**Author:** Jade Winebright  
**Fall 2025**

## Project Overview

This case study analyzes a Golden State Warriors ticket-marketing problem: how customer data can be used to predict **when fans are likely to purchase tickets** so promotional outreach can be timed more effectively.

The analysis addresses two predictive tasks:

1. **Fan-type classification** — classify customers as Last-Minute, Planner, or In-Between purchasers.
2. **Purchase-timing regression** — estimate the number of days before a game that a customer is likely to purchase.

The workflow combines exploratory data analysis, feature selection, classification, regression, model comparison, cross-validation, and hyperparameter tuning.

## Methods

The analysis evaluates several machine-learning approaches:

- K-Nearest Neighbors (KNN)
- Logistic Regression
- Random Forest Classification
- Random Forest Regression
- Grid-search hyperparameter tuning with k-fold cross-validation

Customer features include age, mailing-list status, number of tickets purchased, seat location, ticket price, and concession purchases.

## Key Results

### Fan-Type Classification

| Model | Validation Accuracy |
|---|---:|
| KNN | 0.8133 |
| Logistic Regression | 0.79 |
| Random Forest | **0.82** |

All three classifiers correctly predicted the five held-out test observations. Random Forest was selected based on its validation performance and prediction confidence.

### Purchase-Timing Regression

The tuned Random Forest Regressor improved prediction error compared with the provided linear-regression baselines:

| Model | Mean Squared Error |
|---|---:|
| Simple Linear Regression | 79.5456 |
| Multiple Linear Regression | 20.0589 |
| Random Forest Regression | **11.1764** |

The written report also reports a Random Forest regression validation R² of **0.610** and test R² of **0.901**.

## Business Takeaway

The analysis suggests using Random Forest models to support customer segmentation and purchase-timing predictions. These predictions could help target promotional emails closer to the periods when individual customers are most likely to buy, while reducing unnecessary outreach.

## Repository Structure

```text
golden-state-warriors-customer-analysis/
├── README.md
├── requirements.txt
├── code/
│   └── customer_purchase_timing_analysis.ipynb
├── report/
│   └── Case_Study_2_Report.pdf
└── presentation/
    └── Case_Study_2_Presentation.pdf
```


## Limitations

The provided dataset contains 1,000 customer observations, and the held-out test set contains only five observations. The project therefore emphasizes comparison of model behavior and validation performance rather than treating the small test-set results as evidence of broad real-world generalization.

Additional data across more games and customers, along with game-specific and pre-purchase features, would strengthen future modeling.
