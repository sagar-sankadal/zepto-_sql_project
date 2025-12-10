# zepto-_sql_project
End-to-end SQL data analytics project on Zepto product dataset using PostgreSQL with all business insights.
## 🛒 Zepto E-commerce SQL Data Analyst Portfolio Project
This is a complete, real-world data analyst portfolio project based on an e-commerce inventory dataset scraped from Zepto — one of India’s fastest-growing quick-commerce startups. This project simulates real analyst workflows, from raw data exploration to business-focused data analysis.

## 📌Project Overview
The goal is to simulate how actual data analysts in the e-commerce or retail industries work behind the scenes using SQL to:

1.Set up a messy, real-world e-commerce inventory database  
2.Perform Exploratory Data Analysis (EDA) to explore product categories, availability, and pricing inconsistencies  
3.Implement Data Cleaning to handle null values, remove invalid entries, and convert pricing from paise to rupees  
4.Write business-driven SQL queries to derive insights around pricing, inventory, stock availability, revenue, and more  

## 📁 Dataset Overview
The dataset was sourced from Kaggle and was originally scraped from Zepto’s official product listings. It mimics what you’d typically encounter in a real-world e-commerce inventory system.

Each row represents a unique SKU (Stock Keeping Unit) for a product. Duplicate product names exist because the same product may appear multiple times in different package sizes, weights, discounts, or categories to improve visibility — exactly how real catalog data looks.

### 🧾 Columns:
- **sku_id** – Unique identifier for each product entry (Synthetic Primary Key)
- **name** – Product name as it appears on the app
- **category** – Product category like Fruits, Snacks, Beverages, etc.
- **mrp** – Maximum Retail Price (originally in paise, converted to ₹)
- **discountPercent** – Discount applied on MRP
- **discountedSellingPrice** – Final price after discount (converted to ₹)
- **availableQuantity** – Units available in inventory
- **weightInGms** – Product weight in grams
- **outOfStock** – Boolean flag indicating stock availability
- **quantity** – Number of units per package

## Project Workflow

### 1 .Database & Table Creation
We start by creating a SQL table with appropriate data types:

```sql
CREATE TABLE zepto (
  sku_id SERIAL PRIMARY KEY,
  category VARCHAR(120),
  name VARCHAR(150) NOT NULL,
  mrp NUMERIC(8,2),
  discountPercent NUMERIC(5,2),
  availableQuantity INTEGER,
  discountedSellingPrice NUMERIC(8,2),
  weightInGms INTEGER,
  outOfStock BOOLEAN,
  quantity INTEGER
);

2.  Data Import
Loaded CSV using pgAdmin's import feature.
If you're not able to use the import feature, use this command instead:
\copy zepto(category,name,mrp,discountPercent,availableQuantity,
            discountedSellingPrice,weightInGms,outOfStock,quantity)
FROM 'data/zepto_data_kaggle.csv'
WITH (FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8');



3.  Data Exploration
1.Counted the total number of records in the dataset
2.Viewed a sample of the dataset to understand structure and content
3.Checked for null values across all columns
4.Identified distinct product categories available in the dataset
5.Compared in-stock vs out-of-stock product counts
6.Detected products present multiple times, representing different SKUs

4.  Data Cleaning
1.Identified and removed rows where MRP or discounted selling price was zero
2.Converted mrp and discountedSellingPrice from paise to rupees for consistency and readability

5.  Business Insights
1.Found top 10 best-value products based on discount percentage
2.Identified high-MRP products that are currently out of stock
3.Estimated potential revenue for each product category
4.Filtered expensive products (MRP > ₹500) with minimal discount
5.Ranked top 5 categories offering highest average discounts
6.Calculated price per gram to identify value-for-money products
7.Grouped products based on weight into Low, Medium, and Bulk categories
8.Measured total inventory weight per product category

