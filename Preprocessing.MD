# Preprocessing

## Purpose

This stage prepares the Bank Marketing proxy dataset for subsequent machine-learning modelling. The preprocessing steps focus on understanding the structure and quality of the raw data, identifying missing and unusual values, preparing the target variable, and addressing variables that may introduce information leakage.

The preprocessing stage does not include model training or evaluation.

## Dataset

The raw dataset used for this analysis is the `bank-full.csv` file located in:

`data/raw/bank-full.csv`

The dataset contains 45,211 observations and 17 variables, consisting of 16 input variables and the binary target variable `y`.

The target variable indicates whether a customer subscribed to a term deposit:

- `yes` = positive outcome
- `no` = negative outcome

The dataset is used as a proxy for the STADIOEquities first-deposit activation problem and does not represent actual STADIOEquities customer data.

## Preprocessing Steps

### 1. Data Loading

The raw `bank-full.csv` dataset is loaded using pandas.

The source file uses a semicolon (`;`) as its field separator, so the appropriate delimiter is specified when loading the dataset.

The dataset is inspected to confirm its dimensions, variables and data types.

### 2. Data Quality Checks

The dataset is examined for:

- Missing values
- Exact duplicate rows
- Unusual or special coded values
- Categorical values recorded as `"unknown"`
- Numerical variable ranges
- Target-class distribution

No standard missing values or exact duplicate rows were identified.

The dataset does not contain a unique customer identifier, so the duplicate check only identifies records where all available variable values are identical. It cannot confirm whether the dataset contains duplicate customers.

### 3. Handling `"unknown"` Values

The categorical variables `job`, `education`, `contact` and `poutcome` contain `"unknown"` values.

These values are retained rather than removed because they represent unavailable or unspecified information in the original dataset. Removing them would result in unnecessary data loss, particularly for `poutcome`.

The `"unknown"` category is therefore retained for subsequent feature engineering and modelling.

### 4. Target Variable

The target variable `y` is converted into a numerical binary variable called `y_binary`:

- `no` → `0`
- `yes` → `1`

The original `y` variable is retained at this stage for reference.

The target is imbalanced, with:

- `no`: 39,922 observations (88.3%)
- `yes`: 5,289 observations (11.7%)

This imbalance is considered during later model evaluation. Accuracy is therefore not used as the only measure of model performance; Precision, Recall, F1-score, ROC-AUC and confusion matrices are also considered.

### 5. Handling `pdays`

The `pdays` variable records the number of days since the customer was previously contacted.

A value of `-1` indicates that the customer was not previously contacted rather than representing an actual number of days.

There are 36,954 observations (81.74%) with `pdays = -1`.

These `-1` values are therefore replaced with `NaN` so that they are not interpreted as meaningful numerical values.

The information represented by this special value is retained for feature engineering through the creation of a `previously_contacted` indicator.

### 6. Handling `duration`

The `duration` variable represents the duration of the customer's last contact with the campaign.

Because this value is only known after the contact has taken place, including it in a model intended to identify customers before or during an intervention could introduce information leakage.

For this reason, `duration` is excluded from the primary modelling feature set.

### 7. Categorical Variables

Categorical variables remain in their original categorical form during preprocessing.

One-hot encoding is applied during the subsequent feature-engineering and model-preparation stage so that categorical variables can be represented as numerical inputs for machine-learning models.

### 8. Validation

The preprocessing output is checked to confirm that:

- The number of observations remains unchanged.
- The `pdays` special value has been converted to missing values.
- `y_binary` contains only the expected values of `0` and `1`.
- No rows have been removed during preprocessing.

### 9. Output

The preprocessed dataset is saved as:

`data/processed/bank_marketing_preprocessed.csv`

This file is used as the input for the subsequent feature-engineering stage.

## Notebook

The preprocessing code is contained in:

`preprocessing/preprocessing.ipynb`

### How to Use

1. Ensure `data/raw/bank-full.csv` is available in the repository.
2. Open `preprocessing/preprocessing.ipynb` in Jupyter Notebook or JupyterLab.
3. Run the notebook cells from top to bottom.
4. The preprocessed dataset will be created at:
   
   `data/processed/bank_marketing_preprocessed.csv`
   
5. Use the resulting file as the input for the feature-engineering stage.
