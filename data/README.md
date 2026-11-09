# Bank Account Fraud (BAF) dataset

**Dataset:** Feedzai Bank Account Fraud (BAF), NeurIPS 2022. Use **Base.csv only**.

- [Kaggle dataset](https://www.kaggle.com/datasets/sgpjesus/bank-account-fraud-dataset-neurips-2022)
- [Official repository and datasheet](https://github.com/feedzai/bank-account-fraud)

## Local setup (later)

1. Download the dataset independently on each contributor's computer.
2. Place `Base.csv` at `data/raw/Base.csv` (create `raw/` locally).
3. Never commit raw or processed dataset files to GitHub.
4. Study the feature descriptions and negative missing-value codes before preprocessing.

## Required temporal partitions

| Partition | Months | Purpose |
|---|---|---|
| Training | 0–4 | Fit preprocessing and models |
| Validation | 5 | Compare models and choose thresholds |
| Final test | 6–7 | Reserved for Stage 3 only |

Do **not** inspect test-month outcomes or use them to select models, features, or thresholds before Stage 3.
