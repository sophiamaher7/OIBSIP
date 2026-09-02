# Retail Sales Exploratory Data Analysis

## Project Overview

This project was completed as part of the **Oasis Infobyte Data Analytics Internship**. The objective was to perform Exploratory Data Analysis (EDA) on a retail sales dataset to identify patterns in sales performance, customer behavior, and product demand.

The analysis covers data cleaning, descriptive statistics, time-based sales analysis, customer demographics, product performance, category revenue, correlation analysis, and business insights.

## Objectives

* Inspect and understand the structure and quality of the dataset
* Clean and prepare the data for analysis
* Analyze monthly and quarterly sales trends
* Explore customer demographics and transaction activity
* Identify the top-selling products
* Compare revenue across product categories
* Analyze relationships between numerical variables
* Generate actionable business insights and recommendations

## Dataset

The dataset contains retail transaction records covering **2022–2023**, including information about:

* Transaction ID
* Sale Date and Time
* Customer ID
* Gender
* Age
* Product Category
* Product Name
* Quantity
* Price per Unit
* Cost of Goods Sold (COGS)
* Total Sale

## Data Preparation

The data was cleaned and prepared using **Python and pandas**. The main steps included:

* Standardizing column names
* Correcting column naming inconsistencies
* Converting dates and times to appropriate data types
* Converting ID fields to text
* Handling missing values
* Removing rows with missing core sales information
* Validating sales calculations
* Checking for invalid values and duplicates
* Creating additional analytical features such as age groups, months, and quarters

After cleaning, the dataset contained **1,997 valid transactions with no missing values or duplicate records**.

## Analysis & Visualizations

The following analyses were performed:

1. **Descriptive Statistics**
2. **Monthly Sales Trends**
3. **Quarterly Sales Trends**
4. **Customer Age Group Analysis**
5. **Gender Distribution**
6. **Top 10 Best-Selling Products**
7. **Revenue by Category**
8. **Correlation Heatmap**
9. **Average Transaction Value by Age Group**

## Key Findings

* Sales consistently increase during the **September–December period**, with Q4 recording the strongest performance in both years.
* Customers aged **26–55 account for the largest share of transaction activity**.
* The **18–25 age group has the lowest transaction volume but the highest average transaction value**.
* Demand is relatively distributed across the top 10 products rather than being dominated by a single product.
* **Electronics generates the highest category revenue**, although revenue is relatively balanced across Electronics, Clothing, and Beauty.
* **Price per Unit has the strongest positive relationship with Total Sale**, while customer age shows little linear relationship with transaction value.
* Transaction volume alone does not fully represent customer value, highlighting the importance of analyzing both **frequency and transaction value**.

## Business Recommendations

* Prepare inventory, staffing, and promotional campaigns ahead of the recurring **Q4 sales peak**.
* Increase engagement among younger customers through targeted digital campaigns, loyalty programs, and personalized offers.
* Maintain strong retention strategies for the core **26–55 customer segments**.
* Distribute inventory planning across multiple high-demand products rather than relying on a single best-selling product.
* Continue supporting all major product categories while identifying opportunities to increase the contribution of Beauty.
* Use pricing and product-mix strategies to improve transaction value while monitoring customer purchasing behavior.

## Tools & Technologies

* **Python**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **Jupyter Notebook**

## Project Files

* `Retail_Sales_EDA.ipynb` — Complete analysis and visualizations
* `retail_sales_dataset.csv` — Dataset used for the analysis

## Author

**Sophia Maher**

Data Analytics Internship — Oasis Infobyte


