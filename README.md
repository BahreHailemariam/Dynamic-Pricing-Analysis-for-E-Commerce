# 🛒 Dynamic Pricing Analysis for E-Commerce

_Predictive, data-driven pricing strategy using Python, SQL, and Power BI._

## 📌 Project Overview

This project provides a **data analytics and machine-learning pipeline** to help e-commerce companies determine optimal product prices dynamically based on:

- Demand trends

- Competitor pricing

- Inventory levels

- Customer behavior

- Seasonality

- Historical performance

The goal is to **maximize revenue and profit** while minimizing overpricing/underpricing risks.

## 🎯 Objectives

✔ Analyze demand elasticity and revenue sensitivity<br />
✔ Predict optimal pricing using ML models<br />
✔ Identify price segments and customer willingness-to-pay<br />
✔ Detect competitor pricing gaps<br />
✔ Build a dynamic pricing recommendation engine<br />
✔ Create dashboards for pricing teams

## 🧱 Project Architecture
```java
Raw Data Sources
    ↓
SQL Data Cleaning, Joins, Aggregations
    ↓
Feature Engineering (Demand, Elasticity, Competition, Time Series)
    ↓
ML Models (RandomForest, Prophet, XGBoost)
    ↓
Price Optimization Engine
    ↓
Power BI Dashboard (KPI Reporting)
```

## 📂 Folder Structure
```powershell
Dynamic_Pricing_Analysis/
│
├── data/
│   ├── raw/                     # Source CSV/JSON
│   └── processed/               # Cleaned, transformed datasets
│
├── sql/
│   ├── 01_create_tables.sql
│   ├── 02_cleaning.sql
│   ├── 03_feature_engineering.sql
│   ├── 04_pricing_metrics.sql
│   ├── 05_views_for_powerbi.sql
│
├── scripts/
│   ├── elasticity_model.py      # Estimate demand-price elasticity
│   ├── forecast_demand.py       # Prophet/ARIMA forecasting
│   ├── optimize_price.py        # Revenue-maximizing price recommendation
│   ├── load_data.py             # ETL loader
│   └── app.py                   # Streamlit app (optional)
│
├── dashboard/
│   └── PowerBI_Report_Spec.md   # Full dashboard specification
│
├── docs/
│   └── Workflow_Spec.md         # Pipeline documentation
│
└── README.md
```

## 🗄️ Data Model
### Tables Required

| Table           | Description                                   |
| --------------- | --------------------------------------------- |
| **products**    | SKU, category, cost, base price               |
| **sales**       | Quantity, revenue, price, date                |
| **competitors** | Competitor pricing data                       |
| **inventory**   | Stock levels, replenishment cycles            |
| **calendar**    | Date attributes (month, season, holiday flag) |

## 🧼 SQL Data Cleaning

Script: `02_cleaning.sql`

Tasks include:

- Fix invalid price values

- Fill missing category fields

- Normalize timestamps

- Handle negative or zero demand

- Deduplicate sales records

Example:

```sql
UPDATE sales
SET price = NULL
WHERE price <= 0;
```
## 🧠 Feature Engineering

Script: `03_feature_engineering.sql`

Created Features Include:
**1. Price Elasticity Features**

- % price change

- % quantity change

- elasticity coefficient:
```ini
Elasticity = %Δ Quantity / %Δ Price
```
**2. Competitor Gap**
```ini
PriceGap = OurPrice - CompetitorPrice
```
**3. Margin Features**

- Gross margin

- Profit per SKU

- Category margin contribution

**4. Demand Indicators**

- Rolling 7/30-day demand averages

- Stock-outs

- Holiday spikes

- Seasonality index

**5. Time Features**

- Day of week

- Month

- Promo period flag

- Holiday flag

## 🤖 Modeling Components

**1. Elasticity Estimation**

Script: `elasticity_model.py`
Models:

- Linear regression

- Log-log elasticity model

- Gradient Boosting elasticity

**2. Demand Forecasting**

Script: `forecast_demand.py`
Models:

- Facebook Prophet

- ARIMA

- RandomForest Regressor (optional)

Used to simulate future demand at various price points.

**3. Optimal Price Recommendation**

Script: `optimize_price.py`

Objective:
```java
Maximize Revenue = Price × PredictedDemand(Price)
```
Methods:

- Grid search

- ML-based optimization

- Profit maximization with constraints:

   - Competitor gap limits

   - Minimum margin threshold

   - Stock availability
## 📊 Key Pricing Metrics

SQL Script: `04_pricing_metrics.sql`

**Metrics:**

- Revenue

- Profit

- Conversion rate

- Elasticity score

- Price corridor (acceptable range)

- Price gap vs competition

- Lost revenue due to stockouts

Example SQL:
```sql

SELECT
    product_id,
    AVG(price) AS avg_price,
    SUM(quantity) AS total_units,
    SUM(price * quantity) AS revenue,
    SUM((price - cost) * quantity) AS profit
FROM sales
GROUP BY product_id;
```
## 📈 Power BI Dashboard Overview

### 📄 Pages Included
**1️⃣ Pricing Overview**

- Total revenue

- Profit & margin

- Average selling price

- Price vs competitor gap

- Price corridor visualization

**Visuals:**

- Revenue trend

- SKU-level price-profit scatter plot

- Profit waterfall chart

**2️⃣ Demand Insights**

- Demand trend

- Seasonality patterns

- Promo impact

- Category-level demand spikes

**Visuals:**

- Forecast line chart (Prophet forecasts)

- Rolling demand heatmap

- Holiday spike indicator

**3️⃣ Elasticity & Sensitivity**

- Elasticity coefficient by product

- Demand curve visualization

- Revenue maximize point (Price vs Demand)

**Visuals:**

- Elasticity quadrant chart

- Sensitivity slope graph

**4️⃣ Competitor Pricing**

- Competitor gap analysis

- Price leadership index

- Category competition matrix

**Visuals:**

- Gap vs Sales scatter

- Competitor comparison table

- Competitive pressure heatmap

**5️⃣ Optimal Price Recommendations**

- Recommended price per SKU

- Expected revenue lift

- Expected margin impact

**Visuals:**

- Before/After price comparison

- Recommendation KPI cards

- Product-level optimizer panel

**6️⃣ Inventory & Pricing Risk**

- Overstock / understock flags

- Pricing during supply issues

- Lost sales due to stockouts

**Visuals:**

- Inventory vs demand line charts

- Risk heatmap

- Stockout-driven price adjustment alerts

## 🧮 Sample DAX Measures

```DAX
TotalRevenue = SUM(sales[revenue])

AvgSellingPrice = AVERAGE(sales[price])

GrossMargin = 
DIVIDE(
    SUMX(sales, (sales[price] - sales[cost]) * sales[quantity]),
    SUM(sales[revenue])
)

ElasticityScore = AVERAGE(features[elasticity])
```

## 🚀 How to Run the Project
**1️⃣ Ingest Raw Data**

Place CSVs in:
```bash
data/raw/
```

**2️⃣ Run SQL Scripts**

Execute in sequence:
```pgsql
01_create_tables.sql
02_cleaning.sql
03_feature_engineering.sql
04_pricing_metrics.sql
05_views_for_powerbi.sql
```
**3️⃣ Train Pricing Models**

Run:
```bash

python scripts/elasticity_model.py
python scripts/forecast_demand.py
python scripts/optimize_price.py

```
**4️⃣ Visualize in Power BI**

Connect to:

- processed datasets (CSV)

- SQLite/Postgres DB

- ML prediction outputs

## 🌟 Key Insights You Can Discover

- Most elastic and inelastic products

- Products underpriced or overpriced

- Competitor gaps causing lost sales

- Price changes that maximize revenue

- Optimal pricing per category

- Profit uplift opportunities

- Relationships between price, demand, and seasonality

🔮 Future Enhancements

Reinforcement learning for real-time pricing

A/B testing module

Automated pricing recommendations via API

Integration with Shopify/Amazon APIs

Multi-agent competitive pricing simulation

🙌 Contributing

Pull requests, feature additions, and enhancements are welcome.
