# 🛒 Zepto Inventory Data Analysis | PostgreSQL

## 📌 Project Overview

### ⭐ Situation

Quick-commerce platforms like Zepto manage thousands of SKUs across multiple categories with dynamic pricing, discounts, and inventory fluctuations.
However, raw catalog data is often **messy, inconsistent, and difficult to analyze directly**.

---

### 🎯 Task

The objective of this project was to simulate a real-world data analyst role by:

* Building a structured database from raw e-commerce data
* Performing exploratory data analysis (EDA)
* Cleaning and transforming inconsistent pricing data
* Writing business-driven SQL queries to extract actionable insights

---

### ⚙️ Action

#### 1️⃣ Data Engineering

* Designed and created a PostgreSQL table with appropriate schema
* Imported raw CSV data and resolved UTF-8 encoding issues

#### 2️⃣ Data Exploration (EDA)

* Analyzed dataset structure and volume
* Identified null values, duplicate SKUs, and category distribution
* Compared stock availability across products

#### 3️⃣ Data Cleaning

* Removed invalid records (zero pricing values)
* Standardized pricing by converting paise → rupees
* Ensured consistency in numerical fields

#### 4️⃣ Data Analysis

Executed SQL queries to answer key business questions:

* Which products offer the highest discounts?
* Which high-value products are out of stock?
* Which categories generate the highest potential revenue?
* Which products provide best value based on price per gram?
* How do discounts vary across categories?

---

### 📊 Result (Key Insights)

* Identified **top-performing discount categories**, helping optimize promotional strategies
* Highlighted **high-MRP out-of-stock products**, indicating potential revenue loss
* Derived **price-per-gram metric**, enabling value-based product comparison
* Estimated **category-level revenue potential**, useful for inventory planning
* Segmented products into **Low / Medium / Bulk weight groups** for better categorization

---

## 📁 Dataset Overview

* Source: Kaggle (scraped from Zepto product listings)
* Represents real-world e-commerce inventory data

Each row corresponds to a **unique SKU**, meaning:

* Same product can appear multiple times
* Variations include weight, quantity, discount, and packaging

---

### 🧾 Columns Description

| Column                 | Description               |
| ---------------------- | ------------------------- |
| sku_id                 | Unique product identifier |
| name                   | Product name              |
| category               | Product category          |
| mrp                    | Maximum Retail Price (₹)  |
| discountPercent        | Discount applied          |
| discountedSellingPrice | Final selling price (₹)   |
| availableQuantity      | Stock available           |
| weightInGms            | Product weight            |
| outOfStock             | Availability status       |
| quantity               | Units per package         |

---

## 🔧 Technical Implementation

### Database Schema

```sql id="zepto_sql_1"
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
```

---

### Data Import

```sql id="zepto_sql_2"
\copy zepto(category,name,mrp,discountPercent,availableQuantity,
discountedSellingPrice,weightInGms,outOfStock,quantity)
FROM 'data/zepto_v2.csv'
WITH (FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8');
```

---

## 📊 Key Analysis Performed

* 📦 Inventory Analysis (Stock vs Out-of-Stock)
* 💸 Pricing & Discount Analysis
* 📈 Category Performance Analysis
* ⚖️ Value-based Pricing (Price per Gram)
* 🏷️ Product Segmentation (Weight-based grouping)
* 💰 Revenue Estimation

---

## 🛠️ Tools & Technologies

* PostgreSQL
* SQL (Aggregations, CASE, Filtering, Grouping)
* pgAdmin
* CSV Data Processing

---

## 🚀 How to Run

```bash
git clone https://github.com/hanumanth112/Zepto-Inventory-Data-Analysis-PostgreSQL.git
cd Zepto-Inventory-Data-Analysis-PostgreSQL
```

### Steps to Execute:

1. Create a new database in PostgreSQL
2. Open `zepto_SQL_data_analysis.sql`
3. Run the script to create the table and queries
4. Import the dataset (`zepto_v2.csv`)

   * Ensure file is in **UTF-8 format**
5. Execute queries step-by-step to reproduce analysis

---

### 💡 Tip

If `\copy` command fails:

* Use **pgAdmin Import Tool**
* Or update file path according to your system

Example:

```sql
\copy zepto FROM 'C:/your-path/zepto_v2.csv' WITH (FORMAT csv, HEADER true);

```

## 📈 Business Value

This project demonstrates the ability to:

* Transform raw retail data into structured insights
* Identify revenue opportunities and stock issues
* Support pricing and inventory decision-making
* Simulate real-world e-commerce analytics workflows

---

## 🚀 Future Enhancements

* Build interactive dashboards (Power BI / Tableau)
* Add KPI tracking (Revenue, Avg Discount, Stock Ratio)
* Perform time-series trend analysis
* Integrate Python for advanced analytics

---

## 👨‍💻 Author

**Hanumantha B**

---

## 📜 License

MIT License
