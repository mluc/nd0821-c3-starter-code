# Model Card

For additional information see the Model Card paper: https://arxiv.org/pdf/1810.03993.pdf

## Model Details
* **Model type:** Logistic Regression (scikit-learn `sklearn.linear_model.LogisticRegression`)
* **Input:** Census tabular features (numeric + one-hot encoded categorical columns)
* **Output:** Binary label – `>50K` (positive class = 1) or `<=50K` (negative class = 0)
* **Hyper-parameters:**
  * `max_iter = 1000`
  * `random_state = 23`

* **Pre-processing:**
  * Continuous columns passed through unchanged.
  * Categorical columns one-hot encoded via scikit-learn
  * Labels binarised with `LabelBinarizer`.

## Intended Use
The model predicts whether an individual's annual income exceeds \$50 000 based on UCI Census data features. 

## Training Data
* Source: Census Income dataset (`data/census.csv`).  https://archive.ics.uci.edu/dataset/20/census+income
* Size: 32,562 rows × 15 columns
* Split: 80% train / 20% test using `train_test_split()`.

## Evaluation Data
The 20% hold-out split (≈ 6,512 rows)

## Metrics
The model is evaluated with precision, recall, and fbeta.  
Results on the test set:

| Metric | Value |
|--------|-------|
| Precision | 0.739 |
| Recall    | 0.275 |
| Fbeta  | 0.401 |

Per-slice categorical metrics are logged to `model/slice_output.txt` via the `evaluate_slices` utility.

## Ethical Considerations
It is reflecting societal biases present in historical data—e.g., gender or race ...

## Caveats and Recommendations
* Model performance is ok - consider tree-based models for higher accuracy.
* Monitor slice-based metrics for bias and retrain if needed.
