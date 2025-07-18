# Fetal Health Classification Using SVM & Decision Tree 🤰📊

---

## 📚 Table of Contents
- [Overview](#overview)
- [Key Contributions](#key-contributions)
- [Dataset](#dataset)
- [Data Preprocessing](#data-preprocessing)
- [Evaluation Strategy](#evaluation-strategy)
- [Models](#models)
- [Dimensionality Reduction & Feature Selection](#dimensionality-reduction--feature-selection)
- [Results](#results)
- [Discussion](#discussion)
- [Conclusion](#conclusion)

---

## Overview

This project builds and compares two classic classifiers—**Support Vector Machine (SVM)** and **Decision Tree (DT)**—to predict fetal health status (Normal, Suspect, Pathological) from Cardiotocogram (CTG) measurements. Careful handling of class imbalance and feature engineering maximizes detection of high‑risk cases.

---

## Key Contributions

- Balanced a 3‑class CTG dataset via manual oversampling to ensure equal representation.  
- Demonstrated the effect of feature scaling, hold‑out evaluation, and stratified splitting on model performance.  
- Benchmarked SVM vs. DT across accuracy and macro F1‑score, showing DT + RFE achieved the best results.  
- Explored dimensionality reduction (PCA, LDA) and feature selection (Correlation + RFE) to optimize model performance.

---

## Dataset

- **Source**: Kaggle “Fetal Health Classification” (2,126 CTG records).  
- **Classes (original counts)**:  
  - Normal: 1,655  
  - Suspect: 295  
  - Pathological: 176  

---

## Data Preprocessing

1. **Balancing**  
   - Duplicated minority‑class samples to match the Normal class count (1,655 each).  
2. **Scaling**  
   - Applied `StandardScaler` so all features have zero mean and unit variance.  
3. **Train/Test Split**  
   - 80/20 stratified hold‑out split to preserve class ratios.

---

## Evaluation Strategy

- **Hold‑Out Method** with stratification  
- **Metrics**:  
  - Overall Accuracy  
  - Macro F1‑Score (gives equal weight to each class)

---

## Models

| Model                | Key Settings                                       |
|----------------------|----------------------------------------------------|
| SVM                  | Linear kernel; `C` tuned via grid search           |
| Decision Tree (DT)   | Gini criterion; max depth tuned via cross‑validation |

---

## Dimensionality Reduction & Feature Selection

1. **PCA (95% Variance)**  
   - Reduced 21 features → 14 components; slight drop in accuracy.  
2. **LDA (2 Components)**  
   - Reduced to 2 dimensions; further drop in accuracy.  
3. **Correlation + RFE**  
   - Filtered out low‑correlation features, then applied Recursive Feature Elimination to pick the top 10.  
   - **Best performance**:  
     - DT + RFE → **91.5% accuracy**  
     - SVM + RFE → **89.4% accuracy**

---

## Results

| Configuration           | Accuracy | Macro F1‑Score |
|-------------------------|----------|----------------|
| SVM (raw features)      | 88.0%    | 0.805          |
| DT (raw features)       | 89.7%    | 0.812          |
| SVM + PCA               | 87.1%    | 0.79           |
| DT + PCA                | 87.2%    | 0.79           |
| SVM + LDA               | 83.6%    | 0.75           |
| DT + LDA                | 86.6%    | 0.80           |
| SVM + Correlation + RFE | 89.4%    | 0.82           |
| **DT + Correlation + RFE** | **91.5%** | **0.84**     |

---

## Discussion

- **Feature selection** (Correlation + RFE) outperformed dimensionality reduction, highlighting the importance of retaining informative variables rather than compressing them.  
- **Decision Tree** proved more balanced on minority classes than SVM, especially after RFE.  
- PCA and LDA helped visualization but removed discriminative power for this multiclass problem.

---

## Conclusion

Balancing the dataset, scaling features, and strategically selecting the most relevant CTG measurements enables a simple Decision Tree to reach **91.5% accuracy** in fetal health classification—providing a lightweight, interpretable model for early risk detection.
