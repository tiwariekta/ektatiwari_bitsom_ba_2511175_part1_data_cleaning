# Part 1: Business Data Cleaning, Validation & Excel Reporting

## Problem Summary

The objective of this project was to clean, validate, and prepare retail order data exported from multiple internal systems. The raw dataset contained several data quality issues including inconsistent text formatting, mixed date formats, missing values, duplicate records, invalid discounts, calculation inconsistencies, and order status conflicts.

The goal was to create a clean, analysis-ready dataset along with supporting quality reports and business summary reports for management review.

---

# Dataset Description

The dataset contains order-level retail sales transactions with customer, product, sales, profit, shipping, and payment information.

### Key Fields

* order_id
* order_date
* ship_date
* customer_name
* segment
* region
* state
* city
* category
* sub_category
* product_name
* ship_mode
* quantity
* unit_price
* discount
* sales
* cost
* profit
* payment_status
* order_status

### Dataset Size

| Metric                   | Value |
| ------------------------ | ----: |
| Raw Records              |   932 |
| Final Records            |   912 |
| Exact Duplicates Removed |    20 |

---

# Tools Used

* Python
* Pandas
* NumPy
* Jupyter Notebook (VS Code)
* OpenPyXL
* Microsoft Excel

### Why Python Was Used

Although the assignment mentions Excel-based cleaning techniques, Python was used to implement a more scalable and production-oriented approach. The same cleaning logic can be applied to datasets of any size while maintaining reproducibility and auditability.

---

# Cleaning Steps Performed

## 1. Text Standardization

The following fields were standardized:

* customer_name
* segment
* region
* state
* city
* category
* sub_category
* ship_mode
* payment_status
* order_status

Actions performed:

* Removed leading/trailing spaces
* Removed extra spaces
* Standardized capitalization
* Corrected inconsistent category names
* Standardized business labels

---

## 2. Date Cleaning and Validation

Date fields cleaned:

* order_date
* ship_date

Multiple date formats were identified and standardized:

* YYYY-MM-DD
* DD-MM-YYYY
* MM/DD/YYYY
* DD Mon YYYY

Additional validations:

* Missing dates
* Invalid dates
* Ship date earlier than order date

Created:

* shipping_delay_days

Results:

* Missing Order Dates: 0
* Missing Ship Dates: 0
* Invalid Shipping Records: 22

---

## 3. Duplicate Handling

### Exact Duplicates

* Identified 20 exact duplicate rows
* Removed duplicate copies
* Retained one valid copy

### Duplicate Order IDs

After removing exact duplicates:

* 12 duplicate Order IDs remained
* 24 records contained conflicting business information

### Logic Used

1. Exact duplicate rows were removed.
2. Duplicate Order IDs were analyzed separately.
3. Records with conflicting sales or order status information were retained.
4. Conflicting records were flagged as "Review Required".
5. No conflicting business records were deleted automatically.

---

## 4. Missing Value Handling

| Field     | Action                |
| --------- | --------------------- |
| Region    | Filled with "Unknown" |
| Ship Mode | Filled with "Unknown" |
| Discount  | Filled with 0         |

Summary:

* Missing Region Values: 25
* Missing Ship Mode Values: 21
* Missing Discounts: 18

---

## 5. Discount Validation

Validation rules applied:

* Negative discounts flagged as invalid
* Discounts above 50% flagged as invalid

Results:

| Issue                 | Count |
| --------------------- | ----: |
| Negative Discounts    |    15 |
| High Discounts (>50%) |    15 |

---

## 6. Business Rule Validation

Applied business rules:

* Missing Region → Filled as Unknown
* Missing Ship Mode → Filled as Unknown
* Missing Discount → Treated as 0
* Negative Discount → Flagged Invalid
* High Discount → Flagged Invalid
* Cancelled Orders → Excluded from completed sales analysis
* Failed Payments → Excluded from completed sales analysis
* Refunded Orders → Reported separately
* Invalid Shipping Records → Flagged

---

# Calculated Columns Created

The following calculated fields were added:

* cleaned_discount
* calculated_sales
* calculated_profit
* profit_margin
* shipping_delay_days
* order_month
* order_year
* data_quality_flag

---

# Summary of Data Quality Issues Found

| Issue                    | Count |
| ------------------------ | ----: |
| Missing Region           |    25 |
| Missing Ship Mode        |    21 |
| Missing Discount         |    18 |
| Exact Duplicate Rows     |    20 |
| Duplicate Order IDs      |    12 |
| Negative Discounts       |    15 |
| High Discounts           |    15 |
| Invalid Shipping Records |    22 |

---

# Final Data Quality Summary

| Status  | Count |
| ------- | ----: |
| Clean   |   839 |
| Warning |    22 |
| Invalid |    51 |

---

# Summary of Pivot Reports

The following pivot summaries were created:

1. Sales and Profit by Region
2. Sales and Profit by Category and Sub-Category
3. Order Count by Ship Mode
4. Profit Margin by Customer Segment
5. Refunded / Cancelled / Failed Orders by Region
6. Monthly Sales Trend

---

# Key Business Insights

### 1. South Region Generated Highest Sales

| Region | Sales |
| ------ | ----: |
| South  | 2.24M |
| East   | 2.19M |
| North  | 2.16M |
| West   | 2.12M |

South was the highest revenue-generating region.

---

### 2. Chairs Were the Highest Revenue Furniture Category

Among furniture products, Chairs generated the highest sales and profit contribution.

---

### 3. Data Quality Issues Were Limited

More than 90% of records were classified as clean after validation and standardization.

---

### 4. Duplicate Business Records Were Identified

24 records contained conflicting business information and were retained for business review rather than being removed.

---

### 5. Discount Quality Issues Were Present

30 records contained invalid discount values including negative discounts and unusually high discounts.

---

# Assumptions

1. Discounts above 50% were considered invalid.
2. Missing discounts were treated as 0 according to assignment requirements.
3. Duplicate Order IDs with conflicting information were retained for review.
4. Invalid shipping records were not corrected automatically.

---

# Limitations

1. Business ownership was not available to validate conflicting duplicate records.
2. Discount thresholds were based on business assumptions.
3. Some source system calculations may differ from recalculated values.
4. Data quality decisions were made based on available information only.

---

# Screenshots Included

The following screenshots are included in the repository:

* raw_data_preview.png
* cleaned_data_preview.png
* pivot_summary_1.png
* pivot_summary_2.png

These screenshots demonstrate the raw dataset, cleaned dataset, and final business reporting outputs.

---

# Repository Deliverables

* data/raw_orders.xlsx
* data/cleaned_orders.xlsx
* outputs/data_quality_report.xlsx
* outputs/pivot_summary.xlsx
* outputs/cleaning_log.md
* README.md
* screenshots/raw_data_preview.png
* screenshots/cleaned_data_preview.png
* screenshots/pivot_summary_1.png
* screenshots/pivot_summary_2.png
