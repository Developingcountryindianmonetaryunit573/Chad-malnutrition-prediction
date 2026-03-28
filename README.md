# 🍽️ Child Malnutrition Risk Prediction in Chad

[![Python](https://img.shields.io/badge/Python-3.8+-blue)](https://www.python.org/)
[![Data](https://img.shields.io/badge/Data-DHS%20Chad%202014-green)](https://dhsprogram.com/)
[![Models](https://img.shields.io/badge/Models-7%20Classifiers-orange)](https://scikit-learn.org/)
[![Best](https://img.shields.io/badge/Best%20Accuracy-Gradient%20Boosting%2092%25-success)]()
[![AUC](https://img.shields.io/badge/Best%20AUC-0.979-brightgreen)]()
[![Status](https://img.shields.io/badge/Status-Complete-brightgreen)]()

> **Over half of Chadian children under five are malnourished.**
> This project builds a machine learning pipeline to predict which
> children are at highest risk — using 9,826 children from the
> DHS Chad 2014 survey — enabling NGOs and health workers to
> intervene before malnutrition becomes acute or fatal.

---

## 🌐 Live Demo

👉 **[Try the app here](https://chad-malnutrition-app-tnkhzrgg9pbme32naw5cxg.streamlit.app)**

Enter a child's age, weight, and height to get an instant
malnutrition risk assessment — designed for community
health workers and NGO field teams in Chad.

---

## 🌍 Why This Matters

Chad has one of the highest child malnutrition rates in the world:

- **42.9%** of children under five are stunted
- **32.5%** are underweight
- **14.2%** are wasted — above the WHO emergency threshold
- **52.9%** suffer from some form of malnutrition

Yet most humanitarian responses are **reactive** — children are
identified only when they arrive at a health facility in crisis.
This project asks: **can we predict which children are at highest
risk before they become acutely malnourished?**

---

## 📊 Dataset

- **Source**: [DHS Program — Chad Standard DHS 2014](https://dhsprogram.com/)
- **File**: Children's Recode (KR) — 18,623 total children
- **Measured**: 9,826 children with anthropometric measurements
- **Target**: Any malnutrition (stunting OR underweight OR wasting)

### Malnutrition Definitions (WHO Standards)
| Indicator | Column | Threshold | Prevalence |
|-----------|--------|-----------|------------|
| Stunting | HW70 (HAZ) | Z-score < -2 | **42.9%** |
| Underweight | HW71 (WAZ) | Z-score < -2 | **32.5%** |
| Wasting | HW72 (WHZ) | Z-score < -2 | **14.2%** |
| Any malnutrition | Combined | Any above | **52.9%** |

---

## 🔬 Methodology
```
DHS Chad 2014 (18,623 children)
        ↓
Filter to measured children (9,826)
        ↓
Extract malnutrition Z-scores (HW70, HW71, HW72)
        ↓
Feature selection — 28 variables across 5 domains
        ↓
Remove redundant features (correlation analysis)
        ↓
Median imputation for missing values
        ↓
7 ML classifiers benchmarked
        ↓
5-Fold Stratified Cross-Validation
        ↓
Feature importance analysis
```

---

## 🛠️ Features Used (24 Variables)

| Domain | Features |
|--------|---------|
| Child anthropometrics | Age in months, Weight, Height |
| Mother health | BMI, Height, Education, Age |
| Birth history | Birth order, Preceding birth interval, Births in 5 years |
| Household | Wealth index, Size, Water source, Toilet, Electricity |
| Feeding practices | Breastfeeding duration, Weaning age |

---

## 🤖 Model Results

| Model | Accuracy | ROC-AUC |
|-------|----------|---------|
| **Gradient Boosting** | **92.0%** ✅ | **0.979** ✅ |
| XGBoost | 91.8% | 0.979 |
| CatBoost | 91.3% | 0.974 |
| Decision Tree | 85.1% | 0.919 |
| Logistic Regression | 80.4% | 0.886 |
| Random Forest | 79.2% | 0.889 |
| KNN | 67.2% | 0.732 |

All models evaluated using **5-Fold Stratified Cross-Validation**
on 9,826 children.

---

## 🔑 Key Findings

### 1. Over half of Chadian children are malnourished
52.9% of children under five in Chad suffer from stunting,
underweight, or wasting — making malnutrition the default
condition, not the exception.

### 2. Three measurements predict 95% of outcomes
Child age, weight, and height alone account for ~95% of the
model's predictive power. **A community health worker with
a scale and measuring tape can screen children effectively.**

### 3. Malnutrition compounds with age
Child age is the strongest predictor (importance: 0.421).
Stunting accumulates over time — early intervention before
age 2 is critical to prevent irreversible damage.

### 4. Intergenerational malnutrition is real
Mother's height predicts child stunting — malnourished
mothers raise malnourished children. Breaking this cycle
requires maternal nutrition programs, not just child feeding.

### 5. Wealth and sanitation matter less than expected
Water source, toilet type, and electricity show near-zero
predictive importance — suggesting that in Chad's context,
maternal and child anthropometrics are far stronger signals
than household infrastructure.

---

## 📌 Feature Importance (Top 10)

| Rank | Feature | Description | Importance |
|------|---------|-------------|------------|
| 1 | HW1 | Child age in months | 0.421 |
| 2 | HW2 | Child weight kg | 0.301 |
| 3 | HW3 | Child height cm | 0.229 |
| 4 | V438 | Mother height cm | 0.007 |
| 5 | V445 | Mother BMI | 0.006 |
| 6 | V191 | Wealth index score | 0.005 |
| 7 | V221 | Marriage to first birth interval | 0.004 |
| 8 | V133 | Mother education years | 0.004 |
| 9 | M7 | Duration of breastfeeding | 0.003 |
| 10 | B11 | Preceding birth interval | 0.003 |

---

## 🚀 How to Run
```bash
# Clone
git clone https://github.com/Derio001/chad-malnutrition-prediction
cd chad-malnutrition-prediction

# Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn
pip install xgboost catboost

# Run notebook
jupyter notebook Chad_Malnutrition_Prediction.ipynb
```

> **Note on data**: DHS data requires free registration at
> [dhsprogram.com](https://dhsprogram.com). Request Chad 2014
> KR recode dataset. The processed modeling dataset is included
> in this repo.

---

## 📁 Project Structure
```
chad-malnutrition-prediction/
│
├── Chad_Malnutrition_Prediction.ipynb    # Full pipeline
├── chad_malnutrition_model_data.csv      # Processed dataset
├── malnutrition_model_comparison.csv     # Model results
├── malnutrition_feature_importance.csv   # Feature rankings
└── README.md
```

---

## 🔭 Future Work

- [ ] Regional disaggregation — Sahel vs southern Chad
- [ ] Integrate with crop yield early warning system
- [ ] Add 2023 DHS data when available for Chad
- [ ] Build Streamlit dashboard for field worker use
- [ ] Extend to severe acute malnutrition (SAM) prediction
- [ ] Multi-country model (Niger, Mali, Sudan)

---

## 🏛️ Policy Implications

| Organization | Application |
|-------------|-------------|
| UNICEF Chad | Target child nutrition programs |
| WFP Chad | Link food security to malnutrition risk |
| MSF / Action Against Hunger | Field screening tool |
| Ministry of Health Chad | National nutrition surveillance |
| World Bank | Evidence base for nutrition investment |

---

## 👤 Author

**Mahamat Hanga Derio**
M.Tech Data Science — Christ University, Bangalore
Chadian national | Building ML tools for public health
and development in Sub-Saharan Africa

📬 Open to collaboration with UNICEF, WFP, WHO, NGOs
and research institutions working on child health in Chad
🔗 [GitHub](https://github.com/Derio001) |
[LRI Project](https://github.com/Derio001/lri-prediction-chad) |
[Crop Early Warning](https://github.com/Derio001/Chad-crop-yield-prediction) |
[GDP Dashboard](https://github.com/Derio001/exploratory-predictive-gdp-analysis)

---

*Part of an integrated data science portfolio focused on
child welfare, food security, and economic development
in Chad and the Lake Chad Basin.*
```

---

Now create the GitHub repo `chad-malnutrition-prediction`, upload the files, paste this README, and add topics:
```
machine-learning chad malnutrition child-health
dhs-data africa unicef public-health python
gradient-boosting xgboost
