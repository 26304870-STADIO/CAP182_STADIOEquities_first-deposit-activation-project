# Model 1: Logistic Regression

## Purpose

This stage develops and evaluates a Logistic Regression classification model using the feature-engineered UCI Bank Marketing dataset.

The UCI Bank Marketing dataset is used as a structural proxy for the STADIOEquities first-deposit activation problem. The model results therefore demonstrate the modelling workflow and should not be interpreted as predictions about actual STADIOEquities customers.

Logistic Regression is used as Model 1 because it provides an interpretable baseline for a binary classification problem. The model estimates the probability of an observation belonging to the positive class and provides coefficients that can be examined to understand the direction of the modelled associations.

## Input Dataset

The model uses the feature-engineered dataset produced by the Feature Engineering stage:

`data/processed/bank_marketing_features.csv`

The dataset contains numerical predictor variables and the binary target variable:

`y_binary`

The target is defined as:

- `0` = negative outcome
- `1` = positive outcome

No preprocessing or feature engineering is repeated in this notebook.

## Model Development

### 1. Load the Dataset

The notebook loads:

`data/processed/bank_marketing_features.csv`

The dataset dimensions, target distribution and predictor structure are checked before model development.

The target variable `y_binary` is separated from the predictor variables.

### 2. Train/Test Split

An 80/20 train/test split is used.

The split is stratified using the target variable to preserve the proportion of the two classes in both datasets.

The split uses:

- Test size: `20%`
- `random_state = 42`
- Stratification: `y`

This produces:

- Training observations: 36,168
- Test observations: 9,043

The test dataset is kept separate from model development and is only used for the final evaluation.

### 3. Logistic Regression Pipeline

The Logistic Regression model is implemented using a scikit-learn Pipeline containing:

1. `StandardScaler`
2. `LogisticRegression`

The predictor variables are standardised before model fitting.

Scaling is performed within the Pipeline so that the transformation is fitted only on the relevant training data, preventing information from the held-out test set from influencing model development.

The Logistic Regression model uses:

`max_iter = 1000`

and:

`random_state = 42`

### 4. Five-Fold Stratified Cross-Validation

Five-fold stratified cross-validation is performed on the training dataset.

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
| Accuracy | 89.17% |
| Precision | 62.71% |
| Recall | 18.29% |
| F1-score | 28.30% |
| ROC-AUC | 76.98% |

The results indicate that the model has some ability to distinguish between the two outcome classes. However, recall and F1-score are substantially lower than accuracy, reflecting the difficulty of identifying the minority positive class at the default classification threshold.

## Held-Out Test Evaluation

After cross-validation, the trained Logistic Regression pipeline is evaluated on the held-out test dataset.

The test-set results were:

| Metric | Test Set |
|---|---:|
| Accuracy | 89.34% |
| Precision | 65.56% |
| Recall | 18.71% |
| F1-score | 29.12% |
| ROC-AUC | 77.89% |

The test-set confusion matrix was:

```text
[[7881, 104],
 [ 860, 198]]
