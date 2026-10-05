# Comparing Logistic Regression and Random Forest for Binary Classification

IN6227 Assignment 1, Variant 1. A complete workflow for the instructor-provided `train.csv` and `test.csv` split.

## Run in Google Colab

1. Upload `IN6227_Assignment1.ipynb` to Google Colab.
2. Select a CPU runtime and choose **Runtime > Run all**.
3. Upload both supplied data files when prompted, keeping their original filenames.
4. The notebook runs training-only model selection, evaluates the held-out test set and writes outputs to `results/`.
5. The last cell optionally downloads a results ZIP.

## Run locally

Install the analysis dependencies with `pip install -r requirements.txt`. Use Jupyter or VS Code to run the notebook, with `train.csv` and `test.csv` beside it or inside `dataset/`. The original run used Python 3.13.15, NumPy 2.1.3, pandas 2.2.3 and scikit-learn 1.6.1. Jupyter is a separate interface dependency.

## Workflow

- Inspect training-data types, missingness, duplicates, class balance, outliers and correlations.
- Exclude missing labels; retain statistical outliers and all 15 predictors with documented reasons.
- Impute numeric gaps with training-fold medians and categorical gaps with an explicit category.
- One-hot encode nominal features and standardize numeric features for Logistic Regression.
- Fit all preprocessing inside identical three-fold stratified CV splits, with random seed 42.
- Compare six LR and eight RF configurations by mean validation average precision (AP).
- Refit each selected configuration on the full labelled training set.
- Evaluate with a fixed probability threshold of 0.5, reporting accuracy, balanced accuracy, precision, recall, F1, ROC-AUC and AP.
- Export metrics, CV results, predictions, plots, package versions and input SHA-256 hashes.

## Files

- `IN6227_Assignment1.ipynb`: complete annotated source notebook, with outputs cleared.
- `requirements.txt`: analysis dependencies.
- `results/run_summary.json`: aggregate record from the completed Colab run on 4 October 2026.
- `results/cv_summary.csv` and `results/test_metrics.csv`: aggregate validation and held-out results from that run.

The dataset is supplied separately. The source package excludes raw datasets, row-level predictions and report files. Re-running regenerates the full outputs; numerical results may vary slightly across library versions or platforms.

The CV-selected model is Random Forest. Its test AP is 0.7076 versus 0.7023 for Logistic Regression. At threshold 0.5, Random Forest has higher recall and F1, while Logistic Regression has higher precision and accuracy. This is a trade-off, not evidence of universal superiority.
