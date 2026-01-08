
# Sales Data ETL Pipeline

![Python](https://img.shields.io/badge/Python-3.*%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 📄 Project Overview
This project implements an **End-to-End ETL (Extract, Transform, Load) Pipeline** to process and clean raw retail sales transaction data. The goal is to transform dirty, raw CSV data into a high-quality dataset suitable for Business Intelligence (BI) analysis and visualization.

The pipeline is built using **Python** and **Pandas** within a Jupyter Notebook environment, focusing on data integrity, anomaly detection, and automated validation.

---

## 📂 Project Structure
```text
.
├── data/
│   ├── raw/                  # Raw data (Fact_Sales_1.csv)
│   └── clean/                # Processed data (Sales_Cleaned.csv)
├── notebooks/
│   └── sales_etl.ipynb       # Main ETL Notebook containing logic
├── README.md                 # Project Documentation

```


## ⚙️ Key Features & Transformation Logic

### 1. Data Ingestion & Security

* **String Preservation:** The pipeline strictly loads sensitive identifiers (like Credit Card numbers) as *Strings* (`dtype={'credit_card': str}`) to prevent integer overflow errors and preserve leading zeros/formatting.

### 2. Data Cleaning

* **Anomaly Removal:** Automatically detects and removes rows with invalid `customer_id` (specifically values equal to `-1`) which represent system errors or guest checkouts.
* **Missing Value Imputation:** Handles null values in the `payment` column by tagging them as `'Unknown'` to ensure data completeness.

### 3. Transformation & Formatting

* **Date Parsing:** Converts string-based dates (`transactional_date`) into standard Python `datetime` objects for time-series analysis.
* **Text Normalization:** Standardizes categorical text (e.g., `payment` methods) to Title Case (e.g., 'visa' → 'Visa') to fix inconsistencies.

### 4. Feature Engineering

Calculates key business metrics to enrich the dataset for the BI team:

* `Total Amount` = Quantity × Price
* `Total Cost` = Quantity × Cost
* `Net Profit` = Total Amount - Total Cost

---

## 🚀 How to Run

1. **Clone the repository**
```bash
git clone https://github.com/AdityaAksar/sales-etl-pipeline.git

```


2. **Install dependencies**
Ensure you have Python installed, then run:
```bash
pip install pandas numpy notebook

```


3. **Run the Notebook**
Navigate to the `notebooks/` directory and launch Jupyter:
```bash
cd notebooks
jupyter notebook sales_etl.ipynb

```


Execute all cells to generate the cleaned dataset in `data/clean/`.

---

## 📊 Data Validation Results

The pipeline includes a "Smart Validation" step at the end. Current production metrics based on the latest run:

* ✅ **Duplicate Check:** Passed (0 duplicates found in Transaction IDs).
* ✅ **Negative Value Check:** Passed (Price, Quantity, and Cost are all positive).
* ✅ **Invalid IDs:** Passed (All Customer IDs are valid positive integers).

---

**Author:** Aditya Zaldy

**Last Updated:** January 2026

