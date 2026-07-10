# Credit Card Fraud Detection using HOBA Feature Engineering and Deep Learning

This project is a comprehensive replication and extension of the research paper:

> **"HOBA: A Novel Feature Engineering Methodology for Credit Card Fraud Detection with a Deep Learning Architecture"**  
> Zhang, Han, Xu & Wang (Information Sciences, 2021)

Instead of reproducing the results on the proprietary banking dataset used in the paper, we implemented the complete pipeline on the **IBM Synthetic Credit Card Transactions Dataset**, rebuilt the proposed feature engineering framework, trained multiple machine learning and deep learning models, and evaluated whether the paper's conclusions hold on an independent dataset.

---

## Project Objectives

The project aims to answer the following questions:

- Can **HOBA (Homogeneity-Oriented Behavior Analysis)** outperform the traditional **RFM (Recency-Frequency-Monetary)** feature engineering framework?
- Do deep learning models outperform traditional machine learning methods for fraud detection?
- Does the original paper's conclusion generalize to a completely different dataset?

---

## Background

Credit card fraud detection is an extremely challenging classification problem because:

- Fraudulent transactions are extremely rare (<1% of all transactions)
- The dataset is highly imbalanced
- False negatives are very costly
- Excessive false positives reduce customer satisfaction

Traditional fraud detection systems generally rely on the **RFM** framework:

- **Recency**
- **Frequency**
- **Monetary Value**

The original paper argues that RFM ignores the heterogeneous nature of transactions.

Instead, it proposes **HOBA (Homogeneity-Oriented Behavior Analysis)**, where transactions are analyzed only against other transactions sharing similar characteristics (merchant type, transaction type, location, etc.).

---

# Repository Structure

```text
.
├── data/
│   ├── raw/
│   ├── processed/
│
├── notebooks/
│   ├── 01_EDA.ipynb
│   ├── 02_Feature_Engineering.ipynb
│   ├── 03_Model_Training.ipynb
│
├── src/
│   ├── preprocessing.py
│   ├── feature_engineering.py
│   ├── models.py
│   ├── evaluation.py
│
├── figures/
│
├── results/
│
├── requirements.txt
│
└── README.md
```

---

## Dataset

We use the **IBM Synthetic Credit Card Transactions Dataset** available on Kaggle.

The dataset contains:

- **1,727,004 transactions**
- **11,693 fraudulent transactions**
- Fraud rate ≈ **0.68%**

The dataset includes attributes such as:

- Merchant Category Code (MCC)
- Transaction Amount
- Entry Mode
- Merchant Location
- Credit Limit
- Card Information
- Error Flags
- Timestamp

making it suitable for reproducing the HOBA methodology.

---

## Feature Engineering

### 1. RFM Features

We recreated the traditional RFM feature engineering pipeline consisting of:

- Recency
- Frequency
- Monetary statistics

**Total Features:** **65**

---

### 2. HOBA Features

Following the paper, we engineered behavioral features using four dimensions:

- Recency
- Frequency
- Monetary Value
- Location

The aggregation framework considers:

- Transaction characteristics
- Aggregation periods
- Aggregation statistics
- Behavioral measures

Additional rule-based features include:

- High-risk MCC
- Foreign transaction
- Online transaction
- Entry mode
- Error flags
- Geographic anomalies

**Total Features:** **891**

---

## Exploratory Data Analysis

Key findings from EDA:

- Online transactions exhibited significantly higher fraud rates than chip or swipe transactions.
- Fraudulent transactions generally involved larger monetary amounts.
- Merchant categories such as electronics, cruise lines, and jewelry showed elevated fraud risk.
- Transactions with recorded errors (CVV mismatch, bad PIN, insufficient balance) were much more likely to be fraudulent.
- High-risk MCC and foreign transaction indicators showed substantial fraud lift.

These observations validate the motivation behind HOBA's characteristic-based feature engineering.

---

## Models Implemented

### Traditional Machine Learning

- Logistic Regression
- Random Forest
- Support Vector Machine (SVM)

### Neural Networks

- Feedforward Neural Network (BPNN)

### Deep Learning

- Deep Belief Network (DBN)
- Convolutional Neural Network (CNN)
- Recurrent Neural Network (RNN)

---

## Evaluation Metrics

Because fraud detection is a highly imbalanced classification problem, we evaluated every model using:

- ROC-AUC
- Precision
- Recall
- F1 Score
- Recall @ 1% False Positive Rate
- Recall @ 3% False Positive Rate

These metrics better represent real-world fraud detection performance than accuracy.

---

## Experimental Pipeline

```text
Raw Dataset
      │
      ▼
Data Cleaning
      │
      ▼
Feature Engineering
 ├── RFM
 └── HOBA
      │
      ▼
Train/Test Split
      │
      ▼
Model Training
      │
      ▼
Hyperparameter Tuning
      │
      ▼
Performance Evaluation
      │
      ▼
Comparison with Original Paper
```

---

## Results

Our replication closely matches the conclusions reported in the original paper.

### Key Findings

-  Every model achieved higher AUC using HOBA features compared to RFM.
-  Deep learning consistently outperformed traditional machine learning methods.
-  HOBA produced the largest improvements under low False Positive Rate constraints.
-  Recall@1%FPR improved substantially across all models.
-  The paper's central claim generalized successfully to an independent public dataset.

---

## Comparison with Original Paper

| Aspect | Original Paper | Our Replication |
|---------|---------------|----------------|
| Dataset | Commercial Bank (China) | IBM Synthetic Dataset |
| Transactions | 114K | 1.72M |
| Fraud Rate | 1.5% | 0.68% |
| RFM Features | 87 | 65 |
| HOBA Features | 1410 | 891 |
| Models | RF, SVM, BPNN, DBN, CNN, RNN | Same |
| Conclusion | HOBA + Deep Learning performs best | Successfully reproduced |

---

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- TensorFlow / Keras
- Matplotlib
- Seaborn
- SciPy
- Jupyter Notebook

---

## Key Takeaways

- Feature engineering remains one of the most influential components in fraud detection.
- Behavior-aware features significantly outperform generic customer-level statistics.
- Deep neural architectures are capable of learning richer representations when supplied with informative behavioral features.
- HOBA is a robust methodology that generalizes beyond the proprietary dataset used in the original paper.

---

## References

- Zhang, X., Han, Y., Xu, W., & Wang, Q. (2021). *HOBA: A Novel Feature Engineering Methodology for Credit Card Fraud Detection with a Deep Learning Architecture.* Information Sciences, 557, 302–316.

