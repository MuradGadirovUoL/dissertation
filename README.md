# AI-Driven Prediction of Worst-Case Response Times (WCRT) in Fixed-Priority Real-Time Systems

This repository contains the full implementation, models, and reproducibility artefacts for the MSc dissertation project:

**"AI-Driven Prediction of Worst-Case Response Times in Fixed-Priority Uniprocessor Real-Time Systems"**

---

## 📑 Overview

This project investigates the feasibility of using supervised machine learning (ML) to estimate worst-case response times (WCRT) and predict schedulability in real-time systems scheduled under fixed-priority preemptive policies. The repository provides:

* Synthetic task-set generation scripts (UUniFast + Emberson strategy)
* Analytical labelling via Response-Time Analysis (RTA)
* Classification pipeline for schedulability prediction
* Regression pipeline for WCRT estimation
* Safety calibration using Conformalized Quantile Regression (CQR)
* Reproducibility artefacts (scripts, configs, seeds, environment setup)

The implementation follows the design described in the dissertation and is aligned with empirical real-time systems research (Joseph & Pandya, 1986; Bini & Buttazzo, 2005; Baruah et al., 2025).

---

## 📂 Repository Structure

```bash
├── data/                # Scripts to generate and preprocess synthetic datasets
├── models/              # Trained ML model checkpoints (classification + regression)
├── notebooks/           # Jupyter notebooks for experiments and figures
├── src/                 # Core Python source code
│   ├── generation/      # UUniFast + Emberson-based task generation
│   ├── rta/             # Response-Time Analysis (labelling)
│   ├── classification/  # Classification models & evaluation
│   ├── regression/      # Regression models & evaluation
│   ├── calibration/     # Safety wrapper (CQR, abstention)
│   └── utils/           # Helper functions, plotting, metrics
├── requirements.txt     # Python dependencies
├── environment.yml      # Conda environment (optional)
├── README.md            # This file
└── LICENSE
```

---

## 📊 Dataset

The full dataset used in this dissertation is **800,000 task sets (≈1 GB)**, too large to host directly on GitHub. It is available for download from Dropbox:

👉 [Download Main Dataset (CSV, \~1 GB)](https://www.dropbox.com/scl/fi/yg7vam5nee89vwt4d84ga/main_dataset.csv?rlkey=vjtp8hg0ropqrimbyvp9u24lz&st=1k9heoqf&dl=0)

### Dataset Structure

Each row corresponds to a task in a synthetic task set, with the following fields:

* `C` — Worst-case execution time
* `T` — Period
* `D` — Relative deadline
* `U` — Utilization (C/T)
* `hp_util` — Cumulative higher-priority utilization
* `n_tasks` — Number of tasks in the set
* `task_index` — Task index within the set
* `set_schedulable` — Binary label (1 = all tasks schedulable, 0 = unschedulable)
* `task_schedulable` — Binary label per task
* `R_true` — Ground-truth WCRT (if schedulable)

Additional engineered features are included for ML pipelines.

---

## ⚙️ Setup

### Requirements

* Python 3.9+
* Recommended: Conda or virtualenv

Install dependencies:

```bash
pip install -r requirements.txt
```

Or with Conda:

```bash
conda env create -f environment.yml
conda activate rta-ml
```

### Reproducibility

* All experiments are seeded with `42`
* Dataset splits (train/val/test) are saved to disk for exact reproducibility
* Dockerfile (optional) is provided for containerized execution

---

## 🚀 Usage

### 1. Generate synthetic dataset (optional)

```bash
python src/generation/generate_dataset.py --n_sets 10000 --out data/small_dataset.csv
```

### 2. Label dataset with Response-Time Analysis

```bash
python src/rta/label_dataset.py --input data/small_dataset.csv --output data/labeled.csv
```

### 3. Run classification pipeline

```bash
python src/classification/train_classifier.py --input data/labeled.csv --model xgboost
```

### 4. Run regression pipeline

```bash
python src/regression/train_regressor.py --input data/labeled.csv --model random_forest
```

### 5. Apply safety calibration (CQR)

```bash
python src/calibration/apply_cqr.py --input results/regression_preds.csv
```

---

## 📈 Evaluation

* **Classification:** Accuracy, F1, ROC-AUC, false positives per utilization band
* **Regression:** MAE, RMSE, R², underestimation rate
* **Calibration:** Coverage, interval width, abstention rate

Results are stored in `results/` with generated plots (ROC curves, residuals, coverage–abstention trade-offs).

---

## 🔬 Research Context

This repository supports the MSc dissertation submitted to the University of Leeds (2025). The project builds on:

* Classical schedulability theory (Joseph & Pandya, 1986; Audsley et al., 1993)
* Synthetic workload generation (Bini & Buttazzo, 2005; Emberson et al., 2010)
* ML-based schedulability frameworks (Baruah et al., 2025; Agrawal et al., 2023)

The implementation is **uniprocessor-focused** but extensible to multiprocessor systems in future work.

---

## 📜 License

This repository is released under the MIT License.

---

## ✍️ Citation

If you use this work in academic research, please cite the dissertation:

```bibtex
@mastersthesis{qadirov2025,
  title={AI-Driven Prediction of Worst-Case Response Times in Fixed-Priority Uniprocessor Real-Time Systems},
  author={Qadirov, M.K.},
  year={2025},
  school={University of Leeds}
}
```

---

## 🙌 Acknowledgements

* Supervisor: \[Supervisor’s Name], University of Leeds
* Funding: Azerbaijan Government Scholarship
* External references: Bini & Buttazzo (2005), Baruah et al. (2025), Kumar et al. (2024)

---
