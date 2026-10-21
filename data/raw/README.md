# STADIOEquities — First-Deposit Activation: Data Extract

Six tables covering customers registered between January 2024 and August 2025, supplied against the Part C data request. Join every table on `customer_id`. Datetimes are `yyyy-MM-dd HH:mm:ss`; all monetary values are in ZAR. Nulls are empty fields.

## Files

### `table1_customer_acquisition.csv`
Customer registration, demographic and acquisition-channel baseline.  
Rows: 2,418

| Column | Description |
|---|---|
| `customer_id` | String |
| `registration_date` | Datetime |
| `age` | Integer |
| `region_province` | Categorical |
| `investment_goal` | Categorical |
| `risk_appetite` | Categorical |
| `acquisition_channel` | Categorical |
| `campaign_id` | Categorical |
| `acquisition_cost_zar` | Numeric |

### `table2_kyc_onboarding.csv`
KYC status and furthest onboarding step reached per customer.  
Rows: 2,411

| Column | Description |
|---|---|
| `customer_id` | String |
| `kyc_status` | Categorical |
| `kyc_completion_date` | Datetime |
| `onboarding_step_reached` | Categorical |
| `step_status` | Categorical |
| `time_spent_on_step_minutes` | Numeric |
| `failure_reason` | Categorical |

### `table3_app_web_behaviour.csv`
Session-level app and web activity.  
Rows: 14,196

| Column | Description |
|---|---|
| `customer_id` | String |
| `session_date` | Datetime |
| `platform` | Categorical |
| `session_duration_seconds` | Integer |
| `screens_viewed` | Integer |
| `deposit_page_viewed` | Integer |
| `deposit_attempt` | Integer |
| `features_used` | String |
| `days_since_registration` | Integer |

### `table4_funding_deposits.csv`
First-deposit outcome, method and transaction status. Primary outcome table.  
Rows: 2,411

| Column | Description |
|---|---|
| `customer_id` | String |
| `first_deposit_date` | Datetime |
| `first_deposit_amount_zar` | Numeric |
| `deposit_attempt` | Integer |
| `transaction_status` | Categorical |
| `failure_reason` | Categorical |
| `deposit_method` | Categorical |
| `time_to_first_deposit_days` | Numeric |

### `table5_marketing_engagement.csv`
Marketing and nudge communications with open/click/response outcomes.  
Rows: 13,223

| Column | Description |
|---|---|
| `customer_id` | String |
| `campaign_id` | Categorical |
| `message_date` | Datetime |
| `message_channel` | Categorical |
| `message_opened` | Integer |
| `message_clicked` | Integer |
| `nudge_type` | Categorical |
| `nudge_response` | Integer |
| `days_after_registration` | Integer |

### `table6_customer_support.csv`
Support tickets logged, with response and resolution times.  
Rows: 1,387

| Column | Description |
|---|---|
| `customer_id` | String |
| `ticket_date` | Datetime |
| `ticket_reason` | Categorical |
| `issue_type` | Categorical |
| `response_time_hours` | Numeric |
| `resolution_time_hours` | Numeric |
| `resolution_status` | Categorical |
| `deposit_related_indicator` | Integer |

## Data quality notes

This is an extract from live operational systems and has **not** been cleaned. Expect:

- Missing values in optional / conditionally-populated fields
- Inconsistent casing and stray whitespace in some free-text and categorical fields
- A small number of duplicate records
- Occasional out-of-range or implausible values from data-capture errors
- Some date fields captured in inconsistent formats

**Outcome:** derive activation from `table4_funding_deposits.csv` — a customer is activated where `transaction_status = Successful` and `time_to_first_deposit_days` falls inside your chosen window.

_Synthetic data supplied for the CAP182 capstone project. Not real client data._