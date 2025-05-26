# Multi-Model Evaluation for Predicting Nottingham Prognostic Index (NPI) from Breast Cancer Gene Expression Profiles


---

## 📌 Project Overview

This project applies machine learning techniques to predict the Nottingham Prognostic Index (NPI)—a prognostic score used in breast cancer—from gene expression profiles. Our goal is to evaluate whether non-invasive gene expression data (e.g., from blood tests) can approximate traditional clinical scores that normally require surgical biopsy.

We compare **two dimensionality reduction methods** (PCA and LDA) and **three supervised learning models** (Logistic Regression, Decision Tree, and ResNet) using multiple evaluation metrics (Accuracy, Precision, Recall, F1 Score, and ROC-AUC).

---

## 🧠 Motivation

Breast cancer prognosis is currently determined using features like tumor size and grade, which are only measurable after surgery. The NPI is widely used for this purpose but requires histopathological data. This project explores whether NPI can be predicted using only gene expression data, enabling earlier, less invasive risk stratification.

---

## 📚 Related Work

- **Molecular Subtyping:** Past studies (e.g., Perou et al., Parker et al.) developed classifiers like PAM50 to define molecular subtypes of breast cancer using gene expression.
- **Prognostic Modeling:** Zhou et al. demonstrated nearly perfect NPI prediction using multi-omics and deep learning. Our work explores whether simpler, more interpretable models with only gene expression data can still be effective.

---

## 📂 Dataset

- **Source:** METABRIC dataset (~1980 patients)
- **Features:**  
  - 489 gene expression features  
  - 173 gene mutation features (excluded in final model)  
  - NPI score (continuous, converted to binary classes)
- **Target Classes:**  
  - **Low Risk:** NPI ≤ 3.4  
  - **High Risk:** NPI > 3.4

---

## ⚙️ Methods

### 🧹 Preprocessing

- Removed mutation features for simplicity.
- Standardized gene expression features.
- Converted NPI into binary classes using threshold of 3.4.

### 📉 Dimensionality Reduction

| Method | Description | Observations |
|--------|-------------|--------------|
| **PCA** | Unsupervised, variance-maximizing | Showed clustering but with class overlap |
| **LDA** | Supervised, class-separation maximizing | Found strong linear separability |

### 🤖 Models

| Model | Summary | Notes |
|-------|---------|-------|
| **Logistic Regression** | Fine-tuned with Grid Search, L1 regularization, feature selection | 71.9% accuracy, strong recall for high-risk class |
| **Decision Tree (LightGBM)** | Used all expression data, tuned extensively | 71.4% accuracy, strong precision/recall for high-risk |
| **ResNet** | Lightweight CNN for tabular data | Outperformed simpler models in recall and AUC |

---

## 📊 Results Summary

| Metric | Logistic Regression | Decision Tree | ResNet |
|--------|---------------------|---------------|--------|
| Accuracy | 71.9% | 71.4% | 72.97% |
| Precision | 77.0% | 79.0% | 77.99% |
| Recall | 82.2% | 78.0% | 82.61% |
| F1 Score | 79.5%| 79.0% | 80.23% |
| AUC-ROC | 75.5% | 74.0% | 72.89% |

- LDA provided valuable interpretability via gene importance (e.g., **GATA3**, **MMP11**, **COL12A1**), which aligned with known breast cancer biomarkers.

---

## 📁 Repository Structure

```bash
├── data/
│   └── METABRIC_RNA_Mutation.xlsx             # Raw input dataset
├── notebooks/
│   ├── logistic_regression_NPI_Final.ipynb
│   ├── decision_tree_NPI.ipynb
│   └── ResNet.ipynb
├── README.md
└── A Multi-Model Evaluation for Predicting Nottingham Prognostic Index from Breast Cancer Gene Expression Profiles.pdf                   # Final detailed report (includes methods, results, and figures)
