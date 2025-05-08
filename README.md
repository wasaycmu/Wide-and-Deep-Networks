# Wide-and-Deep-Networks

# 🍄 Mushroom Classification - Poisonous vs Edible

## 🧠 Techniques Used
- One-Hot Encoding
- Feature Engineering (Cross Features)
- Dimensionality Reduction (via feature elimination)
- Data Scaling and Preprocessing
- Stratified K-Fold Cross-Validation
- Wide and Deep Neural Networks (Keras)
- Multi-Layer Perceptron (MLP) Comparison
- ROC-AUC, Recall as Evaluation Metrics
- Statistical Analysis (McNemar Test)

---

## 📊 Project Overview

This project classifies mushrooms as **poisonous or edible** using a dataset from [Kaggle](https://www.kaggle.com/datasets/uciml/mushroom-classification/data). Each sample is described using categorical features related to the mushroom's physical attributes.

---

## 🧹 Data Preparation

### ✅ Preprocessing Steps
- Converted all categorical variables using **One-Hot Encoding**
- Removed redundant or irrelevant variables
- Checked for missing values — none found
- Normalized where needed (optional in one-hot scenario)

### 🧾 Final Dataset Summary
- **Target Column**: `class` (poisonous = `p`, edible = `e`)
- **Rows**: 8123
- **Missing Values**: None
- **All features** are one-hot encoded from the original categorical variables

---

## 🔗 Crossed Features

To capture interactions between correlated features, we created cross-product terms for:

1. **Cap Features**: `cap-shape`, `cap-surface`, `cap-color`
2. **Stalk Features**: `stalk-shape`, `stalk-root`, `stalk-surface-above-ring`, `stalk-surface-below-ring`, `stalk-color-above-ring`, `stalk-color-below-ring`
3. **Veil Features**: `veil-type`, `veil-color`
4. **Ring Features**: `ring-number`, `ring-type`

### ❌ Uncrossed Features:
`odor`, `gill-color`, `spore-print-color`, `habitat`, `population` — these features provide stand-alone value and are not meaningfully combinable.

---

## 🎯 Evaluation Metrics

Given the **critical risk** of false negatives (i.e., predicting a poisonous mushroom as edible), the following metrics are used:

- **Recall**: Prioritizes minimizing false negatives
- **ROC-AUC**: Measures tradeoff between true positive and false positive rates

These metrics are suitable for high-risk classification scenarios like food safety.

---

## 🧪 Data Splitting Strategy

We used **Stratified K-Fold Cross-Validation** to:
- Preserve class balance across folds
- Ensure rare categorical feature combinations are represented
- Get a more generalizable performance estimate

---

## 🧠 Model Architectures

### 1. **Wide and Deep Network (2-layer deep branch)**
- **Performance**: Excellent; reaches near-perfect recall, AUC in 4 epochs
- **Optimal Model**

### 2. **Wide and Deep Network (3-layer deep branch)**
- **Slightly worse loss**, similar accuracy and recall
- **Faster AUC convergence**, but not significantly better overall

### 3. **MLP (No wide branch)**
- **Matched performance** with Wide + Deep
- **Simpler architecture**, faster training
- **McNemar test**: No significant difference vs wide & deep

---

## 📈 Visualizations

- Loss vs Epoch
- Accuracy vs Epoch
- Recall vs Epoch
- ROC-AUC vs Epoch

(*All plots demonstrate rapid convergence, usually by epoch 3–4*)

---

## 🔬 Statistical Comparison

- **McNemar's Test** confirms:
  - No significant difference between MLP and wide + deep models
  - **MLP alone suffices** for this dataset

---

## ✅ Conclusion

- **Best Model**: Wide and Deep Network with 2-layer deep branch
- **MLP Alternative**: Equally effective, simpler to train
- **Recommendation**: Use MLP unless you're specifically evaluating wide+deep architectures

---

## 💡 Real-World Application

A food production line can benefit immensely from this model:
- Automatically classify mushrooms via computer vision + this model
- Prevent poisonous items from reaching the supply chain
- Integrate a two-stage detection process: high-recall pre-filter followed by stricter secondary validation

---

## 📁 Dataset Reference

[Mushroom Classification Dataset on Kaggle](https://www.kaggle.com/datasets/uciml/mushroom-classification/data)

