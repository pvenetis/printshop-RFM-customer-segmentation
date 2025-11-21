# Print Shop Customer Segmentation using RFM Analysis

> For more of my projects and analytics journey, visit my [Portfolio](https://pvenetis.github.io/).

### Table of Contents
- [Project Overview](#project-overview)
- [Executive Summary](#executive-summary)
- [Tools Used](#tools-used)
- [Dataset Description](#dataset-description)
- [RFM Methodology](#rfm-methodology)
  - [Recency](#recency)
  - [Frequency](#frequency)
  - [Monetary](#monetary)
  - [RFM Scoring](#rfm-scoring)
- [Customer Segmentation](#customer-segmentation)
- [Key Insights](#key-insights)
- [Segmentation Priority Matrix](#segmentation-priority-matrix)
- [Business Recommendations](#business-recommendations)
- [Data & Analysis Artifacts](#data--analysis-artifacts)

---

## Project Overview

This project focuses on analyzing a print shop business that sells products such as **Greeting Cards, Business Cards, Photo Books, Canvas Prints, Flyers, and Posters**.  
The goal is to understand **who the best customers are, which segments need retention campaigns, which segments represent growth opportunities, and which segments can be deprioritized**.

---

## Executive Summary

This project analyzes ~1,000 print shop orders using RFM segmentation to understand customer behavior, revenue contribution, and product preferences.  

Key findings:
- The **Best + Loyal** customers (~136 people) generate ~70% of total revenue. Top revenue-driving products are **Canvas Print** and **Photo Book** for Best Customers, and **Business Card** and **Greeting Card** for Loyal Customers.  
- **Potential Loyal** customers (~81 people) contribute ~22% of revenue and represent the largest growth opportunity; targeted campaigns could increase engagement and purchase value.  
- **Need Attention** customers (~57 people, ~7.8% of revenue) primarily order **Greeting Cards** (~35% of their purchases); product-specific promotions could recover ~$1,348 revenue.  
- **At Risk** customers (~13 people, ~0.8% of revenue) have minimal impact and can be deprioritized in short-term retention strategies.  

A single-page Power BI dashboard visualizes customer segmentation, revenue contribution, product mix, and behavioral metrics, providing actionable insights to guide retention and growth initiatives.

---

## Tools Used

- Excel
- Power Query
- Power BI

---

## Dataset Description

File: `print_orders.csv`  
Approximately 1,000 orders, containing the following columns:

| Column        | Description                         |
|---------------|-------------------------------------|
| OrderID       | Unique transaction ID               |
| CustomerID    | Unique customer identifier          |
| OrderDate     | Timestamp of purchase               |
| ProductType   | Product purchased                   |
| OrderValue    | Revenue from the order              |

Data was cleaned and aggregated in Excel to compute customer-level RFM metrics.

---

## RFM Methodology

RFM stands for Recency, Frequency, Monetary. It is a well-established technique for understanding customer behavior and segmenting a customer base.

### Recency

Number of days since the customer’s most recent purchase.

**Formula:**
```excel
Recency = TODAY() - Max(OrderDate)
```

**Scoring:** Lower recency = more recent = higher R score.

### Frequency
Total number of purchases made by the customer.

**Scoring:** Higher frequency = more loyal = higher F score.

### Monetary

Total amount spent by the customer.

**Scoring:** Higher spend = more valuable = higher M score.

## RFM Scoring

Scoring applied using Excel percentile logic.
```excel
RFM = R + F + M
```

### Recency Score (R):
```excel
=IFS(
    B2 <= PERCENTILE.INC($B$2:$B$288,0.2), 5,
    B2 <= PERCENTILE.INC($B$2:$B$288,0.4), 4,
    B2 <= PERCENTILE.INC($B$2:$B$288,0.6), 3,
    B2 <= PERCENTILE.INC($B$2:$B$288,0.8), 2,
    B2 > PERCENTILE.INC($B$2:$B$288,0.8), 1
)
```

### Frequency Score (F):
```excel
=IFS(
    C2 >= PERCENTILE.INC($C$2:$C$288,0.8), 5,
    C2 >= PERCENTILE.INC($C$2:$C$288,0.6), 4,
    C2 >= PERCENTILE.INC($C$2:$C$288,0.4), 3,
    C2 >= PERCENTILE.INC($C$2:$C$288,0.2), 2,
    C2 < PERCENTILE.INC($C$2:$C$288,0.2), 1
)
```

### Monetary Score (M):
```excel
=IFS(
    D2 >= PERCENTILE.INC($D$2:$D$288,0.8), 5,
    D2 >= PERCENTILE.INC($D$2:$D$288,0.6), 4,
    D2 >= PERCENTILE.INC($D$2:$D$288,0.4), 3,
    D2 >= PERCENTILE.INC($D$2:$D$288,0.2), 2,
    D2 < PERCENTILE.INC($D$2:$D$288,0.2), 1
)
```

## Customer Segmentation

Customer groups are defined based on combined RFM scores:

| Segment                   | Criteria                               |
|---------------------------|----------------------------------------|
| Best Customers            | Highest RFM scores (≥ 13)              |
| Loyal Customers           | High F and M scores (≥ 10)             |
| Potential Loyal Customers | Moderate R and F scores (≥ 7)          |
| Need Attention            | Low to moderate R scores (≥ 4)         |
| At Risk                   | Lowest R scores, low engagement (< 4)  |

---

## Key Insights

| Segment                   | Count | Revenue Contribution (%) | Description / Findings |
|---------------------------|-------|-------------------|-----------------------|
| Best Customers            | 61    | 39.30%  | Core revenue drivers; high engagement and repeat purchases. Product mix is fairly balanced, with **Canvas Print** and **Photo Book** driving the most revenue. |
| Loyal Customers           | 75    | 30.27%   | Consistent buyers with strong retention potential. Top revenue-driving products are **Business Card** and **Greeting Card**. |
| Potential Loyal Customers | 81    | 21.79%   | Largest group; significant growth potential. Focused engagement could increase frequency and value. |
| Need Attention            | 57    | 7.83%    | Moderate engagement; primarily order **Greeting Cards** (~35% of orders). Targeted promotions could recover revenue. |
| At Risk                   | 13    | 0.81%     | Minimal revenue impact; can be deprioritized in short-term strategy. |

**Quick Takeaways:**
- **Best + Loyal** groups (~136 customers) form the revenue core (~70% of total). Retention is key, with top products identified per segment.  
- **Potential Loyal** is the largest segment (~22% revenue), representing the **highest growth opportunity**.  
- **Need Attention** can be re-engaged via product-focused promotions, especially Greeting Cards (~35%).  
- **At Risk** segment has negligible revenue (~0.8%) and can be deprioritized.  

---

## Segmentation Priority Matrix

| Segment                   | Revenue (%) | Priority | Action Focus |
|---------------------------|-----------|----------|--------------|
| Best Customers            | 39.30%    | 🔵 High Retention | Maintain engagement, upsell Canvas Print and Photo Book, VIP perks |
| Loyal Customers           | 30.27%    | 🟢 Strong | Loyalty programs, cross-sell Business Card and Greeting Card, referrals |
| Potential Loyal Customers | 21.79%    | 🔴 High Growth | Targeted campaigns to increase frequency/value, nudges based on top products |
| Need Attention            | 7.83%     | 🟠 Medium | Product-specific promotions (Greeting Cards), light re-engagement campaigns |
| At Risk                   | 0.81%     | ⚪ Low | Optional win-back; minimal impact |

**Legend for Priority Colors/Emojis:**  
- 🔴 High Growth / Must Focus  
- 🟢 Strong / Secondary Focus  
- 🟠 Medium / Tactical / Monitor  
- 🔵 High Retention / Maintain Core  
- ⚪ Low / Ignore for now  

---

## Business Recommendations

**Best Customers**
- Maintain engagement and upsell high-value products (**Canvas Print**, **Photo Book**).  
- Offer VIP perks and personalized communications.

**Loyal Customers**
- Introduce loyalty programs and bundles targeting top products (**Business Card**, **Greeting Card**).  
- Encourage referrals and cross-selling.

**Potential Loyal Customers**
- Highest growth priority; use targeted campaigns to increase frequency and value.  
- Leverage product preferences to personalize promotions.

**Need Attention**
- Moderate priority: re-engage via promotions, especially **Greeting Cards**.  
- Light-touch campaigns to prevent churn and recover ~$1,348 revenue.

**At Risk**
- Low priority: minimal revenue impact (~0.8%).  
- Optional win-back campaigns if resources allow.

---

**Notes:**
- Product mix per segment informs targeted promotions.  
- Scatter plot and RFM scores provide additional behavioral insights for campaign segmentation.

---

## Data & Analysis Artifacts

**Access the data and analysis files used in this project:**

- 📊 [Excel Workbook with Pivot Tables](./analysis/printshop_rfm_analysis.xlsx)  
- 🧾 [Raw Dataset](./data/print_shop_orders_raw.csv)  
- 📈 [Power BI Dashboard Screenshot](./dashboard/Print_shop_All_View.PNG)

---

*© 2025 Peri Venetis – Print Shop Customer Segmentation using RFM Analysis*

---

*© 2025 Peri Venetis – Print Shop Customer Segmentation using RFM Analysis*
