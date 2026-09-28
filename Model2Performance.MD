# Model 2 Performance — Gradient Boosting

## 1. Purpose

This document presents the performance results of **Model 2: Gradient Boosting Classifier** developed for the STADIOEquities first-deposit activation project.

The evaluation uses the publicly available **UCI Bank Marketing dataset** as a structural proxy for the STADIOEquities activation problem. The dataset is not STADIOEquities customer data; therefore, the results reported here demonstrate the modelling and evaluation methodology and are not interpreted as evidence about actual STADIOEquities customers.

## 2. Evaluation Notebook

The performance calculations for Model 2 are contained in:

`evaluation/evaluation.ipynb`

The notebook reconstructs the Gradient Boosting model using the same feature-engineered dataset, train/test split and modelling configuration used during Model 2 development.

### Input Dataset

The notebook uses:

`data/processed/bank_marketing_features.csv`

This is the fully processed and feature-engineered modelling dataset.

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

## 3. Evaluation Method

The Gradient Boosting model was evaluated using:

- An **80/20 stratified train/test split** with `random_state=42`.
- **5-fold StratifiedKFold cross-validation** on the training data.
- A final evaluation using the **held-out test set**.
- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion matrix
- Classification report

The target variable is `y_binary`, where:

- `1` represents the proxy conversion outcome.
- `0` represents the proxy non-conversion outcome.

The dataset contains 45,211 observations, with 39,922 observations in class 0 (88.30%) and 5,289 observations in class 1 (11.70%). Because the target is imbalanced, accuracy is considered together with precision, recall, F1-score and ROC-AUC rather than being used as the sole measure of performance.

## 4. Cross-Validation Performance

The Gradient Boosting model achieved the following results using 5-fold stratified cross-validation:

| Metric | Cross-validation |
|---|---:|
| Accuracy | 89.47% |
| Precision | 65.88% |
| Recall | 20.75% |
| F1-score | 31.54% |
| ROC-AUC | 78.82% |

The cross-validation results provide an estimate of how consistently the model performs across different validation folds of the training data.

## 5. Held-Out Test Performance

The final Gradient Boosting model was evaluated on the held-out test set:

| Metric | Test set |
|---|---:|
| Accuracy | 89.52% |
| Precision | 67.08% |
| Recall | 20.42% |
| F1-score | 31.30% |
| ROC-AUC | 79.79% |

The similarity between the cross-validation and test-set results indicates that the model produced reasonably consistent performance on unseen observations.

## 6. Confusion Matrix

The Gradient Boosting confusion matrix on the held-out test set was:

| | Predicted 0 | Predicted 1 |
|---|---:|---:|
| Actual 0 | 7,879 | 106 |
| Actual 1 | 842 | 216 |

The model correctly identified 7,879 observations belonging to class 0 and 216 observations belonging to class 1.

The model therefore identified a larger proportion of the actual positive-class observations than the Logistic Regression model at the default 0.50 classification threshold. This is reflected in the recall of 20.42%.

## 7. Interpretation of Results

The Gradient Boosting model demonstrates consistent performance across cross-validation and the held-out test set.

The test-set precision of 67.08% indicates that approximately two-thirds of observations predicted as the positive class were correctly classified. The recall of 20.42% indicates that the model identified approximately one-fifth of the actual positive-class observations at the default classification threshold.

The accuracy of 89.52% should be interpreted alongside the class distribution because approximately 88% of observations belong to class 0. Accuracy alone therefore does not provide a complete representation of model performance.

The ROC-AUC of 79.79% indicates that the model has useful ability to distinguish between the two classes across different probability thresholds.

## 8. Feature Importance

Gradient Boosting provides feature-importance measures that indicate the relative contribution of input variables to the model's predictions.

The highest feature-importance values identified in the evaluation were:

| Feature | Importance |
|---|---:|
| `poutcome_success` | 0.4196 |
| `age` | 0.0924 |
| `contact_unknown` | 0.0634 |
| `day` | 0.0604 |
| `month_mar` | 0.0497 |
| `housing_yes` | 0.0468 |
| `month_oct` | 0.0382 |
| `month_jun` | 0.0364 |
| `balance` | 0.0270 |
| `month_sep` | 0.0239 |

`poutcome_success` has substantially higher feature importance than the other variables in this model.

These feature-importance values describe predictive contribution within the fitted model. They should not be interpreted as evidence that a variable causes conversion or non-conversion.

## 9. Statistical and Diagnostic Measures

The evaluation incorporates both cross-validation and held-out test-set assessment.

**5-fold stratified cross-validation** was used to assess the consistency of model performance across different subsets of the training data while maintaining the class distribution.

The **held-out test set** was used only for the final evaluation and was not used during cross-validation or model tuning.

The **confusion matrix** provides the class-level distribution of correct and incorrect predictions, while the **classification report** provides precision, recall and F1-score for the classification outcome.

ROC-AUC was also used because it evaluates the model's ability to discriminate between the two classes across different probability thresholds.

## 10. Reproducibility

The evaluation notebook uses:

- `random_state=42` for the train/test split.
- `random_state=42` for the cross-validation procedure.
- `random_state=42` for the Gradient Boosting model.
- The same feature-engineered dataset used during model development.
- The same Gradient Boosting modelling configuration used during Model 2 development.

The Gradient Boosting model was not persisted as a separate model file. Instead, `evaluation.ipynb` reconstructs the model using the same deterministic procedure. This allows the reported evaluation results to be reproduced from the repository.

## 11. Limitations

The results must be interpreted within the limitations of the proxy dataset.

The UCI Bank Marketing dataset is structurally related to the project's classification objective but is not STADIOEquities customer data. Consequently, the model's performance cannot be interpreted as evidence of how accurately first-deposit activation could be predicted for actual STADIOEquities customers.

The target is also imbalanced, with the majority of observations belonging to class 0. This contributes to the difference between the model's relatively high accuracy and its substantially lower recall for the positive class.

No hyperparameter tuning or resampling was performed at this baseline evaluation stage.

## 12. Summary

Gradient Boosting achieved:

- **89.52% accuracy**
- **67.08% precision**
- **20.42% recall**
- **31.30% F1-score**
- **79.79% ROC-AUC**

on the held-out test set.

The results provide the Model 2 performance measures required for comparison with Model 1. The direct comparison of Logistic Regression and Gradient Boosting is presented separately in `Comparison.MD`.
