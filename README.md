# CAP182_STADIOEquities_first-deposit-activation-project
Data science project investigating first-deposit activation at STADIOEquities, identifying factors associated with customer activation and informing targeted onboarding interventions.
# CAP182 STADIOEquities First-Deposit Activation Project

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
| `data/` | Data requirements and datasets |
| `preprocessing/` | Data cleaning and preparation |
| `feature_engineering/` | Creation and transformation of modelling features |
| `models/` | Machine learning models |
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
