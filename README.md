# 📊 Lead Conversion Analysis - Sales Analytics Dashboard

**A comprehensive sales analytics project demonstrating SQL, Google Sheets, and Looker Studio expertise for data-driven sales insights.**

🔗 **[View Live Looker Studio Dashboard](https://lookerstudio.google.com/u/0/reporting/a104319a-5e71-4746-8c99-b15c705c1368/page/uWKrF)**

---

## 🎯 Project Overview

This project analyzes 18 months of sales data (March 2024 - September 2025) to identify actionable insights in lead conversion, pipeline health, sales rep performance, and revenue trends. Built as a complete end-to-end analytics solution for sales operations decision-making.

### Dataset Summary
- **Time Period:** 18 months (Mar 2024 - Sep 2025)
- **Total Records:** 2,832 rows across 5 interconnected tables
- **Scope:** 10 sales reps, 1,000 leads, 500 accounts, 261 opportunities, 1,061 activities

---

## 💡 Key Business Insights

### 1. Lead Source Performance
**Finding:** Inbound Marketing delivers highest conversion at 34.21%, significantly outperforming Outbound (17.78%)

**Recommendation:** Reallocate marketing budget toward Inbound channels; optimize Outbound targeting

### 2. Pipeline Health - Critical Revenue Leakage  
**Finding:** $7.5M lost in Closed Lost deals vs $4M won (33% win rate) - bleeding $3.5M in missed opportunities

**Business Impact:** Urgent need to analyze loss reasons and improve sales methodology at Proposal/Negotiation stages

### 3. Rep Performance - Quality vs Quantity
**Finding:** 
- Emily Rodriguez: #1 revenue ($711K) but only 38% win rate
- Michael Torres: #2 revenue ($713K) but 60% win rate (most efficient closer!)

**Recommendation:** Study Michael's sales process for best practices; provide Emily with closing skills training

### 4. Sales Cycle Analysis
**Finding:** Referral leads offer best combination (47-day cycle + highest volume: 58 deals)

**Action:** Invest heavily in referral programs; Events close fastest (45 days) but low scalability

### 5. Revenue Growth Trajectory
**Finding:** Steady $4.05M cumulative revenue over 18 months (~$225K/month average)

**Trend:** Consistent growth despite monthly fluctuations; peak month: June 2024 ($580K)

### 6. At-Risk Opportunities - Urgent Attention Needed
**Finding:** 160 deals open 30+ days (some 700+ days old!) representing significant pipeline stagnation

**Recommendation:** Implement weekly pipeline reviews; set maximum age limits per stage; automate alerts

---

## 🛠️ Technical Skills Demonstrated

### SQL (Expert Level)
- ✅ Complex CTEs (Common Table Expressions)
- ✅ Window Functions (RANK, SUM OVER, running totals)
- ✅ Multi-table JOINs (3+ tables)
- ✅ Date calculations (DATEDIFF, DATEPART)
- ✅ Advanced aggregations and CASE WHEN logic
- ✅ Database design (fact/dimension tables, foreign keys)

### Google Sheets
- ✅ Data import and transformation
- ✅ Pivot tables for multi-dimensional analysis
- ✅ Advanced formulas (SUMIF, AVERAGEIF, calculations)
- ✅ Dashboard creation with KPI metrics

### Looker Studio
- ✅ Multi-page interactive dashboards
- ✅ Live data connections to Google Sheets
- ✅ Chart design (bar charts, scorecards, tables)
- ✅ Visual storytelling for business insights

### YAML
- ✅ Configuration file structure
- ✅ LookML-style data modeling
- ✅ Metadata documentation

---

## 📂 Project Structure
```
Lead-Conversion-Analysis/
├── SQL/
│   ├── 01_create_tables.sql          # Database schema with relationships
│   ├── 02_load_data.sql               # Bulk insert statements
│   ├── 03_lead_conversion.sql         # Conversion analysis query
│   ├── 04_pipeline_analysis.sql       # Pipeline health metrics
│   ├── 05_rep_performance.sql         # Rep rankings with window functions
│   ├── 06_sales_cycle.sql             # Time-to-close analysis with CTEs
│   ├── 07_revenue_trends.sql          # Running totals and growth
│   └── 08_at_risk_opportunities.sql   # Risk identification logic
├── Data/
│   ├── sales_reps.csv
│   ├── leads.csv
│   ├── accounts.csv
│   ├── opportunities.csv
│   └── activities.csv
├── sales_analytics_config.yaml        # Project configuration
└── README.md
```

---

## 🔍 Sample SQL Query

**Rep Performance Ranking with Window Functions:**
```sql
WITH Rep_Performance AS (
    SELECT 
        s.rep_id,
        s.rep_name,
        SUM(CASE WHEN o.stage = 'Closed Won' THEN o.amount ELSE 0 END) AS total_revenue,
        COUNT(CASE WHEN o.stage = 'Closed Won' THEN 1 ELSE NULL END) AS deals_won,
        COUNT(CASE WHEN o.stage = 'Closed Lost' THEN 1 ELSE NULL END) AS deals_lost,
        ROUND(
            CAST(COUNT(CASE WHEN o.stage = 'Closed Won' THEN 1 ELSE NULL END) AS FLOAT) 
            / (COUNT(CASE WHEN o.stage = 'Closed Won' THEN 1 ELSE NULL END) 
               + COUNT(CASE WHEN o.stage = 'Closed Lost' THEN 1 ELSE NULL END)) 
            * 100, 2
        ) AS win_rate
    FROM opportunities o
    JOIN sales_reps s ON o.rep_id = s.rep_id
    WHERE o.stage IN ('Closed Won', 'Closed Lost')
    GROUP BY s.rep_id, s.rep_name
)
SELECT 
    rep_name,
    total_revenue,
    deals_won,
    deals_lost,
    win_rate,
    RANK() OVER (ORDER BY total_revenue DESC) AS revenue_rank
FROM Rep_Performance
ORDER BY total_revenue DESC;
```

---

## 🚀 How to Use This Project

1. **Database Setup:** Run SQL scripts in order (01-02) to create schema and load data
2. **Analysis:** Execute queries 03-08 for specific business insights
3. **Visualization:** Import data to Google Sheets, connect to Looker Studio
4. **Dashboard:** Access live dashboard via link above

---

## 📧 Contact

**Created by:** Arravind  
**Date:** March 2026  
**Purpose:** Sales Analytics Interview Preparation

---

**Tools:** SQL Server | Google Sheets | Looker Studio | YAML
