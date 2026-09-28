# Model 1 Performance — Logistic Regression

## 1. Purpose

This document presents the performance results of **Model 1: Logistic Regression** developed for the STADIOEquities first-deposit activation project.

The evaluation uses the publicly available **UCI Bank Marketing dataset** as a structural proxy for the STADIOEquities activation problem. The dataset is not STADIOEquities customer data; therefore, the results reported here demonstrate the modelling and evaluation methodology and are not interpreted as evidence about actual STADIOEquities customers.

## 2. Evaluation Notebook

The performance calculations for Model 1 are contained in:

`evaluation/evaluation.ipynb`

The notebook reconstructs the Logistic Regression model using the same feature-engineered dataset, train/test split and modelling configuration used during Model 1 development.

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

The Logistic Regression model was evaluated using:

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

The Logistic Regression model achieved the following results using 5-fold stratified cross-validation:

| Metric | Cross-validation |
|---|---:|
| Accuracy | 89.16% |
| Precision | 62.71% |
| Recall | 18.22% |
| F1-score | 28.21% |
| ROC-AUC | 76.98% |

The cross-validation results provide an estimate of how consistently the model performs across different validation folds of the training data.

## 5. Held-Out Test Performance

The final Logistic Regression model was evaluated on the held-out test set:

| Metric | Test set |
|---|---:|
| Accuracy | 89.34% |
| Precision | 65.56% |
| Recall | 18.71% |
| F1-score | 29.12% |
| ROC-AUC | 77.89% |

The similarity between the cross-validation and test-set results indicates that the model produced reasonably consistent performance on unseen observations.

## 6. Confusion Matrix

The Logistic Regression confusion matrix on the held-out test set was:

| | Predicted 0 | Predicted 1 |
|---|---:|---:|
| Actual 0 | 7,881 | 104 |
| Actual 1 | 860 | 198 |

The model correctly identified 7,881 observations belonging to class 0 and 198 observations belonging to class 1.

The model therefore identified relatively few of the actual positive-class observations at the default 0.50 classification threshold. This is reflected in the recall of 18.71%.

## 7. Interpretation of Results

The Logistic Regression model provides a stable baseline for the classification problem. Cross-validation and held-out test results are relatively close across all reported metrics.

The test-set precision of 65.56% indicates that approximately two-thirds of observations predicted as the positive class were correctly classified. However, the recall of 18.71% indicates that the model identified less than one-fifth of the actual positive-class observations at the default classification threshold.

The relatively high accuracy of 89.34% should therefore be interpreted alongside the class distribution. Since approximately 88% of observations belong to class 0, accuracy alone does not provide a complete representation of model performance.

The ROC-AUC of 77.89% indicates that the model has useful ability to distinguish between the two classes across different probability thresholds.

## 8. Statistical and Diagnostic Measures

The evaluation incorporates both cross-validation and held-out test-set assessment.

**5-fold stratified cross-validation** was used to assess the consistency of model performance across different subsets of the training data while maintaining the class distribution.

The **held-out test set** was used only for the final evaluation and was not used during cross-validation or model tuning.

The **confusion matrix** provides the class-level distribution of correct and incorrect predictions, while the **classification report** provides precision, recall and F1-score for the classification outcome.

## 9. Reproducibility

The evaluation notebook uses:

- `random_state=42` for the train/test split.
- `random_state=42` for the cross-validation procedure.
- The same feature-engineered dataset used during model development.
- The same Logistic Regression modelling configuration used during Model 1 development.

The Logistic Regression model was not persisted as a separate model file. Instead, `evaluation.ipynb` reconstructs the model using the same deterministic procedure. This allows the reported evaluation results to be reproduced from the repository.

## 10. Limitations

The results must be interpreted within the limitations of the proxy dataset.

The UCI Bank Marketing dataset is structurally related to the project's classification objective but is not STADIOEquities customer data. Consequently, the model's performance cannot be interpreted as evidence of how accurately first-deposit activation could be predicted for actual STADIOEquities customers.

The target is also imbalanced, with the majority of observations belonging to class 0. This contributes to the difference between the model's relatively high accuracy and its substantially lower recall for the positive class.

No hyperparameter tuning or resampling was performed at this baseline evaluation stage.

## 11. Summary

Logistic Regression achieved:

- **89.34% accuracy**
- **65.56% precision**
- **18.71% recall**
- **29.12% F1-score**
- **77.89% ROC-AUC**

on the held-out test set.

The results establish Logistic Regression as the baseline against which Model 2, Gradient Boosting, can be compared using the same evaluation framework.
