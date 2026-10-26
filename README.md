# Bank Account Fraud Detection

**Machine Learning Lab · University of Haifa**

*An experimental machine learning study of imbalanced fraud detection, temporal generalization, and resource-constrained decision-making.*

![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikitlearn&logoColor=white)
![Status](https://img.shields.io/badge/Status-Planning-blue)
![Project](https://img.shields.io/badge/Academic-ML%20Lab-64748B)

---

## Overview

Fraud detection is a challenging machine learning problem because fraudulent applications represent a small fraction of overall activity, fraud patterns may change over time, and investigation resources are limited.

A model that achieves high classification accuracy may still fail to identify meaningful fraudulent activity. Likewise, a model that performs well on historical data may deteriorate when evaluated on future applications.

This project investigates these challenges using the **Bank Account Fraud (BAF) dataset**, introduced in the NeurIPS 2022 research literature.

Our goal is not simply to maximize predictive accuracy, but to understand how different machine learning approaches behave under realistic operational constraints.

The project emphasizes rigorous experimentation, theoretical understanding, reproducibility, and critical analysis of model limitations.

## Research Objectives

The study is organized around three central research directions.

### 01 — Imbalanced Fraud Classification

Investigate how class imbalance influences model learning, predictions, and evaluation.

**Research questions:**

- How do baseline classification models compare with ensemble and boosting approaches?
- Which evaluation metrics provide the most meaningful assessment of rare-event detection?
- How do different modeling choices affect the trade-off between precision and recall?

**Planned methodology:**

Establish reproducible baselines, train selected classical machine learning models, and evaluate their performance using appropriate classification metrics.

### 02 — Temporal Generalization

Examine how well fraud detection models generalize to observations from later time periods.

**Research questions:**

- Does predictive performance change when evaluation moves from random splits to chronological splits?
- How sensitive are different models to temporal changes in the data?
- Which features and model behaviors are associated with performance deterioration?

**Planned methodology:**

Compare suitable validation strategies, evaluate models across time-based partitions, and investigate changes in predictive performance.

### 03 — Resource-Constrained Fraud Detection

Study fraud detection as a decision-making problem under limited investigation capacity.

**Research questions:**

- How should suspicious applications be prioritized when only a limited number can be reviewed?
- What proportion of fraudulent applications can be identified within a fixed investigation budget?
- How do different models perform when evaluated using operational rather than purely statistical criteria?

**Planned methodology:**

Rank applications by predicted risk, simulate limited review capacity, and analyze detection performance at different operational thresholds.

*These research directions are preliminary and will be aligned with the official three-stage project instructions.*

---

## Dataset

**Bank Account Fraud (BAF)**

The BAF dataset is a research benchmark designed to support investigation of fraud detection challenges, including class imbalance, model generalization, and responsible evaluation.

**Reference:**

Jesus et al. (2022). *Turning the Tables: Biased, Imbalanced, Dynamic Tabular Datasets for ML Evaluation.* NeurIPS 2022.

Official dataset repository:

https://github.com/feedzai/bank-account-fraud

### Data Handling Principles

- Preserve the integrity of the original dataset.
- Keep raw datasets separate from processed artifacts.
- Prevent data leakage between training and evaluation partitions.
- Apply learned preprocessing transformations using training data only.
- Document all data transformations and experimental assumptions.
- Avoid committing large datasets or generated artifacts unless explicitly required.

Dataset access and preprocessing instructions will be documented as implementation progresses.

---

## Methodology

The experimental workflow will follow a reproducible machine learning process.

**Data Acquisition → Data Validation → Exploratory Analysis → Preprocessing → Model Training → Evaluation → Error Analysis → Reporting**

### Model Development

Candidate approaches include:

- Simple baseline classifiers
- Logistic Regression
- Random Forest
- Gradient Boosting

Final model selection will depend on the official project requirements and experimental findings.

### Evaluation Strategy

Depending on the research stage, evaluation may include:

| Evaluation area | Candidate metrics |
|---|---|
| Classification | Precision, Recall, F1-score |
| Imbalanced prediction | PR-AUC, ROC-AUC |
| Temporal generalization | Performance across chronological partitions |
| Investigation capacity | Precision@k, Recall@k, fraud capture rate |
| Model reliability | Error analysis and performance stability |

Metrics will be selected according to the relevant research question rather than reported indiscriminately.

### Experimental Integrity

To support valid comparisons, the project aims to maintain:

1. Consistent data partitions across comparable experiments.
2. Fixed random seeds where applicable.
3. Explicitly documented preprocessing and model configurations.
4. Separation between training, validation, and final evaluation data.
5. Reproducible evaluation procedures.
6. Clear documentation of limitations and negative findings.

---

## Technical Stack

| Area | Planned tools |
|---|---|
| Language | Python |
| Data processing | pandas, NumPy |
| Machine learning | scikit-learn |
| Visualization | Matplotlib, Seaborn |
| Experimentation | Jupyter Notebook |
| Testing | pytest |
| Version control | Git, GitHub |

Additional dependencies will be introduced only when justified by the experimental requirements.

---

## Repository Architecture

```text
ml-lab-bank-fraud-detection/
│
├── data/
│   └── README.md
│
├── notebooks/
│   └── 01_exploratory_analysis.ipynb
│
├── src/
│   ├── __init__.py
│   ├── data_loading.py
│   ├── preprocessing.py
│   ├── models.py
│   └── evaluation.py
│
├── results/
│   ├── figures/
│   └── metrics/
│
├── reports/
│   ├── stage_1/
│   ├── stage_2/
│   └── stage_3/
│
├── tests/
│
├── requirements.txt
├── .gitignore
└── README.md
```

*The structure represents the intended repository organization. Components will be introduced incrementally.*

---

## Getting Started

### Prerequisites

- Python 3.11 or later
- Git
- A Python virtual environment
- Access to the BAF dataset

### Clone the Repository

```bash
git clone https://github.com/<your-username>/ml-lab-bank-fraud-detection.git
cd ml-lab-bank-fraud-detection
```

Replace `<your-username>` with the actual repository owner.

### Create a Virtual Environment

**Windows (PowerShell):**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**macOS / Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### Install Dependencies

```bash
python -m pip install -r requirements.txt
```

The dependency file and executable workflows will be finalized during initial development.

---

## Project Roadmap

| Phase | Milestone | Status |
|---|---|---|
| 00 | Project declaration and repository initialization | Planned |
| 01 | Dataset investigation and theoretical foundations | Planned |
| 02 | Baseline modeling and imbalanced classification experiments | Planned |
| 03 | Temporal generalization experiments | Planned |
| 04 | Investigation-capacity analysis | Planned |
| 05 | Final experimental analysis and reproducibility review | Planned |
| 06 | Final report and presentation | Planned |

The roadmap will be updated to reflect the official academic milestones.

---

## Results and Findings

**Status: Experiments not yet conducted.**

Experimental results will be published after implementation and validation.

Future documentation will include:

- Baseline performance comparisons
- Model evaluation tables
- Relevant visualizations
- Temporal performance analysis
- Operational decision trade-offs
- Interpretation of results and limitations

All reported findings will be supported by reproducible experiments.

---

## Collaboration and Development Practices

The repository is maintained collaboratively by two students.

### Branching Strategy

- `main` — reviewed, stable project state
- `feature/*` — feature development and experiments
- `docs/*` — documentation improvements
- `fix/*` — corrections and bug fixes

### Contribution Guidelines

Contributions should follow these principles:

- Keep commits focused and descriptive.
- Use pull requests for substantial changes.
- Review code and experimental assumptions before merging.
- Document significant design decisions.
- Avoid committing temporary files, virtual environments, credentials, or unnecessary datasets.
- Ensure that both contributors understand the theoretical and experimental aspects of the project.

### Commit Naming Examples

```text
docs: document research objectives
chore: initialize project structure
feat: implement baseline classifier
test: add preprocessing validation
exp: compare temporal evaluation strategies
fix: prevent preprocessing data leakage
```

---

## Academic Context

This repository was created as part of the **Machine Learning Lab** at the University of Haifa.

The project emphasizes independent learning, mathematical and theoretical understanding, experimental investigation, and scientific communication.

All implementations, analyses, and conclusions will be developed in accordance with the course requirements and academic integrity guidelines.

## Authors

**Fidaa Arrabi**  
B.Sc. Data Science & Information Systems  
University of Haifa

**Project Partner**  
B.Sc. Computer Science  
University of Haifa

## Acknowledgments

University of Haifa — Machine Learning Lab course staff.

BAF dataset authors and contributors.

---

**Project Status:** Planning and repository initialization.
