
# Superstore Data Analysis

### 🔍 Project Overview

This project demonstrates the design and deployment of a real-time, scalable data pipeline on AWS for retail sales analysis using Superstore data. The objective is to simulate incremental data ingestion, metadata cataloging, query execution, and data visualization—all through native AWS services. The goal is to enable retail analytics teams to gain timely insights using cloud-native tools


### 🧰 Tech Stack
* **AWS S3** – Storage for raw and partitioned data snapshots (CSV files)

* **AWS Glue** – Metadata cataloging using Crawlers, schema inference

* **AWS IAM** – Role and permission management for Glue and Athena

* **AWS Athena** – SQL querying directly over S3-based data

* **AWS QuickSight** – Dashboards and visualizations for business insights



### 📈 Project Workflow

#### 1. S3: Storage Setup
* Created buckets and subfolders in S3.

* Uploaded incremental data snapshots for specific dates (e.g., 2017-01-01, 2017-01-02) for partition-based querying.

* Maintained naming conventions to allow automatic partition recognition.

#### 2. Glue: Cataloging and Metadata Extraction
* Created a database in AWS Glue.

* Configured a Crawler to scan S3 folders and infer schema.

* Defined an IAM role for Glue access.

* Ran the crawler on demand to populate the Data Catalog.

* Ensured the crawler respected the S3 folder structure for partitions.

#### 3. Athena: SQL Analytics on S3
* Set up an Athena query output location in S3.

* Queried Glue catalog tables to:

* Aggregate sales by category

* Filter data by region or date

* Analyze profit vs discount

* Identify top-selling sub-categories

🔎 Sample Athena Queries:


```sql
-- Total Sales by Category
SELECT Category, SUM(Sales) AS Total_Sales
FROM "superstore_db"."orders"
GROUP BY Category;

-- Profit by State
SELECT State, SUM(Profit) AS Profit
FROM "superstore_db"."orders"
GROUP BY State
ORDER BY Profit DESC
LIMIT 10;

-- Monthly Sales Trend
SELECT date_trunc('month', order_date) AS month, SUM(sales) AS total_sales
FROM "superstore_db"."orders"
GROUP BY 1
ORDER BY 1;
```

### 4. QuickSight: Visual Insights
Created dashboards with the following charts:
```
Chart Type	       Purpose

Bar Chart	       Total Sales by Category
Pie Chart	       Distribution of Orders by City
Line Chart	       Monthly Sales Trend
Heatmap	           Profit by Category and Sub-Category
KPI Widget	       Total Sales, Profit, Orders
```

### 📊 Sample Dataset Columns
```
Column Name	       Description
Order Date	       Date of order
Sales	           Revenue generated
Quantity	       Units sold
Discount	       Discount applied
Profit	           Profit earned
Category	       Product category
Sub-Category	   Detailed category
City, State	       Customer location
Segment	           Type of customer
```

### ✅ Use Cases & Tasks Performed
- Sales Analysis by Region and Category

- Profitability Analysis by State

- Customer Segment Performance

- Order Trend Over Time

- Top Performing Products

### 📝 Summary
This AWS data engineering project exemplifies how to build a modular and efficient pipeline using cloud-native tools. Starting from raw data ingestion in S3, metadata management via Glue, SQL analysis through Athena, and interactive dashboards in QuickSight, it offers an excellent starting point for scalable business analytics projects in retail or e-commerce domains.