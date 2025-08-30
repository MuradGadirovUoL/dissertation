# AI-Driven Schedulability Assessment and Worst-Case Response Time Prediction in Fixed-Priority Uniprocessor Real-Time Systems


This repository contains the full implementation, models, and reproducibility artefacts for the MSc dissertation project:

**"AI-Driven Schedulability Assessment and Worst-Case Response Time Prediction in Fixed-Priority Uniprocessor Real-Time Systems
"**

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
├── data/
│   └── main_dataset_metadata.json
├── figures/
│   ├── confusion_matrices/
│   │   ├── logistic_regression_basic_cm.png
│   │   ├── logistic_regression_engineered_cm.png
│   │   ├── random_forest_basic_cm.png
│   │   ├── random_forest_engineered_cm.png
│   │   ├── xgboost_basic_cm.png
│   │   └── xgboost_engineered_cm.png
│   ├── clf_roc_overlay.png
│   ├── clf_xgb_feature_importances.png
│   ├── coverage_vs_util.png
│   ├── error_stratification.png
│   ├── improved_cqr_plot.png
│   ├── safety_distribution.png
│   ├── threshold_optimization.png
│   └── underestimation_analysis.png
├── models/
│   ├── classification_models/
│   │   ├── logistic_regression_basic.pkl
│   │   ├── logistic_regression_basic_cv.json
│   │   ├── logistic_regression_engineered.pkl
│   │   ├── logistic_regression_engineered_cv.json
│   │   ├── random_forest_basic.pkl
│   │   ├── random_forest_basic_cv.json
│   │   ├── random_forest_engineered.pkl
│   │   ├── random_forest_engineered_cv.json
│   │   ├── xgboost_basic.pkl
│   │   ├── xgboost_basic_cv.json
│   │   ├── xgboost_engineered.pkl
│   │   └── xgboost_engineered_cv.json
│   └── regression_models/
│       ├── base_linear_regression.pkl
│       ├── base_random_forest.pkl
│       ├── base_xgboost.pkl
│       ├── cqr_lower_model.pkl
│       ├── eng_random_forest.pkl
│       ├── eng_xgboost.pkl
│       ├── linear_regression_regressor.pkl
│       ├── random_forest_regressor.pkl
│       └── xgboost_regressor.pkl
├── notebooks/
│   ├── classification.ipynb
│   ├── dataset_generation.ipynb
│   └── regression.ipynb
├── results/
│   ├── results_base.csv
│   ├── results_comparison.csv
│   └── results_engineered.csv
├── README.md

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

### Reproducibility

* All experiments are seeded with `42`
* Dataset splits (train/val/test) are saved to disk for exact reproducibility
* Dockerfile (optional) is provided for containerized execution

---

## 📈 Evaluation

* **Classification:** Accuracy, F1, ROC-AUC, false positives per utilization band
* **Regression:** MAE, RMSE, R², underestimation rate
* **Calibration:** Coverage, interval width, abstention rate

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
@mastersthesis{gadirov2025,
  title={AI-Driven Schedulability Assessment and Worst-Case Response Time Prediction in Fixed-Priority Uniprocessor Real-Time Systems},
  author={Gadirov, M.K.},
  year={2025},
  school={University of Leeds}
}
```

---

## 🙌 Acknowledgements

* Supervisor: Professor Leandro Soares Indrusiak, University of Leeds
* Funding: Azerbaijan Government Scholarship
* External references: Bini & Buttazzo (2005), Baruah et al. (2025), Kumar et al. (2024)

---
