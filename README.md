# CAP182_STADIOEquities_first-deposit-activation-project

Data science project investigating first-deposit activation at STADIOEquities, identifying factors associated with customer activation and informing targeted onboarding interventions.

# STADIOEquities First-Deposit Activation Project

This project investigates the customer activation challenge at STADIOEquities, with a specific focus on the transition from registration to first deposit. The project progresses from defining the business problem and requesting the required data to developing, evaluating and comparing machine-learning models using a proxy dataset.

---

# SS1 – Project Definition

## Part A – Motivation

### 1. Industry and Business Context

STADIOEquities is a South African digital investment platform that aims to make investing accessible to a broad population by lowering traditional barriers to entry. Through this approach, the company has grown to approximately 2.3 million registered accounts. Despite this growth, only 760,000 accounts are funded and active, while 41% of registered accounts have never deposited funds. This indicates a substantial gap between customer acquisition and customer activation.

### 2. Business Problem

The inability to convert registered users into funded and active clients represents a significant business challenge. Customer acquisition costs are only recovered once an account becomes active, while most of STADIOEquities' revenue streams are dependent on clients funding their accounts and remaining engaged with the platform. Furthermore, the sign-up-to-first-deposit conversion rate has declined from 64% to 59% over the past two years, suggesting that customer activation is becoming increasingly difficult.

### 3. Importance of the Problem

This problem is important because it directly affects business growth, customer lifetime value, and the organisation's ability to generate sustainable revenue from its existing customer base. It also aligns with STADIOEquities' 2030 strategic objective of activating more existing accounts and improving long-term customer engagement. Addressing the activation gap could therefore improve the effectiveness of customer acquisition investments while contributing to increased platform usage and revenue generation.

### 4. Data Science Opportunity

Advances in data science and machine learning provide an opportunity to better understand customer activation behaviour. STADIOEquities collects extensive customer, onboarding, behavioural, funding, marketing and support data throughout the customer journey. However, despite operating in a data-rich environment, activation efforts are currently based on a largely standardised onboarding process rather than customer-specific insights.

By analysing patterns in historical customer behaviour, machine learning techniques can be used to identify the characteristics and behaviours associated with successful activation, as well as customers who may be at risk of failing to make a first deposit. This would enable STADIOEquities to move from a one-size-fits-all onboarding approach towards more personalised and timely interventions.

### 5. Value of the Study

The findings of this study could help STADIOEquities identify customers who need support during the onboarding process and improve customer activation rates. This could reduce the number of never-funded accounts and help the organisation gain greater value from its existing customer base.

Increased activation may also contribute to higher customer lifetime value and sustainable revenue growth. Furthermore, the study will demonstrate how data science can be used to address a real-world business challenge while supporting STADIOEquities' goal of growing its active client base.

---

## Part B – Problem Statement

### 1. The Problem

STADIOEquities faces a customer activation challenge in which 41% of registered accounts have never been funded. Each registration costs approximately R180 to acquire, and this cost is only recovered once a customer activates by making a deposit. While the organisation collects extensive customer, onboarding, behavioural, marketing and support data, it has limited insight into which customers are likely to activate and which are likely to stall before making their first deposit.

As a result, activation efforts are largely applied uniformly rather than being guided by customer-specific behaviour and characteristics. This limits STADIOEquities' ability to convert registrations into funded investors, maximise the value of its customer acquisition investment and support the growth of its active client base.

### 2. Who Is Affected

The problem affects STADIOEquities' customer acquisition, onboarding and customer-service functions, as well as registered customers who do not progress to becoming funded investors.

### 3. What Is Unknown

It is not sufficiently understood which customer characteristics and behaviours are associated with failing to make a first deposit. Potential factors include onboarding progress, app/web behaviour, acquisition source, demographics, marketing interactions and customer-service interactions.

### 4. Data to Be Used

The study will use available customer demographic, account and funding, app/web behaviour, onboarding, marketing and customer-support data to examine differences between customers who activate and those who remain unfunded.

### 5. Data Science Problem

The study will analyse historical customer data to identify patterns and factors associated with first-deposit activation. The outcome can be defined as whether a registered customer makes a first deposit within a specified activation period.

### 6. Research Question

**To what extent can STADIOEquities' customer, onboarding, behavioural, marketing and support-service data be used to identify factors associated with first-deposit activation and inform interventions that may encourage registered customers to make their first deposit?**

---

## Part C – Data Request

The detailed data requirements are provided in the data request document located in the `data/` folder.

---

## Part D – Repository Structure

| Folder | Purpose |
|---|---|
| `data/` | Data requirements, datasets and project reports |
| `preprocessing/` | Data cleaning and preparation |
| `feature_engineering/` | Creation and transformation of modelling features |
| `models/` | Machine-learning models |
| `evaluation/` | Model evaluation |
| `statistical_analysis/` | Statistical helper and comparison scripts |
| `visualisation/` | Visualisation scripts |
| `results/` | Experimental results, figures and tables |

### Project Workflow

Data Collection → Data Validation → Data Preprocessing → Feature Engineering → Exploratory Data Analysis → Model Development → Model Evaluation → Results → Recommendations

---

## Part E – RAAIDD Log

| Category | Description / Log Entries |
|---|---|
| **Risks** | **1.** Customer ID inconsistencies may prevent reliable integration of customer, onboarding, behavioural, funding, marketing and support datasets required for activation modelling.<br><br>**2.** Incorrect activation classification may occur if First Deposit Date or Transaction Status records are incomplete, resulting in mislabelled target variables.<br><br>**3.** Limited predictive value of behavioural variables may reduce the model's ability to identify factors associated with first-deposit activation.<br><br>**4.** Class imbalance between activated and never-funded customers may bias model performance and reduce predictive accuracy.<br><br>**5.** Missing or incomplete marketing and support data may limit investigation of whether customer engagement activities influence activation outcomes. |
| **Actions** | **1.** Obtain the six STADIOEquities datasets specified in Part C and verify field availability and historical coverage.<br><br>**2.** Conduct data-quality assessments, including completeness, consistency, duplicate-record and missing-value analysis.<br><br>**3.** Integrate datasets using Customer ID to create a unified customer-level analytical dataset.<br><br>**4.** Define and validate the first-deposit activation outcome variable.<br><br>**5.** Perform exploratory data analysis and feature engineering using customer, onboarding, behavioural, funding, marketing and support data.<br><br>**6.** Develop, train and evaluate an appropriate machine-learning model.<br><br>**7.** Interpret the results and formulate recommendations to improve customer activation rates. |
| **Assumptions** | **1.** Customer IDs are consistently recorded across all six datasets, enabling accurate dataset integration.<br><br>**2.** First Deposit Date and Transaction Status accurately represent customer activation status.<br><br>**3.** Behavioural variables such as session activity, onboarding progress and deposit attempts contain meaningful indicators of activation likelihood.<br><br>**4.** Four to six years of historical data provides a sufficiently large sample for robust analysis.<br><br>**5.** Historical activation patterns are broadly representative of future customer activation behaviour.<br><br>**6.** No major changes to onboarding processes occurred during the study period that would materially distort activation patterns. |
| **Issues** | **1.** The STADIOEquities datasets not being received timely or not received at all. This will result in data completeness, linkage success and feature availability not being verified. This will be addressed once access to the datasets is obtained. |
| **Decisions** | **1.** First-deposit activation will be used as the target variable because it directly addresses the business problem of reducing the proportion of never-funded accounts and improving sign-up-to-deposit conversion.<br><br>**2.** A supervised machine-learning approach will be used because activation status is a known outcome that can be predicted using historical customer data. |
| **Dependencies** | **1.** Data quality assessment depends on dataset acquisition. The STADIOEquities datasets must be received before their completeness, accuracy and consistency can be evaluated.<br><br>**2.** Dataset integration depends on data quality assessment. The datasets must be validated and Customer ID consistency confirmed before they can be combined into a single customer view.<br><br>**3.** Feature engineering depends on dataset integration. Customer, onboarding, behavioural, funding, marketing and support data must be combined before meaningful variables can be created for analysis.<br><br>**4.** Model development depends on feature engineering. The activation outcome and predictor variables must be prepared before a machine-learning model can be developed and evaluated.<br><br>**5.** Recommendations depend on model evaluation. Recommendations for improving first-deposit activation can only be made after the model results have been analysed and the key factors influencing activation have been identified. |

---

# SS2 – Data Science Project

## Part A – Literature Review and Dataset Selection

The literature review investigated the use of machine-learning techniques for customer response, conversion and take-up prediction.

Three related studies were reviewed:

1. **Verster et al. (2021)** – prediction of home-loan take-up using tree-based ensemble models.
2. **Breed and Verster (2017)** – customer-response prediction and segmentation in a South African banking context.
3. **Moro, Cortez and Rita (2014)** – prediction of bank telemarketing success using the Bank Marketing dataset.

The **UCI Bank Marketing dataset** was selected as a structural proxy dataset because the actual STADIOEquities customer data requested in SS1 was not available for the modelling stage.

### Part A Report

[View the Part A Literature Review and Dataset Selection Report](data/CAP182%20-%20SS2%20-PART%20A.pdf)

### Proxy Dataset

The modelling dataset used in SS2 is the UCI Bank Marketing `bank-full.csv` dataset. It contains 45,211 observations and was used only as a proxy for demonstrating the data-science workflow.

The proxy dataset should not be interpreted as STADIOEquities customer data.

---

# SS2 Part B – Data Science Implementation

Part B implements the complete modelling workflow through separate preprocessing, feature-engineering and model-development stages.

## 1. Data Preprocessing

### Documentation

[Preprocessing Documentation](Preprocessing.MD)

### Code

[`preprocessing/preprocessing.ipynb`](preprocessing/preprocessing.ipynb)

The preprocessing stage loads the raw Bank Marketing dataset, performs data-quality checks, handles the `pdays = -1` representation, creates the binary target variable and produces the preprocessed dataset.

### Data

- Raw dataset: `data/raw/bank-full.csv`
- Preprocessed dataset: `data/processed/bank_marketing_preprocessed.csv`

---

## 2. Feature Engineering

### Documentation

[Feature Engineering Documentation](FeatureEngineering.MD)

### Code

[`feature_engineering/feature_engineering.ipynb`](feature_engineering/feature_engineering.ipynb)

The feature-engineering stage creates additional modelling variables, including:

- `previously_contacted`
- `age_band`
- `balance_band`
- `repeated_contact_flag`

Categorical variables are one-hot encoded and the final modelling dataset is prepared for machine learning.

### Data

`data/processed/bank_marketing_features.csv`

---

## 3. Model 1 – Logistic Regression

### Documentation

[Model 1 Documentation](Model1.MD)

### Code

[`models/logistic_regression.ipynb`](models/logistic_regression.ipynb)

Logistic Regression was implemented as the first classification model.

The workflow uses:

- 80/20 stratified train-test split
- `random_state = 42`
- StandardScaler
- Logistic Regression
- 5-fold StratifiedKFold cross-validation
- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Held-out test evaluation

---

## 4. Model 2 – Gradient Boosting

### Documentation

[Model 2 Documentation](Model2.MD)

### Code

[`models/gradient_boosting.ipynb`](models/gradient_boosting.ipynb)

Gradient Boosting was implemented as the second classification model.

The workflow uses:

- 80/20 stratified train-test split
- `random_state = 42`
- GradientBoostingClassifier
- 5-fold StratifiedKFold cross-validation
- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Held-out test evaluation

---

# SS2 Part C – Model Performance Evaluation

Model performance was evaluated using a consistent evaluation framework for both models.

The evaluation process uses the same stratified 80/20 train-test split and 5-fold cross-validation approach. Both models are evaluated using Accuracy, Precision, Recall, F1-score and ROC-AUC.

## Model 1 Performance

[Model 1 Performance Evaluation](Model1Performance.MD)

## Model 2 Performance

[Model 2 Performance Evaluation](Model2Performance.MD)

## Model Comparison

[Model Performance Comparison](Comparison.MD)

## Evaluation Code

[`evaluation/evaluation.ipynb`](evaluation/evaluation.ipynb)

The evaluation notebook reconstructs both deterministic models using the same feature-engineered dataset, train-test split and random state used during model development. It then calculates and compares the performance metrics and confusion matrices.

---

# SS2 Part D – Client Report

Part D provides the client-facing interpretation of the modelling results and addresses:

1. Model selection
2. Model improvement
3. Adaptation of the selected model to actual STADIOEquities data
4. Alignment of the results with the related literature

### Part D Report

[View the Part D Client Report](data/CAP182%20-%20SS2%20-PART%20D.pdf)

Gradient Boosting achieved the higher held-out test performance across the reported evaluation metrics and was therefore identified as the model for further development. The report also highlights the relatively low recall and the need for further refinement before applying the approach to actual STADIOEquities data.

---

# SS2 Repository Structure

```text
CAP182_STADIOEquities_first-deposit-activation-project/
│
├── README.md
│
├── data/
│   ├── raw/
│   │   └── bank-full.csv
│   │
│   ├── processed/
│   │   ├── bank_marketing_preprocessed.csv
│   │   └── bank_marketing_features.csv
│   │
│   ├── CAP182 - SS2 -PART A.pdf
│   ├── CAP182 - SS2 -PART D.pdf
│   └── [SS1 data request document]
│
├── preprocessing/
│   └── preprocessing.ipynb
│
├── feature_engineering/
│   └── feature_engineering.ipynb
│
├── models/
│   ├── logistic_regression.ipynb
│   └── gradient_boosting.ipynb
│
├── evaluation/
│   └── evaluation.ipynb
│
├── Preprocessing.MD
├── FeatureEngineering.MD
├── Model1.MD
├── Model2.MD
├── Model1Performance.MD
├── Model2Performance.MD
└── Comparison.MD
