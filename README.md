# Remaining Useful Life Estimation for Industry 4.0 Digital Twins  
**MSc Dissertation: Comparative Evaluation of LSTM, 1D-CNN and Hybrid CNN-LSTM Architectures on NASA C-MAPSS**

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
```

## How to Reproduce the Experiments

### 1. Environment Setup
```bash
python -m venv .venv
source .venv/bin/activate          # Linux/macOS
# or
.venv\Scripts\activate             # Windows

pip install -r requirements.txt
````
### 2. Execution Order
```text
1. 01_data_exploration.ipynb           # Inspect raw data and RUL distributions
2. 02_preprocessing_unified.ipynb      # Generate engine-isolated sequences
3. 03G_baseline_lstm.ipynb             # Train Baseline LSTM (10 seeds)
4. 03G_improved_lstm.ipynb             # Train Stacked LSTM (10 seeds)
5. 04G_cnn.ipynb                       # Train 1D-CNN (10 seeds)
6. 05G_cnn_lstm.ipynb                  # Train Hybrid CNN-LSTM (10 seeds)
7. 07_statistical_tests.ipynb          # Run paired statistical tests  
8. 08_appendix_figures.ipynb           # Generate all figures used in the thesis

```
Each training notebook (03G-05G) automatically:

- Trains across the 10 fixed seeds
- Saves model weights, predictions and training histories
- Writes a summary metrics CSV

## Key Methodological Choices

- **Engine-isolated validation** – entire engines are held out; no sliding-window leakage across the train/validation boundary.
- **Regime-aware scaling** – sensors are scaled within operational regimes (critical for FD002).
- **Piecewise RUL target** - capped at 125 cycles as per the literature.
- **Asymmetric NASA Score (S)** – penalises late predictions more heavily than early ones.
- **Multi-seed protocol** - all reported means and statistical tests are based on 10 independent initialisations.

## Citation

If you use or adapt this code, please cite the dissertation:

*Gareth Du Plooy, (2026). Remaining Useful Life Estimation for Industry 4.0 Digital Twins: A Comparative Evaluation of LSTM, 1D-CNN and Hybrid CNN-LSTM Architectures. MSc Dissertation, Keele University.*

## Contact

For questions regarding the experimental setup or results, please contact the author via the details provided in the dissertation.
