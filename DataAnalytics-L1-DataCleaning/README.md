# Task 3 — Data Cleaning: Financial Transactions

## Project Overview

This project was completed as part of the Oasis Infobyte Internship (OIBSIP).

The objective was to take a deliberately messy financial transactions dataset
and transform it into a clean, consistent, and analysis-ready dataset using
Python.

The project focuses on identifying data quality issues, making appropriate
cleaning decisions, documenting those decisions, and validating the final
dataset.

---

## Dataset

**Dataset:** Dirty Financial Transactions Dataset

**Source:** Kaggle

The dataset contains 100,000 financial transaction records and 8 columns.

### Columns

- Transaction_ID
- Transaction_Date
- Customer_ID
- Product_Name
- Quantity
- Price
- Payment_Method
- Transaction_Status

---

## Tools & Technologies

- Python
- Pandas
- NumPy
- Jupyter Notebook

---

## Data Quality Issues Identified

The initial dataset contained several data quality problems, including:

- Missing values
- Duplicate records
- Incorrect data types
- Invalid date values
- Inconsistent product names
- Inconsistent payment method formatting
- Inconsistent transaction status values
- Negative quantities and prices requiring investigation
- Currency symbols and formatting issues in the Price column

---

## Data Cleaning Process

### 1. Data Quality Assessment

The dataset was inspected using:

- Shape
- Data types
- Missing-value counts
- Duplicate counts
- Unique-value analysis
- Descriptive statistics
- Range checks

A data quality report was created to document the initial condition of the dataset.

### 2. Duplicate Removal

Duplicate records were identified and removed before performing imputation so that
duplicate observations would not influence calculated medians or modes.

A total of **994 duplicate rows** were removed.

### 3. Missing Data Handling

Different strategies were applied according to the meaning of each column.

- **Transaction_ID:** Rows with missing transaction IDs were removed because the
  identifier cannot be reliably reconstructed.
- **Transaction_Date:** Missing and invalid dates were converted to missing
  datetime values and replaced with the median valid transaction date.
- **Customer_ID:** Missing values were replaced with `"Unknown"`.
- **Quantity:** Missing values were imputed using the median.
- **Price:** Missing prices were first imputed using the median price for the
  corresponding product, with the overall median used as a fallback.
- **Transaction_Status:** Missing values were replaced with the mode.
- **Product_Name / Payment_Method:** No missing-value imputation was required.

### 4. Standardisation

Inconsistent categorical values were standardised.

Examples include:

- Product name variations and truncated values
- `"credit card"`, `"creditcard"` → `"Credit Card"`
- `"pay pal"`, `"paypal"` → `"PayPal"`
- `"complete"`, `"completed"` → `"Completed"`

Transaction dates were converted to the appropriate datetime format.

### 5. Value Range Anomalies

Negative quantities and prices were identified as unusual values.

They were not automatically changed or removed because the dataset does not
provide enough business context to determine whether they represent errors,
returns, refunds, reversals, or transaction adjustments.

Therefore, these values were retained and documented as potential anomalies.

### 6. Outlier Detection

The IQR method was used to identify statistical outliers in numerical columns.

Statistical outliers were retained because an unusually large or small
transaction may still represent a legitimate observation.

### 7. Data Type Correction

Data types were corrected according to the meaning of each column:

- IDs → string
- Transaction_Date → datetime
- Quantity → integer
- Price → float
- Categorical fields → string

---

## Before vs After

| Metric | Before Cleaning | After Cleaning |
|---|---:|---:|
| Row Count | 100,000 | 94,040 |
| Total Missing Values | 69,971 | 0 |
| Duplicate Rows | 994 | 0 |
| Dtype Accuracy | 0% | 100% |

Approximately **94% of the original records were preserved**, while the
identified data quality issues were addressed.

---

## Key Takeaways

This project demonstrated that data cleaning is not simply about removing
missing or unusual values.

The main focus was on understanding the meaning of each variable and choosing
a cleaning strategy that improves data quality while preserving useful
information.

In particular, unusual values were not automatically treated as errors.
Potential anomalies were investigated and retained when the available data did
not provide enough evidence to justify changing or removing them.

---

## Output

The cleaned dataset is provided as:

`financial_transactions_cleaned.csv`

The complete cleaning process and decisions are documented in:

`Data_Cleaning_Financial_Transactions.ipynb`
