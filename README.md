# Bank Account Fraud Detection

**PROJECT IN MACHINE LEARNING 2026/2027 · University of Haifa**

*An experimental study of rare-event classification, nonlinear fraud detection, and decisions under a limited investigation budget.*

![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikitlearn&logoColor=white)
![Status](https://img.shields.io/badge/Status-Planning-blue)
![Project](https://img.shields.io/badge/Academic-ML%20Lab-64748B)
![Submission deadline](https://img.shields.io/badge/Final%20Submission-31%20Jan%202027-64748B)

## Overview

This project investigates how to detect fraudulent bank-account applications when fraud is rare, models may behave differently across months, and investigators can review only a limited share of applications.

We use the **Bank Account Fraud (BAF) dataset, Base version**, described by Jesus et al. (NeurIPS 2022). The dataset contains approximately one million synthetic applications across eight months, with about 1% labeled as fraud.

The project follows **three prescribed stages**. Each stage includes self-learning questions, evidence-driven experiments, a reproducible implementation, and a written interpretation. The goal is to explain *why* results change, not merely report the best score.

## Research Stages

### Stage 1 — Rare Fraud: Logistic Regression

**Question:** When approximately 1% of applications are fraudulent, how should we evaluate detection, and how well does logistic regression perform?

- Establish the **never-predict-fraud** baseline to demonstrate why accuracy can be misleading.
- Train logistic regression with and without `class_weight="balanced"`.
- Compare precision–recall curves, average precision, score distributions, and **recall at 5% false-positive rate (FPR)**.
- Report threshold trade-offs: precision, recall, and flagged applications per 1,000.
- Explain whether class weighting changes the ranking or mainly the scores.

**Deliverables:** Reproducible code, required comparison table and figures, answers to self-check questions, Stage 1 report, and AI-use disclosure.

### Stage 2 — Nonlinear Fraud Detection: Random Forest

**Question:** Does a random forest catch more fraud than logistic regression, and do improvements come from individual features or interactions?

- Compare random forest with the best Stage 1 logistic regression model using the **same split and metrics**.
- Test tree depths **1, 2, 4, 8, and unlimited**.
- Compare minimum leaf sizes (**1, 10, 50**) with and without `class_weight="balanced_subsample"`.
- Interpret how depth, feature interactions, rare fraud cases, and class weights affect results.

**Deliverables:** Reproducible experiments, precision–recall and depth-comparison figures, results table for forest settings, self-check answers, Stage 2 report, and AI-use disclosure.

### Stage 3 — Later Months and Limited Review Budgets

**Question:** When investigators can review only a fixed share of applications, which model and decision rule catch the most fraud in later months?

- **Freeze model choices and thresholds before examining final test months 6 and 7.**
- Compare the selected logistic regression and random forest models across months 5, 6, and 7.
- Apply a **fixed threshold selected on validation month 5** to later months.
- Compare that policy with reviewing the **top 1% and top 5%** of monthly application scores.
- Report flagged counts, precision, recall, and an evidence-based operational recommendation.

**Deliverables:** Reproducible temporal and budget evaluations, required month-by-month comparison table, Stage 3 report, self-check answers, and AI-use disclosure.

## Dataset

- **Source:** [Bank Account Fraud Dataset — NeurIPS 2022 (Kaggle)](https://www.kaggle.com/datasets/sgpjesus/bank-account-fraud-dataset-neurips-2022)
- **Official documentation and datasheet:** [Feedzai BAF repository](https://github.com/feedzai/bank-account-fraud)
- **File:** `Base.csv` only; other variants are outside the assignment scope.
- **Target:** `is_fraud` (`1` means fraud).
- **Time variable:** `month` (months 0–7).

The data are synthetic, designed to resemble an anonymized real banking dataset; they do not contain real customers.

### Mandatory Chronological Split

| Partition | Months | Purpose |
|---|---|---|
| Training | 0–4 | Fit preprocessing and models |
| Validation | 5 | Compare models and select thresholds |
| Final test | 6–7 | Stage 3 evaluation only |

**Data leakage rule:** Do not use months 6–7 to choose models, hyperparameters, preprocessing decisions, or thresholds.

### Required Preprocessing

1. Remove `month` from model inputs (retain it for partitioning).
2. Check whether `device_fraud_count` is constant; exclude it as instructed.
3. One-hot encode `payment_type`, `employment_status`, `housing_status`, `source`, and `device_os`.
4. Identify negative missing-value codes using the official datasheet and **retain them as specified**.
5. Standardize numeric features for logistic regression, fitting the scaler on **training months only**.
6. If random forest training is too slow, the assignment permits using a random **30% of training applications**; document any sampling and its effect.

Raw data should not be committed to the repository. Dataset acquisition and local paths will be documented when implementation begins.

## Evaluation Protocol

The **primary metric** throughout the project is **recall at 5% false-positive rate**: the share of fraudulent applications caught when approximately 5% of legitimate applications are flagged. Precision–recall curves and average precision accompany this metric.

Additional required outputs include:

- Stage 1: accuracy for the never-fraud baseline and comparison models; threshold table; precision at 5% FPR.
- Stage 2: average precision and recall at 5% FPR for each forest configuration.
- Stage 3: fraud rate and recall at 5% FPR by month; flagged application counts, precision, and recall for fixed-threshold and top-K rules at 1% and 5% budgets.

The exact threshold-selection and tie-handling conventions will be documented in the implementation to make results reproducible.

## Scientific and Academic Integrity

- **Predict before running:** Record the expected result and rationale for every experiment, then compare with the observed outcome.
- **Report negative results:** Include unsuccessful configurations and explain what they reveal.
- **Reproduce results:** Use fixed random seeds and provide one notebook or script that recreates every submitted figure and table.
- **Compare fairly:** Use the prescribed partitions and consistent metrics across stages.
- **Use only allowed models:** Logistic regression (Stage 1) and random forest (Stage 2), with their selected variants in Stage 3. No additional model families are planned.
- **Own the interpretation:** AI assistants may help write or debug code, but the analysis, interpretation, and written answers must be the students' own work.
- **Disclose AI use:** End each stage report with a short, specific AI-use note.
- **Prepare for oral checks:** Both contributors should understand every submitted line of code and the mathematical reasoning behind it.

## Technical Stack

| Purpose | Planned tools |
|---|---|
| Programming | Python 3.11+ |
| Data manipulation | pandas, NumPy |
| Modeling and metrics | scikit-learn |
| Visualization | Matplotlib, Seaborn |
| Experiments | Jupyter notebooks and/or Python scripts |
| Tests | pytest |
| Collaboration | Git, GitHub Issues, pull requests |

These are planned tools, not a claim that the dependencies or code have already been installed.

## Repository Architecture

The existing repository will be audited before adopting or changing a directory layout. Proposed organization (not yet implemented):

```text
ml-project-bank-fraud-detection/
├── data/
│   └── README.md
├── notebooks/
├── src/
│   ├── data_loading.py
│   ├── preprocessing.py
│   ├── models.py
│   └── evaluation.py
├── experiments/
├── results/
│   ├── figures/
│   └── metrics/
├── reports/
│   ├── stage_1/
│   ├── stage_2/
│   └── stage_3/
├── tests/
├── docs/
│   └── progress/
├── requirements.txt
├── .gitignore
└── README.md
```

## Getting Started

Clone the existing repository:

```bash
git clone https://github.com/fidaaarrabi/ml-project-bank-fraud-detection.git
cd ml-project-bank-fraud-detection
```

**Environment setup and dataset-loading commands will be added after the project structure and dependencies are implemented and verified.**

## Semester Roadmap

**Project start:** November 1, 2026. **Confirmed final submission deadline:** January 31, 2027. The dates below are our internal working plan, not official intermediate deadlines.

| Dates | Phase | Main evidence |
|---|---|---|
| Nov 1–9, 2026 | **Project foundation:** scope, repository planning, dataset documentation, and initial setup | README, project plan, dataset notes; completion to be confirmed |
| Nov 10–23, 2026 | **Stage 1 — Rare fraud detection:** baseline, unweighted and weighted logistic regression, PR curves, recall at 5% FPR, predictions and report | Reproducible experiments, comparison table, Stage 1 report |
| Nov 24–Dec 20, 2026 | **Stage 2 — Random forest:** depth and leaf-size experiments, class weighting, comparison with logistic regression | Depth plot, PR curves, model comparison, Stage 2 report |
| Dec 21, 2026–Jan 17, 2027 | **Stage 3 — Later months and review budgets:** fixed thresholds, top-1% and top-5% review budgets, operational recommendation | Month-by-month tables, budget analysis, Stage 3 report |
| Jan 18–31, 2027 | **Final integration and submission:** reproducibility checks, combined report and documentation | Final report, runnable code, validated figures and tables |

**Scheduling note:** Project foundation is targeted for completion by November 9; completion should be confirmed by both contributors. Stage 1 is planned for November 10–23. Later dates are provisional and can be adjusted without changing the January 31 submission deadline.

## Results and Findings

**Status: Planning — no experimental results are reported yet.** Findings will be added only after experiments have been run and validated.

## Collaboration and Development Practices

The project is developed collaboratively by two students. Proposed workflow:

- `main`: stable, reviewed work.
- `feature/*`, `docs/*`, `fix/*`: focused branches.
- Issues describe the goal and acceptance criteria; pull requests link to issues and explain changes.
- Both students contribute to implementation, evaluation, documentation, and peer review.
- Progress updates should document actual work, decisions, difficulties, and next steps—not artificial commit activity.
- No changes to this repository are made through ChatGPT without explicit user approval.

## References

1. Jesus et al. (2022), *Turning the Tables: Biased, Imbalanced, Dynamic Tabular Datasets for ML Evaluation*. [arXiv:2211.13358](https://arxiv.org/abs/2211.13358).
2. James, Witten, Hastie, Tibshirani & Taylor (2023), *An Introduction to Statistical Learning with Applications in Python* (ISLP). [statlearning.com](https://www.statlearning.com/).
3. [scikit-learn User Guide](https://scikit-learn.org/stable/user_guide.html).

## Academic Context

**PROJECT IN MACHINE LEARNING 2026/2027** · University of Haifa.

## Authors

**Fidaa Arrabi**  
B.Sc. Data Science & Information Systems  
University of Haifa

**Natalie Mosleh**  
B.Sc. Computer Science  
University of Haifa

## Acknowledgments

University of Haifa — PROJECT IN MACHINE LEARNING staff.

BAF dataset authors and contributors.
