# Remaining Useful Life Estimation for Industry 4.0 Digital Twins  
**MSc Dissertation – Comparative Evaluation of LSTM, 1D-CNN and Hybrid CNN-LSTM Architectures on NASA C-MAPSS**

This repository contains the complete experimental pipeline used in the dissertation.  
It implements a statistically audited comparison of four deep learning architectures for Remaining Useful Life (RUL) prediction under both stationary (FD001) and multi-regime (FD002) operating conditions.

---

## Research Overview

The study evaluates:

- **Baseline LSTM** (single-layer)
- **Stacked LSTM** (two-layer)
- **1D-CNN**
- **Hybrid CNN-LSTM**

All models were trained under identical conditions:

- Engine-isolated train/validation splits (prevents data leakage)
- Piecewise-linear RUL target (capped at 125 cycles)
- Multi-seed training (10 independent random seeds)
- Evaluation using RMSE, MAE and the NASA asymmetric scoring function \(S\)
- Formal inferential testing (paired *t*-test and Wilcoxon signed-rank test)

---

## Repository Structure

```text
├── notebooks/
│   ├── 01_data_exploration.ipynb          # Exploratory analysis of C-MAPSS
│   ├── 02_preprocessing_unified.ipynb     # Final preprocessing pipeline
│   ├── 03G_baseline_lstm.ipynb            # Multi-seed Baseline LSTM
│   ├── 03G_improved_lstm.ipynb            # Multi-seed Stacked LSTM
│   ├── 04G_cnn.ipynb                      # Multi-seed 1D-CNN
│   ├── 05G_cnn_lstm.ipynb                 # Multi-seed Hybrid CNN-LSTM
│   ├── 07_statistical_tests.ipynb         # Inferential statistical tests
│   └── 08_appendix_figures.ipynb          # Generation of all thesis figures
│
├── data/
│   └── raw/                               # Place C-MAPSS .txt files here
│
├── results/                               # Generated metrics, histories & predictions
│   ├── metrics/
│   ├── histories/
│   └── preds/
│
└── figures/
    └── appendix/                           # Output location for thesis figures
