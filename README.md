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

