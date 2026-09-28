# Model 2: Gradient Boosting

## Purpose

This stage develops and evaluates a Gradient Boosting classification model using the feature-engineered UCI Bank Marketing dataset.

The UCI Bank Marketing dataset is used as a structural proxy for the STADIOEquities first-deposit activation problem. The target variable represents whether a client subscribed to a term deposit and is therefore used as a proxy for the project's financial conversion outcome. The model results should not be interpreted as predictions about actual STADIOEquities customers.

Gradient Boosting is used as Model 2 because it can model non-linear relationships and interactions between predictor variables. It provides a tree-based ensemble approach that can be compared with the Logistic Regression baseline.

## Input Dataset

The model uses the feature-engineered dataset produced by the Feature Engineering stage:

`data/processed/bank_marketing_features.csv`

The target variable is:

`y_binary`

where:

- `0` = non-conversion outcome
- `1` = conversion outcome

No preprocessing or feature engineering is repeated in this notebook.

## Model Development

### 1. Load the Dataset

The notebook loads:

`data/processed/bank_marketing_features.csv`

The dataset dimensions, target distribution and predictor structure are checked before model development.

The target variable `y_binary` is separated from the predictor variables.

### 2. Train/Test Split

An 80/20 train/test split is used.

The split is stratified using the target variable so that the proportion of the two outcome classes remains approximately consistent in the training and test datasets.

The split uses:

- Test size: `20%`
- `random_state = 42`
- Stratification: `y`

This produces:

- Training observations: 36,168
- Test observations: 9,043

The held-out test dataset is kept separate from model development and is only used for final evaluation.

### 3. Gradient Boosting Classifier

A `GradientBoostingClassifier` from scikit-learn is used.

The model is initialised with:

`random_state = 42`

The baseline Gradient Boosting model is trained without additional hyperparameter tuning.

This provides a reproducible baseline that can be compared with Logistic Regression using the same train/test split, cross-validation procedure and evaluation metrics.

Unlike Logistic Regression, Gradient Boosting does not require predictor standardisation because it is a tree-based model.

## Five-Fold Stratified Cross-Validation

Five-fold stratified cross-validation is performed using the training dataset.

The cross-validation configuration is:

- Number of folds: `5`
- Stratification: `StratifiedKFold`
- Shuffling: enabled
- `random_state = 42`

The held-out test dataset is not used during cross-validation.

The following evaluation metrics are calculated:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC

Multiple metrics are used because the target variable is imbalanced. Accuracy alone may therefore provide an incomplete view of model performance.

## Cross-Validation Results

The mean five-fold validation results were:

| Metric | Cross-Validation |
|---|---:|
| Accuracy | 89.47% |
| Precision | 65.88% |
| Recall | 20.75% |
| F1-score | 31.54% |
| ROC-AUC | 78.82% |

The Gradient Boosting model produced relatively similar training and validation performance across the cross-validation folds, although training performance was consistently higher.

The results indicate that the model has some ability to distinguish between the two outcome classes, while recall remains comparatively low at the default classification threshold.

## Held-Out Test Evaluation

After cross-validation, the Gradient Boosting model is evaluated on the held-out test dataset.

The test set was not used during model fitting or cross-validation and therefore provides an independent assessment of model performance on unseen observations.

The test-set results were:

| Metric | Test Set |
|---|---:|
| Accuracy | 89.52% |
| Precision | 67.08% |
| Recall | 20.42% |
| F1-score | 31.30% |
| ROC-AUC | 79.79% |

The confusion matrix was:

```text
[[7879, 106],
 [ 842, 216]]
