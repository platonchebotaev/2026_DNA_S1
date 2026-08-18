# Automatic QSPR/QSAR report for Log_S1

Generated: 2026-05-10T06:58:57.784340

## 1. Data description

Dataset size: **100 molecules**.

Endpoint: **Log_S1**.

External test set Molecule_ID values:

`[50, 31, 65, 81, 8, 35, 49, 76, 18, 54, 92, 44, 66, 97, 20, 12, 27, 37, 59, 72]`

Train/internal set size: **80**  
External test set size: **20**

## 2. Descriptor list

Descriptor list source: `62_descriptors.txt`

Descriptors listed in TXT: **62**  
Descriptors found in Excel: **62**  
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

Descriptors after preprocessing and optional correlation/VIF settings: **62**.

## 6. Correlation and VIF diagnostics

Correlation filtering: **False**; cutoff = **0.95**.  
VIF filtering: **False**; cutoff = **10.0**.

High-correlation pairs with |r| > 0.95: **0**.  
High-VIF features with VIF > 10.0: **61**.

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

- **1. GaussianProcess__model_specific_best_subset__rank_top_20**: CV Q2 = 0.7095 ± 0.2520, CV RMSE = 0.0288, external R2 = 0.9010, external RMSE = 0.0287, CCC = 0.9409, features = 20, Y-rand p = 0.00332, outside AD fraction = 0.0600.
- **2. CatBoost__model_specific_best_subset__rank_top_20**: CV Q2 = 0.6951 ± 0.2185, CV RMSE = 0.0307, external R2 = 0.9416, external RMSE = 0.0221, CCC = 0.9647, features = 20, Y-rand p = 0.00332, outside AD fraction = 0.1200.
- **3. GradientBoosting__model_specific_best_subset__rank_top_20**: CV Q2 = 0.6385 ± 0.2823, CV RMSE = 0.0325, external R2 = 0.8945, external RMSE = 0.0296, CCC = 0.9345, features = 20, Y-rand p = 0.00332, outside AD fraction = 0.1800.

Best ranked model: **GaussianProcess__model_specific_best_subset__rank_top_20**

## 10. External validation

External validation metrics include R2_test, RMSE_test, MAE_test, CCC, Q2F1, Q2F2, Q2F3 and Golbraikh–Tropsha metrics.

## 11. Applicability domain

Classical leverage AD:

h* = 3(p+1)/n

Standardized residual threshold: |standardized residual| > 3.

- CatBoost__model_specific_best_subset__rank_top_20: outside AD = 12/100; outside leverage = 1; outside standardized residual = 12.
- GaussianProcess__model_specific_best_subset__rank_top_20: outside AD = 6/100; outside leverage = 1; outside standardized residual = 5.
- GradientBoosting__model_specific_best_subset__rank_top_20: outside AD = 18/100; outside leverage = 1; outside standardized residual = 18.

## 12. Robustness validation

Performed:

- repeated complex-only CV;
- Monte Carlo complex-only validation;
- bootstrap validation;
- nested CV for TOP 3 models;
- Y-randomization.

Y-randomization summary:

- CatBoost__model_specific_best_subset__rank_top_20: real Q2 = 0.6951; mean randomized Q2 = -0.8798; p-value = 0.00332.
- GaussianProcess__model_specific_best_subset__rank_top_20: real Q2 = 0.7095; mean randomized Q2 = -0.1672; p-value = 0.00332.
- GradientBoosting__model_specific_best_subset__rank_top_20: real Q2 = 0.6385; mean randomized Q2 = -1.1492; p-value = 0.00332.

## 13. Descriptor interpretation

Interpretability methods:

- permutation importance;
- SHAP where available;
- ALE plots;
- Spearman correlation and ALE trend direction.

- GaussianProcess__model_specific_best_subset__rank_top_20: top permutation descriptors: Se1Cu2Ag1s:(OEstate), Mor08u:(alvaDesc), Mor10s:(alvaDesc), Se1C2N2ss:(OEstate), RDF060e:(alvaDesc).
- CatBoost__model_specific_best_subset__rank_top_20: top permutation descriptors: nHM:(alvaDesc), J_Dz(p):(alvaDesc), GATS1i:(alvaDesc), ZM1Mad:(alvaDesc), Se1C2N2ss:(OEstate).
- GradientBoosting__model_specific_best_subset__rank_top_20: top permutation descriptors: GATS1i:(alvaDesc), J_Dz(p):(alvaDesc), Se1Cu2Ag1s:(OEstate), ZM1Mad:(alvaDesc), nHM:(alvaDesc).

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
