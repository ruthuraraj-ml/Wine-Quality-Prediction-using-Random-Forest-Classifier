# 🍷 Wine Quality Prediction — Random Forest Classifier

This project builds a **Random Forest Classifier** to predict the quality of Portuguese red and white wines using their physicochemical characteristics.  
The study includes full EDA, feature engineering, model training, cross-validation, feature importance analysis, and multi-class evaluation.

---

## 📌 Project Objective
The objective is to predict wine quality scores (3–8) based on measurable chemical attributes:

- Acidity levels  
- Sulfur dioxide content  
- Residual sugar  
- pH  
- Sulphates  
- Alcohol percentage  
- Wine type (red / white)

Random Forest is chosen because it handles nonlinear relationships, is robust to outliers, and provides interpretable feature-importance measures.

---

## 📁 Dataset Details

- **Source:** Kaggle Wine Quality Dataset  
- **Total Samples:** 6,497 (1,599 red + 4,898 white)  
- **Features:** 12 chemical features + 1 categorical feature (`type`)  
- **Target:** `quality` (integer 3–8)

### Key Preprocessing Notes
- Very few missing values → dropped because <1% impact  
- Removed **free sulfur dioxide** due to strong correlation with total sulfur dioxide  
- Encoded wine type (0 = red, 1 = white)  
- Outliers retained (chemically valid)  
- No scaling needed (tree-based model is scale-invariant)  
- Stratified train–test split (80/20)

---

## 🔍 Exploratory Data Analysis — Summary

### **Target Distribution**
- Most wines fall in quality categories **5, 6, and 7**  
- Classes 3, 4, and 8 are rare → classification imbalance

### **Feature Distributions**
- Many chemical features are right-skewed  
- Alcohol and pH show tighter distributions  
- Residual sugar and sulfur variables have long tails  

### **Important EDA Insights**
- Higher **alcohol** generally → higher quality  
- Higher **volatile acidity** → lower quality  
- Higher **sulphates** moderately improve quality  
- **Density** and **chlorides** negatively correlate with quality  
- **White wines** outnumber red wines (~75%)

---

## 🧠 Feature Engineering

### Final Features Used:

### Why remove free sulfur dioxide?
- Strong correlation with total sulfur dioxide → redundant → removed

### Handling Class Imbalance
- Stratified sampling  
- Macro metrics used for fair evaluation  

---

## 🧪 Model Summary

### Algorithm:
- **RandomForestClassifier**  
- `n_estimators=200`, `max_depth=None`, `random_state=12`

### Why Random Forest?
- Handles non-linear boundaries  
- Resistant to outliers  
- Good for multi-class problems  
- Provides feature importances  

### Training Outcome:
- Train accuracy ≈ 0.69  
- Test accuracy ≈ 0.69  
- 5-fold CV accuracy ≈ 0.68  
- Model generalizes well with no overfitting

---

## 🎯 Model Performance

| Metric | Value |
|--------|--------|
| Accuracy | 0.69 |
| Balanced Accuracy | 0.69 |
| Macro Precision | 0.59 |
| Macro Recall | 0.42 |
| Weighted F1 | 0.68 |
| ROC-AUC (Macro) | 0.82 |
| PR-AUC (Macro) | 0.50 |

### Interpretation:
- Good performance for dominant classes (5, 6, 7)  
- Underperforms for rare classes (3, 4, 8)  
- Strong ranking capability despite moderate accuracy  
- Learning curve suggests more data would help

---

## ⭐ Feature Importance

### Top Predictors
1. **Alcohol** (strongest indicator of quality)  
2. **Volatile acidity**  
3. **Density**  
4. **Chlorides**  
5. **Sulphates**  
6. Others contribute moderately

### Permutation Importance validates:
- Shuffling alcohol causes largest drop in accuracy  
- Quality depends on **multiple interacting factors**, not a single variable

---

## 💡 Key Insights
- Alcohol strongly predicts higher quality  
- Volatile acidity worsens wine quality  
- Density and chlorides negatively impact ratings  
- Mid-range wines (5–7) are easiest to classify  
- Outlier wines (3, 4, 8) require more data for improvement  

---

## 📦 Summary Table

| Aspect | Value |
|--------|--------|
| Model | Random Forest Classifier |
| Accuracy | 0.69 |
| Balanced Accuracy | 0.6875 |
| ROC-AUC | 0.82 |
| Important Features | Alcohol, Volatile Acidity, Density |
| Dataset Size | 6,497 samples |
| Task | Multi-class classification (3–8) |

---

## 🧱 Tech Stack
- Python  
- NumPy, Pandas  
- Matplotlib, Seaborn  
- Scikit-learn  
- Jupyter / Google Colab  
