# Online Retail Store — Revenue Analysis

**E-commerce · Transactional Data · European Markets**

---

## 📌 Project Overview

This project analyses one year of transactional data from a UK-based online retailer to understand revenue patterns, customer behaviour, and product performance across European markets.

The dataset contains **537,602 raw transactions** spanning December 2010 to December 2011. After a rigorous cleaning and modelling pipeline, the working dataset covers **377,830 validated sales** across **4,238 customers**, **3,579 products**, and **22 European countries**.

> *This project is currently at the data preparation stage. Revenue and cohort analysis is in progress.*

---

## 🎯 Analytical Goals

- Revenue trends over time — monthly, weekly, and hourly patterns
- Cohort analysis — customer retention and repeat purchase behaviour
- Product performance — top revenue drivers and category-level insights
- Geographic breakdown — revenue distribution across European markets

---

## 🔄 What's Been Done

### Data Cleaning & Preparation
The raw dataset required significant work before it was analysis-ready:

- **Cancellation handling** — removed all transactions where `InvoiceNo` starts with `'C'`
- **StockCode classification** — built a classifier to identify alphabetical, numeric, and alphanumeric codes; filtered out non-product entries (`POST`, `DOT`, `M`, `D`, `AMAZONFEE`, etc.) while deliberately retaining legitimate products like `PADS`
- **Negative and zero values** — removed rows where `Quantity` or `UnitPrice` ≤ 0
- **Missing CustomerID** — dropped ~134K rows with no customer identifier (required for cohort analysis)
- **Duplicate removal** — removed 5,256 exact duplicate records
- **Description normalisation** — resolved conflicting descriptions per StockCode by using the most frequent description per product
- **Outlier treatment** — applied percentile capping (1st–99th) on `Quantity` and `UnitPrice` to remove distorting extreme values
- **Geographic scope** — filtered to 22 European countries only; excluded non-European and unidentified records

### Data Modelling
Cleaned data was structured into a **star schema** for efficient downstream analysis:

| Table | Rows | Description |
|---|---|---|
| `FactSales` | 377,830 | Core transaction table — invoice, customer, product, quantity, price, revenue |
| `DimCustomer` | 4,238 | Customer dimension — ID and country |
| `DimProduct` | 3,579 | Product dimension — StockCode and normalised description |
| `DimDate` | 16,641 | Date dimension — month, day of month, day name, hour |

### Feature Engineering
- `total_price` = `quantity × unit_price` (transaction-level revenue)
- `month`, `day_of_month`, `day_name`, `hour` extracted from `invoice_date`

---

## 📁 Repo Structure

```
├── data/
│   ├── raw/                  # Original UCI dataset (.xlsx)
│   └── cleaned/              # Star schema output (4 CSVs)
│       ├── FactSales.csv
│       ├── DimCustomer.csv
│       ├── DimProduct.csv
│       └── DimDate.csv
└── notebooks/
    └── Data Overview and Cleaning.ipynb
```

---

## 🚀 Next Steps

- [ ] Revenue trend analysis — monthly and seasonal patterns
- [ ] Cohort analysis — customer retention by acquisition month
- [ ] Product performance — top SKUs, revenue concentration
- [ ] Geographic breakdown — revenue by country
- [ ] Streamlit dashboard (planned)

---

## 🛠 Stack

**Python** · pandas · openpyxl · Jupyter Notebooks

---

## 👤 Author

Victor Muthii · mv.munene01@gmail.com
