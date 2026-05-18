# 📊 Business Insights 360 — AtliQ Hardware


> A comprehensive Power BI dashboard delivering 360° business intelligence across Finance, Sales, Marketing, Supply Chain, and Executive dimensions for AtliQ Hardware.

**🔗 [Live Dashboard](https://app.powerbi.com/view?r=eyJrIjoiMDk0OGRhYWQtOWEyYi00OWVmLWI0NWUtOGZlYzZjMjUwNzY3IiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)**

---

## 📌 Project Overview

AtliQ Hardware is a fast-growing electronics company that sells hardware products (PCs, mice, printers, storage devices, etc.) across global markets through multiple channels and customers. As the company expanded rapidly, it faced the challenge of making data-driven decisions across its various business functions.

This project delivers an end-to-end Power BI solution that enables stakeholders across Finance, Sales, Marketing, Supply Chain, and Executive leadership to monitor KPIs, identify trends, and make informed strategic decisions — all from a single, unified dashboard.

---

## 🏢 Business Context

### Company Structure

**AtliQ Hardware** manufactures and sells hardware products through a three-tier distribution model:

| Channel | Partners |
|---|---|
| **Retailer** | Croma, Amazon, Best Buy, Flipkart, Staples |
| **Direct** | AtliQ e Store, AtliQ Exclusive |
| **Distributor** | Neptune |

**Platforms:**
- **Brick & Mortar** — Croma, Best Buy
- **E-Commerce** — Amazon, Flipkart

**Markets/Regions:** APAC, EU, NA, LATAM, ANZ, ROA, NE, SE, India

### Problem Statement

AtliQ Hardware was relying on Excel files for data analysis, which proved insufficient as the business scaled globally. A competitor's data analytics team gave them a significant edge. To remain competitive, AtliQ's management decided to invest in a robust Power BI analytics solution covering all key business functions.

---

## 🛠️ Tech Stack

| Tool | Usage |
|---|---|
| **Power BI Desktop** | Dashboard development and report building |
| **SQL (MySQL)** | Data extraction and querying from source databases |
| **DAX** | Custom measures, KPI calculations, time intelligence |
| **Power Query (M)** | Data transformation and ETL pipeline |
| **Excel** | Supplementary data (targets, market share, operational expenses) |

---

## 📐 Data Model

The data model follows a **Snowflake Schema** design with fact tables connected to multiple dimension tables.

### Fact Tables
- `fact_sales_monthly` — Monthly sales transactions
- `fact_forecast_monthly` — Monthly forecast data per customer and product

### Dimension Tables
- `dim_customer` — Customer details (name, market, platform, channel)
- `dim_product` — Product hierarchy (segment, category, product)
- `dim_market` — Market/region/sub-zone mapping
- `dim_date` — Date table for time intelligence

### Supplementary Tables
- `freight_cost` — Freight cost by market and fiscal year
- `manufacturing_cost` — Manufacturing cost by product and fiscal year
- `pre_invoice_deductions` — Pre-invoice discount percentages
- `post_invoice_deductions` — Post-invoice discount and other deductions
- `operational_expense` — Ads & promotions expense data
- `market_share` — AtliQ and competitor market share data

---

## 💡 Key DAX Measures

### P&L Measures
```dax
-- Net Sales
Net Sales = SUM(fact_sales_monthly[net_sales_amount])

-- Gross Margin
Gross Margin = [Net Sales] - [Total COGS]

-- Gross Margin %
GM % = DIVIDE([Gross Margin], [Net Sales], 0)

-- Net Profit %
Net Profit % = DIVIDE([Net Profit], [Net Sales], 0)
```

### Forecast & Supply Chain Measures
```dax
-- Forecast Accuracy %
Forecast Accuracy % = 
1 - DIVIDE(ABS([Net Error]), [Absolute Forecast Quantity], 0)

-- Net Error
Net Error = [Forecast Quantity] - [Sales Quantity]
```

### Benchmark Comparisons
```dax
-- vs Last Year
NS $ LY = CALCULATE([Net Sales], SAMEPERIODLASTYEAR(dim_date[date]))

-- YoY Change %
NS $ Chg % = DIVIDE([Net Sales] - [NS $ LY], [NS $ LY], 0)
```

---

## 📊 Dashboard Views

### 🏠 Home Page
Central navigation hub with links to all five analytical views, a user manual download option, and a support connector. Shows report refresh date and sales data load period.

---

### 💰 Finance View
**Purpose:** P&L statement analysis across any customer, product, country, or time period.

**Key Visuals:**
- KPI cards for **Net Sales ($3.74bn)**, **GM% (38.08%)**, and **Net Profit% (-13.98%)** with benchmark comparison
- Full **Profit & Loss Statement** table (Gross Sales → Pre-invoice Deductions → Net Invoice Sales → Post-invoice Deductions → Net Sales → COGS → Gross Margin → Operational Expense → Net Profit)
- **Net Sales Performance Over Time** line chart (Sep 21–Aug 22)
- **Top/Bottom Products & Customers by Net Sales** — regional and segment breakdown

**Filters:** Region/Market · Customer · Segment/Category/Product · Year (2019–2022) · Quarter · YTD/YTG · vs LY / vs Target

---

### 🤝 Sales View
**Purpose:** Customer performance analysis across key financial metrics with a profitability/growth matrix.

**Key Visuals:**
- **Customer Performance Table** — NS$, GM$, GM% per customer (Amazon: $496.88M, AtliQ Exclusive: $361.12M, AtliQ e Store: $304.10M, etc.)
- **Performance Matrix (Scatter Chart)** — GM% vs NS$ by customer, color-coded by region (APAC/EU), bubble size as revenue
- **Product Performance Table** — NS$, GM$, GM% by segment
- **Unit Economics Donut Charts** — Revenue waterfall from Gross Sales to Net Sales to Gross Margin

---

### 📣 Marketing View
**Purpose:** Product performance analysis — same metrics as Sales View but focused on products rather than customers.

**Key Visuals:**
- **Product Performance Table** — NS$, GM$, GM%, Net Profit$, Net Profit% by segment (Notebook: $1,580.43M, Peripherals: $897.54M, Desktop: $711.08M, etc.)
- **Performance Matrix (Scatter Chart)** — GM% vs NS$ by product division (N&S, P&A, PC), color-coded
- **Region/Market/Customer Performance Table** — NS$, GM$, GM%, Net Profit$ by region (APAC: $1,923.77M, NA: $1,022.09M, EU: $775.48M)
- **Unit Economics** — Gross Margin vs COGS donut + Waterfall chart showing Gross Margin → Operational Expense → Net Profit impact

---

### 🚚 Supply Chain View
**Purpose:** Forecast accuracy, net error, and risk profiling by product, segment, category, and customer.

**Key Metrics:**
- **Forecast Accuracy: 81.17%** (LY: 80.21%, +1.2%)
- **Net Error: -3,472.7K** (LY: -751.7K, -361.97%)
- **ABS Error: 6,899.0K** (LY: 9,780.7K, -29.46%)

**Key Visuals:**
- **Accuracy / Net Error Trend** — dual-axis line chart (Sep 21–Aug 22) showing Net Error bars and Forecast Accuracy % line vs LY
- **Key Metrics By Customer Table** — Forecast Accuracy %, FA% LY, Net Error, Net Error%, Risk classification (EI = Excess Inventory, OOS = Out of Stock)
- **Key Metrics By Products Table** — Segment-level forecast accuracy and risk (Networking: 93.06%, Accessories: 87.42%, Notebook: 87.24%; risk OOS for Storage, Peripherals, Networking)

---

### 🌐 Executive View
**Purpose:** Integrated top-level dashboard consolidating insights from all business dimensions for C-suite decision making.

**Key KPIs:**
- Net Sales: **$3.74bn** | GM%: **38.08%** | Net Profit%: **-13.98%** | Forecast Accuracy: **81.17%**

**Key Visuals:**
- **Key Insights By Sub Zone** — NS$, Revenue Contribution%, GM%, Net Profit%, AtliQ Market Share%, Net Error%, Risk by sub-zone (NA: 27.4% RC, India: 25.3% RC)
- **Revenue by Division** donut — PC: 61.33%, P&A: 36.18%, N&S: remaining
- **Revenue by Channel** donut — Retailer: 71.53%, Direct: 17.8%, Distributor: 10.67%
- **Yearly Trend** line chart — NS$, GM%, Net Profit%, AtliQ MS% from 2018–2022 Est
- **PC Market Share Trend** — AtliQ vs competitors (BP, Dale, Innovo, Pacer) from 2018–2022 Est; AtliQ share declining from 7.8% to 5.9%
- **Top 5 Customers by Revenue** — Sage, Flipkart, AtliQ Exclusive, AtliQ e Store, Amazon
- **Top 5 Products by Revenue** — AQ BZ Allin1 Gen 2, AQ Home Allin1, AQ HOME Allin1 Gen 2, AQ Smash 1, AQ Smash 2

---

## 📈 Key Business Insights

- **Revenue grew significantly** from BM of $823.85M to **$3.74bn** — a 353.5% change YoY
- **Gross Margin** of 38.08% is tracking above benchmark (36.49%)
- **Net Profit** remains negative at **-13.98%** due to high operational expenses (-$1,945.30M), indicating the company is in a heavy investment/expansion phase
- **APAC** is the largest region by revenue ($1.92bn), followed by NA ($1.02bn)
- **Notebooks** are the top-selling product segment ($1.58bn)
- **AtliQ's PC market share** has been declining from 7.8% (2018) to 5.9% (2022 Est) — a key concern highlighted for management
- **Supply chain risk is OOS (Out of Stock)** at the overall level, indicating demand is outpacing forecast — particularly severe for Peripherals and Storage segments
- **Amazon** is the largest external customer ($496.88M), while **AtliQ Exclusive** has the highest GM% among top customers (46.01%)

---

## 🗂️ Project Structure

```
Business-Insights-360/
│
├── README.md
├── Business_Insights_360.pbix        # Main Power BI report file
│
├── screenshots/
│   ├── home.png
│   ├── finance_view.png
│   ├── sales_view.png
│   ├── marketing_view.png
│   ├── supply_chain_view.png
│   └── executive_view.png
│
└── resources/
    └── data_model_overview.png       # Optional: exported data model diagram
```

> ⚠️ **Note:** Raw datasets are not included in this repository due to data confidentiality. The `.pbix` file contains the full data model, DAX measures, and report layout.

---

## 🚀 How to Use

1. **Clone this repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/Business-Insights-360.git
   ```

2. **Open the report**
   - Open `Business_Insights_360.pbix` in Power BI Desktop

3. **Explore the dashboard**
   - Navigate between views using the left sidebar icons
   - Use slicers (Region, Customer, Segment, Year, Quarter) to filter the data
   - Toggle between **vs LY** (Last Year) and **vs Target** benchmarks using the top-right buttons

4. **View live report**
   - Access the published report directly via the [Live Dashboard link](https://app.powerbi.com/view?r=eyJrIjoiMDk0OGRhYWQtOWEyYi00OWVmLWI0NWUtOGZlYzZjMjUwNzY3IiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)

---

## 🙏 Acknowledgements

- **Guided Project by:** [Codebasics](https://codebasics.io)
- **Designed by:** Shreya Saniya
- **Data period:** Sales data loaded through December 2021; Report refresh date: April 12, 2022

---

## 📬 Connect

Feel free to connect if you have questions or feedback about this project!

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://linkedin.com)
