# DNA QSPR/QSAR Log_S1

This repository contains the data, preprocessing steps, and main workflow used to build QSPR/QSAR models for predicting `Log_S1` in bimetallic nanoclusters, DNA bases, and their complexes.

## Main files

- `S1_preprocessing.ipynb` — preprocessing of the initial data and preparation of molecular descriptors.
- `qspr_qsar_logS1_notebook_7_07_2026.ipynb` — main notebook for feature selection, model training, validation, and interpretation.
- `Log_s1.xlsx` — target variable values (`Log_S1`).
- `All_descriptors.xlsx` — initial molecular descriptors.
- `All_descriptors_combined.xlsx` — combined table of the initial descriptors.
- `All_molecules_noncorelated_descriptors_and_y_quantum.xlsx` — main dataset for final modeling, containing selected molecular and quantum-chemical descriptors together with `Log_S1`.
- `62_descriptors.txt` — list of descriptors selected after GA/frequency-based screening.
- `62_descriptors_and_quantum.txt` — list of selected descriptors with added quantum-chemical features.
- `test_molecules.csv` — molecule IDs included in the external test set.

## Folders

- `Chunk_for_GA/` — input files for GA-MLR descriptor selection.
- `GA_answer/` — results of the GA-MLR analysis.
- `results_QSPR_QSAR_LogS1_20260519_22/` — results of the workflow without VIF filtering.
- `results_QSPR_QSAR_LogS1_20260702_13/` — results of the workflow with VIF filtering.

The `results_*` folders contain:

- trained models;
- metric tables;
- selected descriptors;
- cross-validation and Y-randomization results;
- applicability domain analysis;
- SHAP, permutation importance, and ALE results;
- figures;
- automatic report;
- `summary_tables.xlsx`;
- `run_metadata_final.json`.

## Repository structure

```text
.
├── README.md
├── S1_preprocessing.ipynb
├── qspr_qsar_logS1_notebook_7_07_2026.ipynb
│
├── Log_s1.xlsx
├── All_descriptors.xlsx
├── All_descriptors_combined.xlsx
├── All_molecules_noncorelated_descriptors_and_y_quantum.xlsx
│
├── 62_descriptors.txt
├── 62_descriptors_and_quantum.txt
├── test_molecules.csv
│
├── Chunk_for_GA/
├── GA_answer/
│
├── results_QSPR_QSAR_LogS1_20260519_22/
└── results_QSPR_QSAR_LogS1_20260702_13/
```
