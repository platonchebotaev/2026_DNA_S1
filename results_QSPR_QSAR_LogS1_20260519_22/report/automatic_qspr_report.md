# Automatic QSPR/QSAR report for Log_S1

Generated: 2026-05-20T02:30:36.878616

## 1. Data description

Dataset size: **100 molecules**.

Endpoint: **Log_S1**.

External test set Molecule_ID values:

`[50, 31, 65, 81, 8, 35, 49, 76, 18, 54, 92, 44, 66, 97, 20, 12, 27, 37, 59, 72]`

Train/internal set size: **80**  
External test set size: **20**

## 2. Descriptor list

Descriptor list source: `62_descriptors_and_quantum.txt`

Descriptors listed in TXT: **73**  
Descriptors found in Excel: **73**  
Descriptors missing in Excel: **0**

Missing descriptors:

None

## 3. Manual molecule type assignment

- Molecule_ID 1–6: bimetal
- Molecule_ID 7: base, cytosine
- Molecule_ID 26: base, tyrosine_or_thymine
- Molecule_ID 45: base, adenine
- Molecule_ID 73: base, guanine
- all other molecules: complex

## 4. Train/test split

External test molecules were never used for preprocessing decisions, feature selection, hyperparameter optimization or internal CV.

Internal validation used complex-only validation folds. Bimetals and bases always remained in the training portion.

## 5. Preprocessing

Train-only preprocessing:

- inf replaced by NaN;
- descriptors with >50% NaN on train removed;
- train medians used for imputation;
- constant train descriptors removed.

Descriptors after preprocessing and optional correlation/VIF settings: **69**.

## 6. Correlation and VIF diagnostics

Correlation filtering: **True**; cutoff = **0.95**.  
VIF filtering: **False**; cutoff = **10.0**.

High-correlation pairs with |r| > 0.95: **5**.  
High-VIF features with VIF > 10.0: **69**.

Correlation and VIF were diagnostic by default because descriptors were already pre-filtered before GA feature selection.

## 7. Target distribution

Train target summary:

- min = 2.3625
- max = 2.8751
- mean = 2.5791
- std = 0.0763
- skewness = 0.4979

Because the endpoint is already Log_S1, no additional log-transform was applied by default.

## 8. Feature subset selection strategy

Candidate subsets included all cleaned GA-selected descriptors, LASSO subset, RFE subset, permutation subset, SHAP subset and aggregated-rank top N subsets.

Selector models used where available:

`['Ridge', 'SVR', 'ExtraTrees', 'RandomForest', 'CatBoost', 'XGBoost', 'LightGBM']`

Global robust subset: **rank_top_10**, n = **10**.

## 9. TOP 3 model ranking

Final ranking used preliminary model performance plus Y-randomization and applicability-domain diagnostics for robust candidates.

- **1. GaussianProcess__global_robust_subset__rank_top_10**: CV Q2 = 0.9102 ± 0.0563, CV RMSE = 0.0157, external R2 = 0.9780, external RMSE = 0.0135, CCC = 0.9890, features = 10, Y-rand p = 0.00332, outside AD fraction = 0.0200.
- **2. GaussianProcess__model_specific_best_subset__rank_top_8**: CV Q2 = 0.9098 ± 0.0611, CV RMSE = 0.0158, external R2 = 0.9832, external RMSE = 0.0118, CCC = 0.9913, features = 8, Y-rand p = 0.00332, outside AD fraction = 0.0300.
- **3. Ridge__model_specific_best_subset__rfe_subset**: CV Q2 = 0.8976 ± 0.1031, CV RMSE = 0.0153, external R2 = 0.9753, external RMSE = 0.0143, CCC = 0.9863, features = 20, Y-rand p = 0.00332, outside AD fraction = 0.0200.

Best ranked model: **GaussianProcess__global_robust_subset__rank_top_10**

## 10. External validation

External validation metrics include R2_test, RMSE_test, MAE_test, CCC, Q2F1, Q2F2, Q2F3 and Golbraikh–Tropsha metrics.

## 11. Applicability domain

Classical leverage AD:

h* = 3(p+1)/n

Standardized residual threshold: |standardized residual| > 3.

- GaussianProcess__global_robust_subset__rank_top_10: outside AD = 2/100; outside leverage = 2; outside standardized residual = 0.
- GaussianProcess__model_specific_best_subset__rank_top_8: outside AD = 3/100; outside leverage = 3; outside standardized residual = 0.
- Ridge__model_specific_best_subset__rfe_subset: outside AD = 2/100; outside leverage = 1; outside standardized residual = 1.

## 12. Robustness validation

Performed:

- repeated complex-only CV;
- Monte Carlo complex-only validation;
- bootstrap validation;
- nested CV for TOP 3 models;
- Y-randomization.

Y-randomization summary:

- GaussianProcess__global_robust_subset__rank_top_10: real Q2 = 0.9102; mean randomized Q2 = -0.1786; p-value = 0.00332.
- GaussianProcess__model_specific_best_subset__rank_top_8: real Q2 = 0.9098; mean randomized Q2 = -0.1976; p-value = 0.00332.
- Ridge__model_specific_best_subset__rfe_subset: real Q2 = 0.8976; mean randomized Q2 = -0.8702; p-value = 0.00332.

## 13. Descriptor interpretation

Interpretability methods:

- permutation importance;
- SHAP where available;
- ALE plots;
- Spearman correlation and ALE trend direction.

- GaussianProcess__global_robust_subset__rank_top_10: top permutation descriptors: Chemical_softness, ZM1Mad:(alvaDesc), Koopmans_IP, SsCu:(OEstate), QED:(alvaDesc).
- GaussianProcess__model_specific_best_subset__rank_top_8: top permutation descriptors: Chemical_softness, ZM1Mad:(alvaDesc), Koopmans_IP, SsCu:(OEstate), Koopmans_EA.
- Ridge__model_specific_best_subset__rfe_subset: top permutation descriptors: Chemical_softness, Koopmans_IP, QED:(alvaDesc), Koopmans_EA, ZM1Mad:(alvaDesc).

## 14. OECD validation principles

### 1. Defined endpoint

Endpoint is Log_S1.

### 2. Unambiguous algorithm

The workflow defines fixed preprocessing, feature subset generation, model optimization, validation, ranking and reporting procedures.

### 3. Defined applicability domain

Applicability domain is defined by leverage h and standardized residuals using Williams plots.

### 4. Goodness-of-fit, robustness and predictivity

The notebook reports R2_train, adjusted R2_train, repeated CV Q2, CV RMSE/MAE, external R2/RMSE/MAE, CCC, Q2F1/Q2F2/Q2F3, Golbraikh–Tropsha metrics, bootstrap, Monte Carlo, nested CV and Y-randomization.

### 5. Mechanistic interpretation where possible

Descriptor interpretation is based on permutation importance, SHAP, ALE trends and Spearman direction.

## 15. Limitations

The dataset is small; therefore repeated CV uncertainty, bootstrap uncertainty, applicability domain and Y-randomization should be interpreted together. R2_train alone is not sufficient. Descriptor interpretation is model-dependent.
