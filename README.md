# Digital Twin-Based Intrusion Detection for a Simulated Filling Plant

OS + AI/ML integrated assignment. A small digital-twin IDS (DT-IDS) for a tank-valve-bottle plant, based on
Varghese et al., "Digital Twin-based Intrusion Detection for Industrial Control Systems", IEEE PerCom Workshops 2022.

**Author:** Abdul Rehman | **Roll no.:** <add> | **Course:** Operating Systems + AI/ML

## What this project does
- Simulates a filling plant (tank, valve, bottle) in Python, sampled every 0.5 s (3000 rows).
- Injects three simulated attacks: command injection (CI), naive measurement modification (NMM),
  calculated measurement modification (CMM).
- Trains a baseline, Logistic Regression, Decision Tree, Random Forest and a stacked ensemble.
- Runs the simulator and detector as separate OS processes (Queue, Lock) and monitors CPU/RAM with psutil.

## Files
| File | Content |
|---|---|
| `DT_IDS_Notebook.ipynb` | All code, run top to bottom in Google Colab |
| `dataset.csv` | Generated labeled dataset (Normal, CMM, NMM, CI) |
| `os_log.csv` | CPU and memory log of the multi-process pipeline |
| `e4.csv`, `e5.csv`, `e6.csv` | Feature study, resource study, noise robustness results |
| `*.png` | Figures: architecture, model comparison, confusion matrix, features, noise, EDA |

## How to run
1. Open `DT_IDS_Notebook.ipynb` in Google Colab.
2. Choose **Runtime > Restart session and run all**.
3. The notebook regenerates `dataset.csv` and all result files (random seed 42).

## Environment
Python <version>, scikit-learn <version>, pandas <version>, numpy <version>, psutil <version>, matplotlib.
Platform: Google Colab (<n> CPUs, <RAM> GB).

## Main results (random 70/30 stratified split, seed 42)
| Model | Accuracy | Macro-F1 |
|---|---|---|
| Baseline (majority class) | 0.533 | 0.174 |
| Logistic Regression | 0.871 | 0.788 |
| Decision Tree | 0.879 | 0.802 |
| Random Forest | 0.857 | 0.802 |
| Stacked ensemble | 0.94 | 0.87 |

Time-series features raise command-injection recall from 0.45 to 0.98 (random split). A twin residual feature
(tank + bottle - 80) raises calculated-modification recall to 1.00. Results are from a small synthetic dataset
and are optimistic; see the report for limitations.

## Safety
All attacks are simulated in code on synthetic data. No real industrial system, network or third-party
infrastructure was scanned, attacked or modified.
