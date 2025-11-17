# Print Shop Customer Segmentation using RFM Analysis

> Customer analytics project using Excel, Power Query, and RFM segmentation to identify best customers, at-risk groups, and actionable retention opportunities. A Power BI dashboard will be added to visualize customer behavior and segment insights.

### Table of Contents
- [Project Overview](#project-overview)
- [Tools Used](#tools-used)
- [Dataset Description](#dataset-description)
- [RFM Methodology](#rfm-methodology)
  - [Recency](#recency)
  - [Frequency](#frequency)
  - [Monetary](#monetary)
  - [RFM Scores](#rfm-scores)
- [Segmentation Rules](#segmentation-rules)
- [Key Insights](#key-insights)
- [Recommended Visuals](#recommended-visuals)
- [Business Recommendations](#business-recommendations)
- [Future Improvements](#future-improvements)
- [Dashboard](#dashboard)

---

## Project Overview

This project performs RFM segmentation on a dataset of approximately 1,000 print shop orders to understand customer behavior, identify high-value buyers, and highlight customers who may be slipping away.

The goal is to demonstrate:
- Analytical thinking  
- Business-oriented interpretation  
- Clean Excel modeling  
- Data storytelling with dashboard visuals

---

## Tools Used

- Excel
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

## RFM Scores

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

- **Best Customers**: Core group driving most revenue; highly engaged.  
- **Loyal Customers**: Repeat buyers who are very valuable; strong retention potential.  
- **Potential Loyal Customers**: Largest segment; represents biggest growth opportunity.  
- **Need Attention**: Customers with declining activity; require targeted re-engagement.  
- **At Risk**: Historically valuable but inactive customers; low numbers but high potential for recovery.

---

## Business Recommendations

**Best Customers**
- Provide VIP perks or exclusive offers.  
- Maintain engagement through personalized communications.

**Loyal Customers**
- Encourage referrals and reviews.  
- Offer bundles or loyalty rewards to increase lifetime value.

**Potential Loyal Customers**
- Use targeted onboarding or education flows.  
- Provide incentives to reinforce repeat purchasing.

**Need Attention**
- Send personalized reminders or light-touch campaigns.  
- Offer limited-time promotions to re-engage.

**At Risk**
- Execute time-sensitive win-back campaigns.  
- Provide individualized follow-up communication.

---

**See the raw data and analysis artifacts:**
- 📊 [Excel Workbook with Pivot Tables](./EDA/EDA_Sales_Insights.xlsx)  
- 🧠 [SQL Queries](./SQL)  
- 🧾 [Data Preparation Files](./Data/Profiling_and_Cleaning)  
- 📈 [Power BI Dashboard](./Dashboard)

---

*© 2025 Peri Venetis – DataFlow Cloud SaaS Analysis Project*
