# Customer Segmentation Analysis Using RFM & K-Means

> **Oasis Infobyte Data Analytics Internship — Customer Segmentation Project**

## 📌 Project Overview

This project focuses on identifying groups of customers with similar purchasing behaviour using **RFM analysis and K-Means clustering**.

The analysis starts with transaction-level retail data and transforms it into customer-level behavioural profiles based on:

* **Recency** — how recently a customer made a purchase
* **Frequency** — how often a customer purchased
* **Monetary Value** — how much a customer spent

These behavioural features are then prepared for machine learning and used with **K-Means clustering** to identify distinct customer segments.

The project covers the complete analytical workflow, from initial data-quality assessment and cleaning to feature engineering, exploratory analysis, clustering, customer profiling, and business recommendations.

---

## Objectives

The main objectives of this project were to:

* Understand the structure and quality of the transaction dataset.
* Identify data issues that could affect customer-level analysis.
* Clean and prepare valid customer purchase records.
* Calculate customer-level RFM metrics.
* Calculate average purchase value and historical customer value.
* Explore the distributions of customer behavioural variables.
* Prepare the data for machine learning.
* Standardise the clustering features.
* Determine a suitable number of clusters using the Elbow Method.
* Apply K-Means clustering.
* Profile the resulting customer segments.
* Translate the segments into potential marketing strategies.

---

## 🗂️ Dataset

The project uses the **Online Retail** transaction dataset.

The original dataset contains:

* **541,909 transactions**
* **8 variables**
* **4,372 unique customers**
* **38 countries**
* Transaction dates ranging from **December 2010 to December 2011**

The main variables include:

| Column        | Description                      |
| ------------- | -------------------------------- |
| `InvoiceNo`   | Invoice / transaction identifier |
| `StockCode`   | Product identifier               |
| `Description` | Product description              |
| `Quantity`    | Quantity purchased               |
| `InvoiceDate` | Transaction date and time        |
| `UnitPrice`   | Price per unit                   |
| `CustomerID`  | Customer identifier              |
| `Country`     | Customer country                 |

The original dataset structure and summary were inspected before beginning the cleaning process.

---

# 1. Data Quality Assessment

Before cleaning the data, I first investigated which problems were actually present rather than removing records automatically.

The assessment identified:
<img width="548" height="283" alt="DataQuality Assessment " src="https://github.com/user-attachments/assets/cbf2a253-60ef-46d5-92ed-16603cb5ca3e" />

The most significant issue was the absence of `CustomerID` for almost one-quarter of the original transactions.

Because customer segmentation requires transactions to be attributed to identifiable customers, those records could not reliably contribute to the RFM analysis.

Missing product descriptions, however, did not directly affect the RFM calculations and therefore were not used as a reason to remove otherwise valid transactions.

---

# 2. Data Cleaning

The cleaning process focused specifically on records that could distort customer purchasing behaviour.

The following steps were applied:

1. Removed transactions without `CustomerID`.
2. Converted `CustomerID` from floating-point format to integer.
3. Removed duplicate records.
4. Removed cancelled invoices identified by invoice numbers beginning with `C`.
5. Removed transactions with non-positive quantities.
6. Removed transactions with non-positive unit prices.

After cleaning, validation checks confirmed that:

<img width="749" height="221" alt="Cleaned data " src="https://github.com/user-attachments/assets/4a0e5bb2-297a-4b73-a19e-6b33efb61879" />

The `Description` column was retained because missing descriptions did not affect the RFM calculations.

---

# 3. Transaction Value Engineering

After cleaning the transaction data, I created a `Total_Price` variable:

```text
Total_Price = Quantity × UnitPrice
```

This converts individual transaction quantities and prices into a transaction-level monetary value.

The new variable was then used to calculate total historical spending for each customer.

---

#4. RFM Analysis

The next step was to move from transaction-level data to customer-level behavioural analysis.

### Recency

Measures the number of days since the customer's most recent purchase.

Lower recency values indicate more recent purchasing activity.

### Frequency

Measures the number of unique invoices associated with the customer.

Higher frequency indicates more repeated purchasing activity.

### Monetary Value

Measures the customer's total historical spending during the observed period.

Higher monetary value indicates greater historical customer value.

Together, these three measures provide a behavioural profile of each customer.

---

# 📊 5. Additional Customer Metrics

To provide additional descriptive context, two additional metrics were calculated.

### Average Purchase Value

```text
Average Purchase Value =
Monetary Value / Frequency
```

This measures the typical historical value generated per purchase.

### Historical Customer Lifetime Value

The project uses total historical spending as a measure of historical customer value.

It is **not treated as a predictive Customer Lifetime Value model**, because the dataset covers a limited historical period.

---

#6. Distribution Analysis

Before applying K-Means, the distributions of the customer-level variables were examined.

The analysis showed substantial right-skewness, particularly in:

* Frequency
* Monetary Value

A relatively small number of customers had substantially higher purchasing activity and spending than the majority.

Because K-Means is sensitive to the scale and distribution of its input variables, this needed to be addressed before clustering.
<img width="1103" height="300" alt="Distribution" src="https://github.com/user-attachments/assets/c40713fb-806c-45ab-9db9-feafd684c237" />

A log transformation is therefore applied to Frequency and Monetary Value to reduce the effect of extreme values and produce a more balanced distribution before clustering.

<img width="1113" height="459" alt="image" src="https://github.com/user-attachments/assets/efae5681-8ac5-4778-a0a2-a9b21942bff6" />

---

# 🔧 7. Feature Preparation

The clustering features were prepared before applying K-Means.

The process included:

1. Selecting the RFM variables.
2. Examining their distributions.
3. Applying log transformation where appropriate to reduce the influence of extreme skewness.
4. Standardising the resulting features using `StandardScaler`.

The final standardised behavioural variables were then used as inputs to the clustering algorithm.

---

# 8. Choosing the Number of Clusters

The **Elbow Method** was used to evaluate different values of `K`.

The objective was to find a point where increasing the number of clusters produced diminishing improvements in within-cluster variation.

Based on the resulting analysis, **K = 4** was selected as a suitable clustering solution for this project.

<img width="788" height="475" alt="Elbow Method" src="https://github.com/user-attachments/assets/272c1796-4ef8-43c8-9b3f-0cc30a15e3af" />

---

# 9. K-Means Clustering

K-Means was then applied to the prepared RFM features.

The algorithm grouped customers according to similarities in their behavioural characteristics.

The resulting four clusters showed meaningful differences in:

* Recency
* Frequency
* Monetary Value
* Overall customer engagement
* Historical customer value
<img width="637" height="203" alt="Clusters" src="https://github.com/user-attachments/assets/23a5068a-8e79-4a44-8305-5b4e0cd7f8c8" />

---

# 10. Customer Segment Profiles

The resulting clusters were interpreted based on their behavioural characteristics.

### 🟢 Cluster 2 — High-Value & Highly Engaged Customers

These customers demonstrate the strongest combination of purchasing activity and historical value.

**Potential strategy:**

* Prioritise retention.
* Provide personalised offers.
* Encourage continued engagement.
* Explore loyalty-focused initiatives.

---

### 🔵 Cluster 3 — Active Mid-Value Customers

These customers remain active but have more moderate historical value.

**Potential strategy:**

* Encourage cross-selling.
* Introduce relevant product recommendations.
* Use upselling opportunities.
* Develop them toward higher-value behaviour.

---

### 🟡 Cluster 0 — Recent Low-Value Customers

These customers have purchased relatively recently but show lower purchasing frequency and spending.

**Potential strategy:**

* Encourage repeat purchases.
* Provide relevant product recommendations.
* Use targeted introductory offers where appropriate.
* Monitor whether purchasing behaviour strengthens over time.

---

### 🔴 Cluster 1 — At-Risk / Inactive Customers

These customers have gone the longest period since their last purchase and show relatively low purchasing activity.

**Potential strategy:**

* Launch targeted win-back campaigns.
* Use time-limited incentives.
* Highlight relevant products or new arrivals.
* Prioritise customers with stronger historical value when allocating campaign resources.

These recommendations are potential strategies based on observed customer profiles. Their actual effectiveness would need to be tested using campaign-response and customer-engagement data.

---

# 💡 Key Insights

The analysis demonstrated several important patterns in customer behaviour.

### 1. Customer value is highly uneven

A relatively small number of customers generate substantially higher historical spending than the typical customer.

### 2. Recency provides an important engagement signal

Customers with recent purchases can represent very different levels of value depending on their purchasing frequency and spending.

### 3. Frequency and Monetary Value are strongly skewed

The distributions showed that a small group of customers had exceptionally high purchasing activity and spending.

### 4. Customer segmentation provides more context than total sales alone

Instead of treating the customer base as one group, RFM and clustering reveal different behavioural profiles that can support more targeted strategies.

### 5. Different customer groups require different actions

High-value customers should primarily be retained, active mid-value customers can be developed, recent low-value customers can be encouraged to repeat, and inactive customers can be targeted through reactivation campaigns.

---

# What I Learned

This project was my first hands-on experience applying **machine learning for customer segmentation**.

The main concepts I developed were:

* Data quality assessment
* Data cleaning with pandas
* Feature engineering
* RFM analysis
* Distribution analysis
* Log transformation
* Feature standardisation
* `StandardScaler`
* K-Means clustering
* Elbow Method
* Cluster profiling
* Translating analytical results into business recommendations

One of the most important lessons was that machine learning does not begin with the algorithm.

A large part of the work happened before K-Means was ever applied:

```text
Raw Transactions
       ↓
Data Quality Assessment
       ↓
Cleaning
       ↓
Feature Engineering
       ↓
Customer-Level RFM
       ↓
Distribution Analysis
       ↓
Transformation
       ↓
Standardisation
       ↓
Cluster Selection
       ↓
K-Means
       ↓
Customer Segments
       ↓
Business Recommendations
```

---

# 🛠️ Tools & Technologies

* **Python**
* **pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **scikit-learn**
* **Jupyter Notebook**

---

# 📁 Repository Contents

```text
Customer_Segmentation/
│
├── Customer_Segmentation_RFM_KMeans.ipynb
└──README.md
```

---

# Future Improvements

Future analysis could extend this project by incorporating:

* Campaign-response data
* Customer tenure
* Revenue contribution by segment
* Segment-level profitability
* Predictive Customer Lifetime Value
* Customer churn modelling
* More advanced clustering techniques
* Validation of marketing strategies using actual campaign results

---

## 📌 Project Status

**Completed**

Developed as part of my **Oasis Infobyte Data Analytics Internship** and documented as a portfolio project demonstrating an end-to-end customer analytics and machine-learning workflow.

