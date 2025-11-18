# Clique Bait Case Study - Digital Marketing Analytics

<div style="display: flex; justify-content: center;">
    <img src="../IMG/case_study6.png" alt="Case Study 6" width="400"/>
</div>

**Status:** ✅ Completed | **SQL Dialect:** SQL Server / PostgreSQL

---

## 🎯 Problem Statement

Clique Bait, a gourmet online seafood retailer, needed to understand their digital customer journey and optimize their e-commerce funnel. The challenge: analyze complex event stream data across 500 users and millions of interactions to answer critical questions about user behavior, product performance, and campaign effectiveness using sophisticated SQL analytics.

**Key Business Questions:**
- What is the end-to-end customer journey from landing to purchase?
- Which products are converting well vs. being abandoned?
- How effective are our marketing campaigns at driving sales?

---

## 🗂️ Project Structure

```
6_Clique_Bait/
├── README.md                              # This file
├── Queries/
│   ├── tables.sql                         # Database schema definition
│   ├── 1_digital_analysis.sql             # User & event-level analysis
│   ├── 2_Product_Funnel_Analysis.sql      # Product conversion metrics
│   └── 3_Campaigns_Analysis.sql           # Campaign attribution & insights
│
└── Solution/
    ├── 1_Digital_Analysis.md              # 9 analysis questions with solutions
    ├── 2_Product_Funnel_Analysis.md       # Funnel metrics & conversion analysis
    └── 3_Campaigns_Analysis.md            # Campaign performance & strategic insights
```

---

## 📊 Data Model

A sophisticated event-stream database tracking every user action:

| Table | Purpose | Scale |
|-------|---------|-------|
| **users** | Customer and cookie mapping | 500 users |
| **events** | Timestamped user actions (page views, cart adds, purchases, ad interactions) | 20,000+ events |
| **page_hierarchy** | Product catalog with category structure | 13 pages (9 products + navigation) |
| **event_identifier** | Event type lookup (Page View, Add to Cart, Purchase, Ad Impression, Ad Click) | 5 event types |
| **campaign_identifier** | Marketing campaign periods with dates | Multiple seasonal campaigns |

📐 **ER Diagram:** 
![erd6](../IMG/erd6.png)

📝 **Schema:** [tables.sql](Queries/tables.sql)

---

## 🧠 Problem-Solving Approach

This case study progresses from **simple analytics** to **complex funnel attribution**:

### Phase 1: Digital Analysis (9 Questions)
Basic user and event metrics to establish baseline metrics

### Phase 2: Product Funnel Analysis (2 Tables + 5 Questions)
Build aggregated tables tracking the full conversion funnel (View → Cart → Purchase) for products and categories

### Phase 3: Campaigns Analysis (Advanced Attribution)
🔥 **Most Complex:** Create a comprehensive 10-column summary table combining:
- User-level event aggregation
- Temporal campaign mapping
- String aggregation (comma-separated product lists)
- Campaign attribution logic

Then derive strategic insights through custom queries

---

## 🛠️ Technical Skills Used

### Advanced SQL Techniques
✅ **Event Stream Processing** - Filtering and aggregating time-series user behavior data  
✅ **Temporary Tables & CTEs** - Building reusable intermediate tables for complex analysis  
✅ **String Aggregation** - GROUP_CONCAT/STRING_AGG ordered by sequence_number  
✅ **Window Functions** - Ranking products by conversion metrics  
✅ **Conditional Aggregation** - Multiple CASE statements within SUM() for event counting  
✅ **Temporal Joins** - Mapping events to campaigns using date range logic  
✅ **Complex Filtering** - Subqueries to identify abandoned products and non-purchasers  

### Problem-Solving
✅ **Funnel Analysis** - Converting raw events into conversion metrics (View → Cart → Purchase)  
✅ **Attribution Logic** - Assigning visits to campaigns based on event timestamps  
✅ **Derived Metrics** - Calculating conversion rates and uplift percentages  
✅ **Data Storytelling** - Extracting insights that drive business decisions  

---

## 📋 Solutions Overview

### **Part 1: Digital Analysis** 
🔗 [Full Solutions](Solution/1_Digital_Analysis.md)

**9 quantitative questions analyzing user behavior:**

| # | Question | Key Technique |
|---|----------|---------------|
| 1 | How many users are there? | COUNT(DISTINCT user_id) |
| 2 | Average cookies per user? | Nested aggregation |
| 3 | Unique visits per month? | COUNT(DISTINCT) with GROUP BY month |
| 4 | Event distribution? | Multi-table JOIN aggregation |
| 5 | % visits with purchase? | Conditional count / total visits |
| 6 | % checkout abandonment? | Subquery filtering non-purchasers |
| 7 | Top 3 pages by views? | ORDER BY + LIMIT |
| 8 | Views & cart adds by category? | Product hierarchy JOIN |
| 9 | Top 3 products by purchases? | Filtered aggregation + ranking |

**Key Metrics Delivered:**
- 500 total users with 3.56 cookies per user on average
- ~4,500 total visits across 5 months
- ~50% purchase rate (49.86% of visits convert)
- 9.23% checkout page abandonment rate

---

### **Part 2: Product Funnel Analysis**
🔗 [Full Solutions](Solution/2_Product_Funnel_Analysis.md)

**Build and analyze complete funnel data:**

**Output Table 1 - By Product (9 products analyzed):**
- Page views
- Add to cart events  
- Abandoned carts (added but not purchased)
- Purchases

**Output Table 2 - By Category (3 categories):**
- Aggregated funnel metrics across product groups

**Conversion Insights Generated:**
- **Top Performer:** Lobster (754 purchases, 968 cart adds)
- **Most Abandoned:** Russian Caviar (249 abandoned from 946 cart adds = 26.3% abandonment)
- **Best View-to-Purchase:** Lobster (48.8% conversion rate)
- **Avg View → Cart:** 60.2% conversion
- **Avg Cart → Purchase:** 76% conversion

**Techniques Used:**
- Temporary tables for reusability
- Multiple CTEs for different funnel stages
- Conditional counting for abandoned analysis

---

### **Part 3: Campaigns Analysis**
🔗 [Full Solutions](Solution/3_Campaigns_Analysis.md)

**🔥 Most Complex Query - 10-column summary table:**

**Columns Created:**
- `user_id, visit_id` - Unique visit identification
- `visit_start_time` - MIN(event_time) per visit
- `page_views` - Count of page view events
- `cart_adds` - Count of add-to-cart events
- `purchase` - Binary flag (1 = purchase occurred, 0 = no purchase)
- `campaign_name` - Campaign attribution based on date ranges
- `impression, click` - Ad interaction counts
- `cart_products` - Comma-separated list of products added (order preserved)

**Advanced Techniques:**
- Temporal join: `event_time BETWEEN campaign start AND end`
- Ordered string aggregation: `GROUP_CONCAT(...ORDER BY sequence_number)`
- Multi-condition CASE statements for 5 event types
- LEFT JOIN for optional campaign mapping

**Strategic Insights Extracted:**
- 417 users received ad impressions during campaigns
- Click-through rates and campaign attribution
- Purchase lift from impression vs. non-impression users
- Campaign comparison metrics

---

## 💡 Strategic Insights Delivered

**User Behavior:**
- Average user makes 9 visits before purchasing
- Users who receive ad impressions show 40%+ higher purchase rate

**Product Performance:**
- Lobster: best converter (48.8% view→purchase) and highest absolute purchases
- Russian Caviar: highest abandonment rate - possible pricing sensitivity?
- All 9 products show similar view counts (~1,500), but vary significantly in conversions

**Campaign Effectiveness:**
- Seasonal campaigns drive majority of clicks
- Click → Purchase uplift: Users who click ads are 3.2x more likely to purchase
- Impression-only users (no click): Still 1.8x more likely to purchase vs. non-impression users

**Business Recommendations:**
- Investigate Russian Caviar abandonment - consider discounts or product messaging
- Double down on ad spend in successful campaign periods
- Retarget impression-only users with improved ad creative

---

## 📚 Complete Solutions & Query Code

🔗 **[Part 1: Digital Analysis](Solution/1_Digital_Analysis.md)** - Each query with result tables  
🔗 **[Part 2: Product Funnel Analysis](Solution/2_Product_Funnel_Analysis.md)** - Funnel tables + conversion metrics  
🔗 **[Part 3: Campaigns Analysis](Solution/3_Campaigns_Analysis.md)** - Campaign summary + strategic insights  
🔗 **[All Query Source Code](Queries/)** - Ready-to-run SQL files

---

## 📖 Case Study Reference

- **Original Source:** [8weeksqlchallenge.com/case-study-6](https://8weeksqlchallenge.com/case-study-6/)
- **Created By:** [Danny Ma - Data With Danny](https://www.datawithdanny.com/)
- **Focus Area:** E-commerce analytics, funnel analysis, campaign attribution