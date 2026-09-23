# 📊 Supply Chain Analysis Dashboard — Python, Pandas & Power BI

An end-to-end **supply chain analysis project** focused on analyzing order delivery performance, shipping delays, profitability, customer segments, product categories, and regional trends using the **DataCo Smart Supply Chain dataset**.

The project follows a practical **Data Analytics and Business Intelligence workflow**, starting with raw CSV data, followed by **Python-based data cleaning and exploratory data analysis (EDA)**, and ending with an interactive **Power BI dashboard**.

The analysis focuses on identifying delivery delays, understanding their distribution across regions, evaluating profitability across different business dimensions, and providing an interactive view of overall supply chain performance.

---

## 📊 Dashboard Overview

An interactive **Power BI dashboard** was developed to provide a comprehensive overview of delivery performance, profitability, shipping time, customer segments, product categories, and regional delays.

### 📸 Dashboard Preview
![Supply Chain Analysis Dashboard](dashboard.png)

The dashboard combines key supply chain KPIs with multiple visualizations to help users explore delivery and profitability patterns interactively.

### 📌 Dashboard KPIs

* **Total Profit**
* **Total Orders**
* **Approximate Cost**
* **On-Time Deliveries %**
* **Late Deliveries**

---

## Business Questions

The analysis was designed to answer the following business questions:

* What percentage of orders are delivered late?
* Which regions have the highest number of delayed orders?
* How are delivery delays distributed across orders?
* How does shipping time relate to order profitability?
* Which customer segments generate the most profit?
* Which product categories generate the highest and lowest profit?
* What proportion of orders are profitable, loss-making, or break-even?
* How are orders distributed across different delivery statuses?
* Where are delivery delays most prominent?
* Are longer shipping times associated with lower profitability?

---

## 🔄 Project Workflow

### 1. Data Source

The project uses the publicly available **DataCo Smart Supply Chain dataset**, which contains order, shipping, sales, customer, product, and delivery-related information.

The raw data was provided in CSV format and served as the primary source for the analysis.

### 2. Python — Data Cleaning & Preparation

Python was used to clean and prepare the raw dataset before analysis.

The data preparation process included:

* Inspecting the dataset structure
* Checking missing values
* Checking duplicate records
* Handling data types
* Cleaning inconsistent values
* Creating derived columns
* Preparing delivery-related features
* Preparing profitability-related features
* Validating the cleaned dataset

### 📌 Derived Columns

Several analytical columns were created during data preparation, including:

* `Delay`
* `Is_Delayed`
* `order_month`
* `order_hour`
* `order_day`
* `Profitibility Flag`

The `Delay` column was used to analyze whether orders were delivered early/on time or late.

### Delivery Delay Logic

```text
Delay <= 0  →  On Time / Early
Delay > 0   →  Late
```

---

## 3. Python — Exploratory Data Analysis

Python was also used for **Exploratory Data Analysis (EDA)** to understand patterns and relationships within the supply chain data before developing the Power BI dashboard.

The EDA focused on:

* Delivery delay patterns
* Regional delivery performance
* Shipping time
* Order profitability
* Profitability distribution
* Customer segment performance
* Product category profitability
* Delivery status distribution

### 📌 Python Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

EDA visualizations were used to identify important trends and determine which metrics and dimensions would be most useful in the final Power BI dashboard.

---

## 4. Power BI — Dashboard Development

The cleaned dataset was imported into **Power BI Desktop** to create an interactive supply chain performance dashboard.

The dashboard combines delivery, profitability, regional, customer, and product-level analysis.

### 📊 Dashboard Visualizations

#### Order Profit by Shipping Time

Shows the relationship between actual shipping time and order profitability, helping identify whether shipping duration is associated with changes in average profit.

#### Delay Orders by Region

Compares delayed order counts across different order regions to identify regions experiencing higher delivery delays.

#### Delay Distribution

Displays the distribution of delivery delays in days, including early, on-time, and late orders.

#### Order Count by Delivery Status

Shows the number of orders across different delivery status categories.

#### Profitability Distribution

Breaks orders down into:

* Profit
* Loss
* Break-even

using the `Profitibility Flag`.

#### Order Profit by Customer Segment

Compares total order profit across customer segments.

#### Category-wise Profitability

Compares total profit across product categories to identify stronger and weaker performing categories.

---

## 🧮 Key DAX Measures

### Total Profit

```DAX
Total Profit =
SUM('DataCo_Cleaned'[Order Profit Per Order])
```

### Total Orders

```DAX
Total Orders =
COUNTROWS('DataCo_Cleaned')
```

### Late Deliveries

```DAX
Late Deliveries =
CALCULATE(
    COUNTROWS('DataCo_Cleaned'),
    'DataCo_Cleaned'[Delay] > 0
)
```

### On-Time Delivery %

```DAX
On Time % =
1 - DIVIDE(
    [Late Deliveries],
    [Total Orders]
)
```

### Late Delivery %

```DAX
Late Delivery % =
DIVIDE(
    [Late Deliveries],
    [Total Orders]
)
```

### Approximate Cost

```DAX
Approx Cost =
SUM('DataCo_Cleaned'[Sales])
-
SUM('DataCo_Cleaned'[Order Profit Per Order])
```

> **Note:** `Approx Cost` is an estimated cost measure because the dataset does not provide a direct total logistics/cost field.

---

## 📌 Dashboard Filters

The dashboard includes interactive slicers for:

* **Product Name**
* **Order Region**

These filters allow users to explore delivery and profitability performance for specific products and regions.

---

# 💡 Key Business Insights

## 1. High Delivery Delay Rate

Approximately **55% of orders arrive late** relative to the scheduled shipping window.

This indicates that delivery performance is an important area for further supply chain investigation.

---

## 2. Regional Differences in Delays

The number of delayed orders varies across regions.

This allows supply chain teams to identify regions with relatively higher delivery delay volumes and investigate potential operational differences.

---

## 3. Profitability Varies Across Categories

Product categories show different levels of profitability, with some categories generating substantially higher profit while others show lower or negative profitability.

This provides an opportunity to investigate pricing, product costs, demand, and operational factors affecting category performance.

---

## 4. Customer Segments Contribute Differently

Different customer segments contribute different amounts of total order profit.

Comparing customer segments helps identify where profitability is concentrated and provides a basis for further customer-level analysis.

---

## 5. Shipping Time and Profitability

The shipping-time analysis shows that shipping duration does not always have a direct relationship with order profitability.

This suggests that profitability may also depend on other factors such as product category, sales value, order characteristics, and customer segment.

> **Note:** The insights above represent overall dataset-level observations. Results may change when dashboard filters are applied.

---

## 🗂️ Dataset

This project uses the **DataCo Smart Supply Chain dataset**.

The project includes both the original and cleaned datasets used throughout the Python analysis and Power BI dashboard.

### Dataset Files

The datasets are provided inside:

```text
data.zip
```

The ZIP file contains:

* **`DataCoSupplyChainDataset.csv`** — Original raw DataCo Smart Supply Chain dataset
* **`DataCo_Cleaned.csv`** — Cleaned and prepared dataset used for exploratory data analysis and Power BI dashboard development

> The datasets are compressed into `data.zip` to reduce repository size and make downloading easier.

---

## 📁 Project Structure

```text
Supply-Chain-Analysis/
│
├── README.md
├── dashboard.png
├── supply_chain_analysis.ipynb
├── Supply Chain Analysis.pbix
└── data.zip
`
---

### 3. Explore the Python Analysis

Open:

```text
supply_chain_analysis.ipynb
```

The notebook contains the Python-based:

* Data cleaning
* Data preparation
* Feature engineering
* Exploratory data analysis
* Data visualization


### 4. Explore the Dashboard

Use the available **Product Name** and **Order Region** filters to interact with the dashboard and explore different supply chain patterns.

---

## 🛠️ Tools & Technologies

* **Python**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **Microsoft Power BI**
* **DAX**
* **CSV**

---

## 🔄 Complete Project Pipeline

```text
Raw DataCo Dataset
        ↓
CSV Data
        ↓
Python Data Cleaning
        ↓
Feature / Derived Column Creation
        ↓
Exploratory Data Analysis
        ↓
Cleaned CSV Dataset
        ↓
Power BI Data Import
        ↓
DAX Measures
        ↓
Interactive Dashboard
        ↓
Supply Chain Insights
```

---

## 🎯 Project Goal

The primary goal of this project is to demonstrate an end-to-end **data analytics workflow** for evaluating supply chain delivery performance and profitability.

The project demonstrates how **Python and Power BI** can be combined to transform raw supply chain data into meaningful business insights.

The analysis provides a framework for:

* Monitoring delivery performance
* Identifying regional delay patterns
* Evaluating profitability
* Comparing customer segments
* Analyzing product categories
* Understanding shipping-time patterns
* Supporting data-driven supply chain decisions

