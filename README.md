# Gender-Aware Cardiovascular Disease Prediction

Research project (Forschungspraktikum) for the M.Sc. Web and Data Science at the
University of Koblenz, supervised by Prof. Dr. Andreas Mauthe and Christopher Latz, M.Sc.

## Overview

Women often present with different symptoms and risk profiles than men, yet most
clinical datasets and prediction models are dominated by male patients. This project
detects, quantifies and mitigates the resulting gender bias in machine-learning
models for heart disease prediction.

## Dataset

- **Heart Failure Prediction Dataset** (Kaggle, by fedesoriano, 2021), a combination
  of five public heart-disease datasets (including UCI) with duplicates removed
- 918 patients, 11 clinical features, binary target `HeartDisease`
- Strong imbalance in the sensitive attribute: 725 male (79%) vs. 193 female (21%)
- Features: Age, Sex, ChestPainType, RestingBP, Cholesterol, FastingBS, RestingECG,
  MaxHR, ExerciseAngina, Oldpeak, ST_Slope

## Approach

1. **Pre-processing**: cleaning, outlier handling (Winsorization), feature
   transformation and encoding
2. **Baseline models**: Logistic Regression, Random Forest, Decision Tree and others
   (80/20 train-test split), evaluated with recall and fairness metrics
   (equal-opportunity gap, TPR/FPR gap, demographic parity)
3. **Bias detection**: univariate, bivariate and group-disparity EDA, correlation
   analysis, and gender-stratified feature importance (mutual information, Cramér's V,
   chi-square)
4. **Bias mitigation**
   - Random oversampling
   - SMOTE (female subgroup only)
   - Fairness-aware reweighting
   - Fairlearn Exponentiated Gradient (Demographic Parity and Equalized Odds)
   - AIF360-style reweighing
   - Female-specific models (full, 3-feature metabolic, 4-feature)
5. **Evaluation**: comparison of recall, accuracy and fairness gaps before and after
   each strategy

## Key Results

- Baseline Logistic Regression: female recall **0.50** vs. male recall **0.92**
  (equal-opportunity gap 0.42)
- Most predictive features differ between men and women, so a single pooled feature
  set favors the majority group
- SMOTE (female only): female recall 0.50 → **0.83**, gap reduced to 0.08
- Fairness-aware reweighting: female recall 0.50 → **0.83**, gap reduced to **0.03**
- Female-specific 4-feature models: female recall up to **0.89** (LR) and
  **0.91** (RF), gaps 0.03-0.08
- Effectiveness is **model-dependent**. For example, Equalized Odds helped Logistic
  Regression but not Random Forest, and Demographic Parity risked overcompensation.

## Tech Stack

Python, Pandas, NumPy, Scikit-learn, imbalanced-learn (SMOTE), Fairlearn, AIF360,
Matplotlib, Seaborn

## Disclaimer

Academic research only. Not intended for clinical use or medical decision-making.
