# Model Comparison — Logistic Regression vs Gradient Boosting

## 1. Purpose

This document compares the performance of **Model 1: Logistic Regression** and **Model 2: Gradient Boosting Classifier** developed for the STADIOEquities first-deposit activation project.

The comparison uses the publicly available **UCI Bank Marketing dataset** as a structural proxy for the STADIOEquities activation problem. The dataset is not STADIOEquities customer data; therefore, the results demonstrate the modelling and evaluation methodology and are not interpreted as evidence about actual STADIOEquities customers.

## 2. Evaluation Notebook

The performance comparison is contained in:

`evaluation/evaluation.ipynb`

The direct comparison is presented in the model comparison section of the notebook.

### Input Dataset

The notebook uses:

`data/processed/bank_marketing_features.csv`

This is the fully processed and feature-engineered modelling dataset used by both models.

### How to Run

1. Open the repository in Jupyter Notebook, JupyterLab or VS Code.
2. Open `evaluation/evaluation.ipynb`.
3. Ensure that `data/processed/bank_marketing_features.csv` is available.
4. Install the required Python packages:
   - pandas
   - numpy
   - matplotlib
   - scikit-learn
5. Run the notebook cells from beginning to end.

The notebook uses repository-relative file paths and should therefore be run from the repository root.

## 3. Models Compared

### Model 1 — Logistic Regression

Logistic Regression was used as an interpretable linear baseline.

The model uses a `StandardScaler` and `LogisticRegression` within a scikit-learn pipeline. The model was evaluated using the same stratified train/test split and cross-validation procedure as Model 2.

### Model 2 — Gradient Boosting

Gradient Boosting Classifier was used as a tree-based ensemble model capable of modelling non-linear relationships and interactions between predictors.

The model does not require feature scaling and was evaluated using the same stratified train/test split and cross-validation procedure as Model 1.

Using the same evaluation framework allows the two models to be compared directly.

## 4. Evaluation Method

Both models were evaluated using:

- An **80/20 stratified train/test split** with `random_state=42`.
- **5-fold StratifiedKFold cross-validation** on the training data.
- A final evaluation using the **held-out test set**.
- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion matrices
- Classification reports

The target variable is `y_binary`, where:

- `1` represents the proxy conversion outcome.
- `0` represents the proxy non-conversion outcome.

The dataset contains 45,211 observations, with 39,922 observations in class 0 (88.30%) and 5,289 observations in class 1 (11.70%).

Because the target is imbalanced, accuracy is considered alongside precision, recall, F1-score and ROC-AUC.

## 5. Cross-Validation Comparison

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 89.16% | 62.71% | 18.22% | 28.21% | 76.98% |
| Gradient Boosting | 89.47% | 65.88% | 20.75% | 31.54% | 78.82% |

The cross-validation results show that Gradient Boosting produced higher values for all five evaluation metrics.

The differences are relatively modest. The largest difference is observed in F1-score, where Gradient Boosting achieved 31.54% compared with 28.21% for Logistic Regression. ROC-AUC was also higher for Gradient Boosting at 78.82%, compared with 76.98% for Logistic Regression.

## 6. Held-Out Test Comparison

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 89.34% | 65.56% | 18.71% | 29.12% | 77.89% |
| Gradient Boosting | 89.52% | 67.08% | 20.42% | 31.30% | 79.79% |

The held-out test results show the same general pattern as the cross-validation results.

Gradient Boosting achieved higher accuracy, precision, recall, F1-score and ROC-AUC than Logistic Regression on the held-out test set.

The difference in accuracy is small, at 0.18 percentage points, while the ROC-AUC difference is 1.90 percentage points.

## 7. Confusion Matrix Comparison

### Logistic Regression

| | Predicted 0 | Predicted 1 |
|---|---:|---:|
| Actual 0 | 7,881 | 104 |
| Actual 1 | 860 | 198 |

### Gradient Boosting

| | Predicted 0 | Predicted 1 |
|---|---:|---:|
| Actual 0 | 7,879 | 106 |
| Actual 1 | 842 | 216 |

The confusion matrices show that both models correctly classify a large number of class 0 observations. Both models identify fewer class 1 observations than class 0 observations.

Gradient Boosting correctly identifies 216 class 1 observations compared with 198 for Logistic Regression on the held-out test set. This corresponds with the higher recall achieved by Gradient Boosting.

## 8. Generalisation Comparison

The cross-validation and held-out test results are relatively close for both models.

### Logistic Regression

- Cross-validation ROC-AUC: 76.98%
- Test ROC-AUC: 77.89%

### Gradient Boosting

- Cross-validation ROC-AUC: 78.82%
- Test ROC-AUC: 79.79%

The similarity between cross-validation and test-set results indicates that both models produced consistent performance on unseen observations.

No substantial difference between validation and test performance is observed in the reported metrics.

## 9. Interpretation of the Comparison

The evaluation results show that the two models have similar overall performance, while Gradient Boosting produces modestly higher values across the reported evaluation metrics.

Gradient Boosting achieves higher test-set precision (67.08%) than Logistic Regression (65.56%) and higher test-set recall (20.42%) than Logistic Regression (18.71%). Its F1-score is also higher at 31.30%, compared with 29.12% for Logistic Regression.

ROC-AUC provides a threshold-independent measure of discrimination. Gradient Boosting achieves a test ROC-AUC of 79.79%, compared with 77.89% for Logistic Regression.

However, the differences should be interpreted in the context of the imbalanced target. Both models achieve relatively high accuracy because the majority class represents approximately 88% of observations. Neither model captures most of the positive-class observations at the default 0.50 classification threshold.

## 10. Interpretability

The models provide different forms of interpretability.

Logistic Regression provides coefficients and odds ratios that allow the direction and relative association of predictors with the modelled outcome to be examined.

Gradient Boosting provides feature-importance measures that indicate the relative contribution of variables to the model's predictions.

The evaluation identified `poutcome_success` as an important predictor in both modelling approaches. For Logistic Regression, its odds ratio was approximately 1.49. For Gradient Boosting, its feature importance was approximately 0.42.

These measures represent predictive associations within the dataset. They do not establish that any variable causes conversion or non-conversion.

## 11. Limitations

The comparison must be interpreted within the limitations of the proxy dataset.

The UCI Bank Marketing dataset is not STADIOEquities customer data. The target outcome, variables and customer journey represented in the dataset differ from the actual first-deposit activation process.

The class imbalance also affects interpretation of the results, particularly recall for the positive class.

Neither model was hyperparameter-tuned or subjected to resampling during this baseline evaluation.

The comparison therefore demonstrates the relative behaviour of the two modelling approaches on the selected public dataset rather than establishing how either model would perform on actual STADIOEquities customer data.

Validation using actual STADIOEquities customer data would be required before applying either model to the first-deposit activation problem.

## 12. Summary

Both Logistic Regression and Gradient Boosting produced consistent results across cross-validation and the held-out test set.

The results were:

| Model | Test Accuracy | Test Precision | Test Recall | Test F1-score | Test ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 89.34% | 65.56% | 18.71% | 29.12% | 77.89% |
| Gradient Boosting | 89.52% | 67.08% | 20.42% | 31.30% | 79.79% |

Gradient Boosting produced higher values across all reported test-set metrics, while Logistic Regression provides a more directly interpretable linear model through its coefficients and odds ratios.

The comparison provides the evidence required to assess the two models using a consistent evaluation framework. Any model selection for actual STADIOEquities deployment would require validation using real customer data and consideration of the organisation's operational requirements, intervention capacity and the costs associated with different types of classification errors.
