
# Data Cleaning Log

## Project Overview

This project involved cleaning, validating, and preparing retail order data for business reporting and analysis.

The raw dataset contained text inconsistencies, mixed date formats, missing values, duplicate records, invalid discounts, and business rule violations.

---

## Issues Identified

### Text Quality Issues

- Leading and trailing spaces
- Inconsistent capitalization
- Duplicate category naming conventions
- Mixed text formatting across business fields

### Date Issues

- Multiple date formats present in the dataset
- Mixed formats including:
  - YYYY-MM-DD
  - DD-MM-YYYY
  - MM/DD/YYYY
  - DD Mon YYYY
- Ship dates occurring before order dates

### Missing Values

- Missing Region values: 25
- Missing Ship Mode values: 21
- Missing Discount values: 18

### Duplicate Issues

- Exact duplicate rows: 20
- Conflicting duplicate Order IDs: 12

### Discount Issues

- Negative discounts: 15
- Excessive discounts (>50%): 15

---

## Cleaning Actions Performed

### Text Standardization

Applied cleaning to:

- customer_name
- segment
- region
- state
- city
- category
- sub_category
- ship_mode
- payment_status
- order_status

Actions performed:

- Removed extra spaces
- Removed leading/trailing spaces
- Standardized capitalization
- Corrected inconsistent category names

### Date Standardization

Implemented custom date parsing logic to standardize all dates.

Converted:

- order_date
- ship_date

Created:

- shipping_delay_days

### Missing Value Treatment

- Missing Region filled as "Unknown"
- Missing Ship Mode filled as "Unknown"
- Missing Discounts filled as 0

### Duplicate Handling

- Removed 20 exact duplicate rows
- Retained conflicting duplicate Order IDs
- Added review flag for conflicting records

---

## Business Rules Applied

### Region

Missing Region values replaced with "Unknown".

### Ship Mode

Missing Ship Mode values replaced with "Unknown".

### Discount Rules

- Missing discount values treated as 0
- Negative discounts flagged as invalid
- Discounts greater than 50% flagged as invalid

### Order Rules

- Cancelled orders retained but flagged
- Failed payment orders retained but flagged
- Refunded orders retained for separate reporting

### Shipping Rules

- Ship dates earlier than order dates flagged as invalid shipping records

---

## Assumptions

1. Discounts above 50% were considered invalid because normal business discounts in the dataset ranged from 0% to 25%.

2. Missing discounts were treated as 0 according to assignment requirements.

3. Conflicting duplicate Order IDs could not be resolved automatically and were therefore retained for business review.

---

## Records Removed

| Description | Count |
|-------------|-------|
| Exact Duplicate Rows Removed | 20 |

---

## Records Flagged

| Description | Count |
|-------------|-------|
| Conflicting Duplicate Records | 24 |
| Invalid Shipping Records | 22 |
| Negative Discounts | 15 |
| High Discounts | 15 |

---

## Final Data Quality Summary

| Status | Count |
|--------|-------|
| Clean | 839 |
| Warning | 22 |
| Invalid | 51 |

---

## Limitations

1. Business ownership was not available to verify conflicting duplicate records.

2. Discount validity thresholds were based on business assumptions.

3. Certain business decisions required interpretation due to incomplete business definitions in the source data.

4. Calculated sales and profit values were independently recomputed and may differ from source system calculations.
```
