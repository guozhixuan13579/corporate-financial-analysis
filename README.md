
# Corporate Financial Analysis Tool

**Supports both Kaggle local data and WRDS database**

---

## 1. Project Overview

This project is developed for the ACC102 Mini Assignment (Track 2). It provides an automated financial analysis tool for corporate financial statements. The tool performs data cleaning, feature engineering, financial ratio calculation, multi-company comparison, and generates a complete HTML report with charts and recommendations.

**Key Features:**
- Supports both Kaggle (upload local files) and WRDS (direct database connection)
- Automatically detects and standardizes column names from different data sources
- Supports single company, multi-company comparison, and stock data analysis
- One-click generation of complete HTML report

**Author:** [zhixuan.Guo]
**Date:** April 2026
**Course:** ACC102 Mini Assignment - Track 2
**AI Tool:** DeepSeek-V3

---

## 2. Problem Definition & Target User

### Problem

Financial analysts and business students often need to quickly assess a company's financial health, identify profitability drivers, and detect potential risks. However, manually processing financial data is time-consuming and error-prone.

### Solution

This tool automates the entire financial analysis workflow:
- Load data from Kaggle or WRDS
- Clean and standardize column names
- Calculate key financial ratios
- Generate visualizations
- Export a professional HTML report

### Target User

- Financial analysts
- Business managers
- Students learning financial analysis
- Anyone who needs to analyze corporate financial statements

---

## 3. Supported Data Sources

This tool supports two types of data sources:

Kaggle: Upload local CSV or Excel files (e.g., Sample Superstore dataset). No login required.

WRDS Compustat: Direct database connection for public company financial statements. WRDS login required.

WRDS CRSP: Direct database connection for stock prices and returns. WRDS login required.

### Data Requirements

Important: This tool is designed for corporate financial statement analysis only.

Required columns (at least one of each):
- Revenue/Sales (e.g., Sales, Revenue)
- Profit/Net Income (e.g., Profit, Net Income)

NOT supported data types:
- Customer credit score data
- Loan risk assessment data
- Demographic data

---

## 4. Key Features

- Dual Data Source Support: Supports both Kaggle local files and WRDS database
- Data Cleaning: Automatically handles missing values, duplicates, outliers
- Feature Engineering: Calculates profit margin, ROA, ROE, debt ratio, etc.
- Financial Health Score: Composite score from 0 to 100
- Multi-Company Comparison: Automatically ranks companies by profit margin, ROA, debt ratio
- Visualization: Automatically generates 2-6 charts based on data type
- HTML Report: Exports complete report with charts and written conclusions

---

## 5. Technical Approach

### 5.1 Analysis Workflow (12 Steps)

Run the 12 cells in the Jupyter Notebook in order:

Step 1 (Cell 1): Import all required Python packages
Step 2 (Cell 2): Select data source (Kaggle or WRDS)
Step 3 (Cell 3): Configure parameters (file name, tickers, year range, etc.)
Step 4 (Cell 4): Load data (WRDS requires username and password)
Step 5 (Cell 5): Column Name Standardization (core feature)
Step 6 (Cell 6): Data Cleaning
Step 7 (Cell 7): Feature Engineering
Step 8 (Cell 8): Overall Financial Analysis
Step 9 (Cell 9): Dimensional Analysis
Step 10 (Cell 10): Visualization
Step 11 (Cell 11): Conclusions & Recommendations
Step 12 (Cell 12): Export HTML Report

### 5.2 Column Name Standardization (Cell 5)

This is the core feature. It automatically unifies column names from different data sources into standard names:

- Sales, Revenue → sales
- Profit, Net Income → profit
- Assets, Total Assets → total_assets

If unmapped columns are detected, the code will prompt the user. Users can simply add their column names to the USER_*_NAMES lists (see Section 9 for details).

### 5.3 Data Cleaning (Cell 6)

- Data type conversion (numeric, datetime)
- Missing value analysis and filling (median for numeric, mode for categorical)
- Duplicate row removal
- Outlier detection (IQR method, 3x IQR threshold)
- Logical consistency checks (profit ≤ sales, discount ≥ 0)

### 5.4 Feature Engineering (Cell 7)

Features created include:

- Profit Margin: Profit / Sales × 100%
- ROA: Profit / Total Assets × 100%
- ROE: Profit / Shareholders' Equity × 100%
- Debt Ratio: Total Liabilities / Total Assets × 100%
- Financial Health Score: Composite score (0-100)

---

## 6. How to Run

### 6.1 Install Dependencies

Run the following command in your terminal:

pip install wrds pandas numpy matplotlib seaborn openpyxl

### 6.2 Clone the Project

git clone https://github.com/guozhixuan13579/corporate-financial-analysis.git
cd corporate-financial-analysis

### 6.3 Open the Notebook

jupyter notebook corporate_financial_analysis.ipynb

### 6.4 Run the 12 Cells in Order

Run Cell 1 through Cell 12 sequentially and follow the prompts.

Kaggle Mode Example:

Cell 2: Enter 1
Cell 3: Enter file name (e.g., SampleSuperstore.xlsx)
Cell 3: Enter company name (e.g., Sample Superstore)

WRDS Mode Example:

Cell 2: Enter 2
Cell 3: Enter 'financial' or 'stock'
Cell 3: Enter 'single' or 'multiple'
Cell 3: Enter tickers (e.g., AAPL,MSFT,GOOGL)
Cell 3: Enter start year and end year
Cell 4: Enter WRDS username and password

### 6.5 View Output

After all cells complete, you will find in the current folder:

- {company_name}_charts.png - Analysis charts
- {company_name}_complete_report.html - Complete HTML report

Double-click the HTML file to open it in your browser.

---

## 7. Output Files

### Chart File (PNG)

Automatically generates 2-6 charts based on data type:

Multi-company Financial: Profit margin bar chart, ROA bar chart, debt ratio bar chart, trend line
Single-company Financial: Profit margin histogram, ROA histogram, loss pie chart, health score histogram
Stock Data: Return distribution histogram, cumulative return line, volatility line
Retail Data: Category profit bar chart, region profit bar chart, discount scatter plot

### HTML Report

The report includes:
- Report summary (date, data source, record count)
- Key metrics cards (profit margin, ROA, debt ratio, health score)
- Multi-company comparison table (if applicable)
- Embedded analysis charts
- Written conclusions (key findings)
- Actionable recommendations

---

## 8. Example Results

Example output from analyzing AAPL, MSFT, and GOOGL.

### Profit Margin Ranking

1. MSFT: 28.69%
2. GOOGL: 22.58%
3. AAPL: 17.53%

### ROA Ranking

1. AAPL: 16.07%
2. MSFT: 15.33%
3. GOOGL: 15.20%

### Recommendations

1. Study MSFT's cost management strategies to improve margins for AAPL and GOOGL
2. AAPL has the highest asset utilization (ROA #1) - other companies can learn from this
3. All three companies have low debt ratios, indicating healthy financial positions

---

## 9. Data Customization Guide (Important)

If your dataset has column names that don't match the default mappings, you can easily add them.

### How to See Unmapped Columns

After running Cell 5, the code will display:

Unmapped columns (not used in analysis):
- total_revenue
- net_profit
- product_type

### How to Add Mappings

Find the corresponding USER_*_NAMES list in Cell 5 and add your column names:

USER_SALES_NAMES = ['total_revenue']      # Sales/revenue columns
USER_PROFIT_NAMES = ['net_profit']        # Profit/net income columns
USER_CATEGORY_NAMES = ['product_type']    # Product category columns
USER_REGION_NAMES = ['sales_area']        # Region columns

### Column Name Mapping Reference

- Sales, Revenue → USER_SALES_NAMES
- Profit, Net Income → USER_PROFIT_NAMES
- Cost, Expenses → USER_COST_NAMES
- Product Category → USER_CATEGORY_NAMES
- Region → USER_REGION_NAMES
- Customer Segment → USER_SEGMENT_NAMES
- Stock Ticker → USER_TICKER_NAMES
- Date → USER_DATE_NAMES
- Year → USER_YEAR_NAMES

After adding, re-run Cell 5.

---

## 10. Limitations

- Data Scope: This tool is designed for corporate financial statement analysis only. Non-financial data is not supported.
- Analysis Depth: Analysis depth depends on data completeness (e.g., ROA cannot be calculated without an Assets column)
- WRDS Account Required: WRDS mode requires a valid WRDS account and campus network/VPN access
- Column Names: If completely unfamiliar column names appear, users need to manually add mappings in Cell 5

---

## 11. AI Disclosure

- Tool Name: DeepSeek
- Access Date: April 2026
- Purpose: Assisted with code structure design, column mapping dictionary generation, debugging data cleaning and feature engineering functions, and provided README and reflection report templates

---

## 12. File Structure

- corporate_financial_analysis.ipynb (Main Notebook, 12 cells)
- README.md (Project documentation)
- requirements.txt (Dependencies list)

- data/ (Sample data, optional)
  - SampleSuperstore.xlsx

- outputs/ (Output files, generated after running)
  - xxx_charts.png
  - xxx_complete_report.html

## 13. Contact

For questions or suggestions, please contact:

Author: [zhixuan.Guo]
Email: [Zhixuan.Guo24@student.xjtlu.edu.cn]
Course: ACC102 Mini Assignment - Track 2
