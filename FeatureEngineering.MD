# Feature Engineering

## Purpose

This stage transforms the preprocessed UCI Bank Marketing dataset into a modelling-ready predictor and target matrix.

The UCI Bank Marketing dataset is used as a structural proxy for the STADIOEquities first-deposit activation problem. The target variable represents whether a client subscribed to a term deposit and is therefore used as a proxy for the project's financial conversion outcome. The dataset is not used to make claims about actual STADIOEquities customers.

The feature-engineering stage does **not** train, tune, cross-validate or evaluate models. Those activities are performed in the modelling stage.

## Input Dataset

The feature-engineering notebook uses the output from the preprocessing stage:

`data/processed/bank_marketing_preprocessed.csv`

The notebook first loads this dataset and confirms its structure, data types and target variable before creating modelling features.

## Feature Engineering Steps

### 1. Previously Contacted

The `pdays` variable records the number of days since a customer was previously contacted. During preprocessing, `pdays = -1` was converted to a missing value because it represents the absence of a previous contact.

A binary feature called `previously_contacted` is created:

- `1` = customer had been contacted previously
- `0` = customer had not been contacted previously

This converts the information represented by the special value in `pdays` into an explicit modelling feature.

### 2. Age Bands

The original numerical `age` variable is retained. Additional age bands are created to investigate whether conversion patterns differ across broader age ranges without assuming that the relationship between age and the target is strictly linear.

The age bands are:

- `18-29`
- `30-39`
- `40-49`
- `50-59`
- `60+`

### 3. Balance Bands

The original numerical `balance` variable is retained. Additional balance bands are created to represent broader ranges of customer account balance.

The balance bands are:

- `Negative`
- `0-999`
- `1000-4999`
- `5000-9999`
- `10000+`

This provides an additional representation of the customer's financial position for modelling.

### 4. Repeated Contact Flag

The `campaign` variable records the number of contacts performed during the current campaign.

A binary `repeated_contact_flag` is created:

- `1` = customer received more than one contact
- `0` = customer received one contact

The original `campaign` variable is retained for modelling.

## Modelling Feature Selection

### Exclusion of Contact Duration

The `duration` variable records the duration of the most recent contact with the customer.

Because this information is only known after the contact has taken place, including it could introduce information leakage relative to an early-prediction objective. The variable could therefore provide information that would not be available at the intended prediction point.

For this reason, `duration` is excluded from the primary modelling feature set.

The variable remains available in the preprocessed dataset for reference but is not passed to the modelling stage.

### One-Hot Encoding

Categorical predictor variables are converted into numerical representations using one-hot encoding.

The categorical variables encoded are:

- `job`
- `marital`
- `education`
- `default`
- `housing`
- `loan`
- `contact`
- `month`
- `poutcome`
- `age_band`
- `balance_band`

`drop_first=True` is used so that one category from each categorical variable acts as the reference category and redundant columns are avoided.

The target variable `y_binary` is already numerical and is therefore not encoded.

### Removal of Redundant Variables

The original text target variable `y` is removed because `y_binary` provides the required numerical binary representation.

The original `pdays` variable is also removed from the primary modelling dataset. The information it provides has already been represented by the engineered `previously_contacted` feature.

This prevents the modelling dataset from containing the missing-value representation of `pdays` while retaining the relevant information through the engineered feature.

## Final Validation

Before saving the modelling dataset, the notebook validates that:

- No non-numerical predictor columns remain.
- The target variable `y_binary` contains only `0` and `1`.
- No missing values remain.
- No infinite numerical values remain.
- The number of observations remains unchanged.
- The final dataset is suitable for the modelling stage.

The feature-engineering process produces **45,211 observations and 51 modelling columns**, including the binary target `y_binary`.

## Output

The final feature-engineered dataset is saved as:

`data/processed/bank_marketing_features.csv`

The notebook reloads the saved CSV to verify that it was written correctly and confirms the expected number of rows and columns, absence of missing values, and valid target values.

## Notebook

The feature-engineering code is contained in:

`feature_engineering/feature_engineering.ipynb`

## How to Use

1. Ensure `data/processed/bank_marketing_preprocessed.csv` has been created by the preprocessing notebook.
2. Open `feature_engineering/feature_engineering.ipynb` in Jupyter Notebook or JupyterLab.
3. Run the notebook cells from top to bottom.
4. The notebook will load the preprocessed dataset, create the engineered features, encode the categorical variables, remove variables that are not appropriate for the modelling objective, and validate the final dataset.
5. The resulting modelling dataset will be saved to:

   `data/processed/bank_marketing_features.csv`

6. Use `data/processed/bank_marketing_features.csv` as the input for the Logistic Regression and Gradient Boosting modelling notebooks.
