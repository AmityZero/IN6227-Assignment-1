# Logistic Regression and Random Forest for Binary Classification

A notebook comparing Logistic Regression and Random Forest using separate training and test datasets.

## Data

The dataset is supplied separately. Both `train.csv` and `test.csv` are required, with matching columns and a `label` column containing `no` or `yes` values. Rows with missing labels are excluded from training or evaluation.

## Run in Google Colab

1. Open `IN6227_Assignment1.ipynb` in Google Colab.
2. Select a CPU runtime and choose **Runtime > Run all**.
3. Upload `train.csv` and `test.csv` when prompted.

The notebook writes outputs to `results/`. The final cell creates and downloads a results ZIP when `DOWNLOAD_RESULTS` is `True`.

## Run locally

Install the analysis dependencies:

```bash
pip install -r requirements.txt
```

Place `train.csv` and `test.csv` beside the notebook or in `dataset/`, then run all cells in Jupyter or VS Code. Install the notebook interface separately.

The recorded run used Python 3.13.15, NumPy 2.1.3, pandas 2.2.3 and scikit-learn 1.6.1. `requirements.txt` pins these three analysis packages and specifies Matplotlib `>=3.8,<4`. Results may vary across package versions or platforms.

## Workflow

1. Inspect training-data types, missing values, duplicates, class balance, outliers and correlations.
2. Impute missing features, one-hot encode categorical features and standardize numeric features for Logistic Regression. All preprocessing is fitted within the training folds.
3. Compare six Logistic Regression and eight Random Forest configurations using the same three-fold stratified cross-validation splits, random seed 42 and mean validation average precision (AP).
4. Refit the selected configuration for each model on the labelled training set and evaluate the held-out test set. Classification metrics use a probability threshold of 0.5.
5. Export metrics, cross-validation results, predictions, plots, package versions and input SHA-256 hashes.

## Files

- `IN6227_Assignment1.ipynb`: source notebook, with outputs cleared.
- `requirements.txt`: analysis dependencies.
- `results/run_summary.json`: recorded runtime versions, input hashes, data summaries and model results.
- `results/cv_summary.csv`: cross-validation results and selected parameters.
- `results/test_metrics.csv`: held-out test metrics.

Raw datasets and row-level predictions are excluded from the repository. Running the notebook regenerates the analysis outputs.

The recorded cross-validation run selected Random Forest. Test AP was 0.7076 for Random Forest and 0.7023 for Logistic Regression.
