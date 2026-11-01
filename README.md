# Customer Shopping Behavior Analysis

An end-to-end data analytics project: Python (EDA and cleaning) → PostgreSQL (business analysis) → Power BI (interactive dashboard) → written report with recommendations.

---

## Table of Contents
1. [Overview](#overview)
2. [Dataset](#dataset)
3. [Tools & Technologies](#tools--technologies)
4. [Project Workflow](#project-workflow)
5. [Dashboard](#dashboard)
6. [Key Results](#key-results)
7. [Business Recommendations](#business-recommendations)
8. [Repository Structure](#repository-structure)
9. [How to Run](#how-to-run)
10. [Future Improvements](#future-improvements)

---

## Overview

This project analyzes **3,900 retail transactions** to understand spending patterns, customer segments, product preferences, and subscription behavior. The goal is to turn raw purchase data into insights that support marketing, pricing, and loyalty decisions.

**Skills demonstrated:** data cleaning, exploratory analysis, feature engineering, SQL (aggregations, CTEs, window functions), database integration, dashboarding, and business storytelling.

---

## Dataset

| Item | Detail |
|---|---|
| File | `customer_shopping_behavior.csv` |
| Rows | 3,900 |
| Columns | 18 (17 after cleaning, plus 2 engineered features) |
| Missing data | 37 values in `Review Rating` |

**Column groups**
- **Demographics:** Customer ID, Age, Gender, Location, Subscription Status
- **Purchase details:** Item Purchased, Category, Purchase Amount (USD), Size, Color, Season
- **Behavior:** Discount Applied, Promo Code Used, Previous Purchases, Frequency of Purchases, Review Rating, Shipping Type, Payment Method

---

## Tools & Technologies

| Purpose | Tool |
|---|---|
| Data cleaning & EDA | Python, pandas, NumPy, Jupyter Notebook |
| Database connection | SQLAlchemy, psycopg2 |
| Data analysis | PostgreSQL (pgAdmin) |
| Visualization | Power BI |
| Reporting | PDF report |

---

## Project Workflow

### 1. Data loading & EDA (Python)
- Loaded the CSV with pandas
- Inspected structure with `df.info()`, `df.describe()`, `df.shape`

### 2. Data cleaning & feature engineering
- Filled missing `Review Rating` values with the **median rating of each product category**
- Standardized column names to `snake_case`
- Created **`age_group`** (Young Adult, Adult, Middle-aged, Senior) using quartile binning
- Created **`purchase_frequency_days`** by mapping purchase frequency text (e.g., "Weekly" → 7)
- Confirmed `discount_applied` and `promo_code_used` were identical, then dropped `promo_code_used`

### 3. Database integration
- Loaded the cleaned DataFrame into a PostgreSQL table named `customer`

### 4. SQL analysis (PostgreSQL)
Ten business questions answered in `customer_shopping_behavior_analysis_queries.sql`:

1. Revenue by gender
2. Discount users who still spent above average
3. Top 5 products by average review rating
4. Average spend: Standard vs. Express shipping
5. Subscribers vs. non-subscribers (spend and revenue)
6. Top 5 products by discount rate
7. Customer segmentation: New / Returning / Loyal
8. Top 3 products in each category
9. Repeat buyers and subscription likelihood
10. Revenue by age group

### 5. Dashboard (Power BI)
- Built an interactive dashboard with filters for subscription status, gender, category, and shipping type

### 6. Report
- Summarized the process, findings, and recommendations in a PDF report

---

## Dashboard

The Power BI dashboard (`customer_behavior_dashboard.pbix`) includes:

- **KPI cards:** Number of customers (3.9K), average purchase amount ($59.76), average review rating (3.75)
- **Charts:** customers by subscription status, revenue and sales by category, revenue and sales by age group
- **Slicers:** subscription status, gender, category, shipping type

![Customer Behavior Dashboard](images/dashboard.png)

---

## Key Results

- **Gender:** Male customers generated about **$157.9K** in revenue vs. **$75.2K** from female customers.
- **Subscriptions:** Only **27%** of customers are subscribers, and average spend is nearly identical ($59.49 vs. $59.87), so subscribing does not currently increase spend per purchase.
- **Customer segments:** **3,116** of 3,900 customers are "Loyal" (more than 10 previous purchases); only 83 are "New".
- **Shipping:** Express shipping customers spend slightly more on average ($60.48 vs. $58.46).
- **Discounts:** Hat, Sneakers, Coat, Sweater, and Pants have the highest discount rates (about 47–50%).
- **Top-rated products:** Gloves (3.86), Sandals (3.84), Boots (3.82), Hat (3.80), Skirt (3.78).
- **Age groups:** Revenue is fairly evenly spread; Young Adults lead slightly (~$62K).
- **Categories:** Clothing is the largest category by both revenue and sales volume.

---

## Business Recommendations

- **Boost subscriptions:** promote exclusive subscriber benefits, since only about a quarter of customers subscribe.
- **Loyalty programs:** reward repeat buyers to keep them in the Loyal segment.
- **Review discount policy:** some products are discounted in about half of purchases, so balance sales lift against margin.
- **Product positioning:** feature top-rated and best-selling items in campaigns.
- **Targeted marketing:** focus on high-revenue age groups and express-shipping users.

---

## Repository Structure

```
├── customer_shopping_behavior.csv                    # Raw dataset
├── customer_shopping_behavior_analysis.ipynb         # Python EDA, cleaning, DB load
├── customer_shopping_behavior_analysis_queries.sql   # PostgreSQL business queries
├── customer_behavior_dashboard.pbix                  # Power BI dashboard
├── images/
│   └── dashboard.png                                 # Dashboard screenshot
├── Customer_Shopping_Behavior_Analysis.pdf           # Final report
└── README.md
```

---

## How to Run

### Prerequisites
- Python 3.8+
- PostgreSQL and pgAdmin
- Power BI Desktop (Windows)

### Steps

**1. Clone the repository**
```bash
git clone https://github.com/gauricodes27/customer-shopping-behavior-analysis.git
cd customer-shopping-behavior-analysis
```

**2. Install Python dependencies**
```bash
pip install pandas numpy jupyter sqlalchemy psycopg2-binary
```

**3. Create the database**

In pgAdmin (or `psql`), create an empty database named `customer_behavior`.

**4. Configure the connection**

Open the notebook and update the connection settings in the database cell with your own credentials:
```python
username = "postgres"
password = "<your-password>"
host     = "localhost"
port     = "5432"          # default PostgreSQL port
database = "customer_behavior"
```
> Tip: avoid committing real passwords. Use environment variables or a `.env` file instead.

**5. Run the notebook**
```bash
jupyter notebook customer_shopping_behavior_analysis.ipynb
```
Run all cells. This cleans the data and creates the `customer` table in PostgreSQL.

**6. Run the SQL queries**

Open `customer_shopping_behavior_analysis_queries.sql` in pgAdmin and run each query against the `customer_behavior` database.

**7. Open the dashboard**

Open `customer_behavior_dashboard.pbix` in Power BI Desktop. If prompted, refresh or re-point the data source to your local PostgreSQL database or the CSV.

---

## Future Improvements

- Add statistical tests (e.g., subscriber vs. non-subscriber spend)
- Build a customer segmentation model (e.g., K-Means)
- Add time-based analysis if purchase dates become available
- Automate the pipeline with a scheduled script

---

## Author

**Gauri Gadadhe** · [LinkedIn](https://www.linkedin.com/in/gauri-gadadhe-b08299258/) · [GitHub](https://github.com/gauricodes27)
