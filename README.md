# 8 Week SQL Challenge

A comprehensive portfolio project demonstrating advanced SQL problem-solving skills through complex real-world case studies from the [8 Week SQL Challenge](https://8weeksqlchallenge.com/) by [Danny Ma](https://www.datawithdanny.com/).

## 🎯 Project Overview

This repository showcases my ability to solve complex data analysis problems using SQL. Each case study represents realistic business scenarios requiring intermediate to advanced SQL techniques including window functions, CTEs, complex joins, and data aggregation strategies.

**Completed Case Studies:** 2 of 8
- ✅ Case Study #1: Danny's Diner
- ✅ Case Study #6: Clique Bait

## Case Studies & Skills Demonstrated

### 1. **Danny's Diner** ✅
**Business Context:** A restaurant needs customer insights to drive loyalty program decisions.

**SQL Skills Demonstrated:**
- Complex JOINs (LEFT, INNER) across multiple tables
- Window functions (DENSE_RANK, RANK) for ranking and partitioning
- Date-based filtering and aggregations
- CASE statements for conditional logic
- CTEs (Common Table Expressions) for query optimization
- Advanced point calculation logic with business rules

**Key Accomplishments:**
- Solved 10 core questions covering customer spending, visit frequency, and preferences
- Implemented sophisticated loyalty point system with time-based multipliers
- Created member status indicators with membership timeline analysis
- Generated denormalized views for business intelligence

### 6. **Clique Bait** ✅
**Business Context:** An e-commerce platform needs digital analytics and funnel analysis for campaign optimization.

**SQL Skills Demonstrated:**
- Event tracking and user journey analysis
- Funnel analysis with multi-step conversion tracking
- Complex aggregations with multiple GROUP BY levels
- Product performance analysis and ranking
- Campaign effectiveness metrics
- User behavior pattern recognition

**Key Accomplishments:**
- Analyzed digital behavior across multiple event types
- Tracked customer journeys through purchase funnels
- Evaluated campaign performance with retention metrics
- Designed views for marketing analytics reporting

## Project Structure

```
8-Week-SQL-Challenge/
├── 1_Dannys_Diner/
│   ├── README.md                          # Full case study with solutions & insights
│   ├── Queries/
│   │   ├── tables.sql                     # Database schema
│   │   ├── 1_Case_Study_Qns.sql           # Main queries
│   │   └── 2_Bonus_qns.sql                # Advanced bonus queries
│   └── Solution/
│       ├── 1_Case_Study_Qns.md            # Solution explanations
│       └── 2_Bonus_Qns.md                 # Bonus solutions
│
├── 6_Clique_Bait/
│   ├── README.md                          # Full case study with solutions & insights
│   ├── Queries/
│   │   ├── tables.sql                     # Database schema
│   │   ├── 1_digital_analysis.sql
│   │   ├── 2_Product_Funnel_Analysis.sql
│   │   ├── 3_Campaigns_Analysis.sql
│   │   └── erd_dbdiagram.txt
│   └── Solution/
│       ├── 1_Digital_Analysis.md
│       ├── 2_Product_Funnel_Analysis.md
│       └── 3_Campaigns_Analysis.md
│
├── IMG/                                   # Case study images & ERDs
└── README.md                              # This file
```

## Quick Start

To review my SQL problem-solving work:

1. **Start with case study folders** - Each contains a detailed `README.md` with full solutions
2. **Review the SQL queries** - Located in the `Queries/` subdirectories
3. **Check schema design** - `tables.sql` shows how I worked with the data structures
4. **See my approach** - Solution files include explanations and business logic

## Technical Capabilities

### Advanced SQL Techniques
- **Window Functions:** ROW_NUMBER(), RANK(), DENSE_RANK(), LAG(), LEAD() with PARTITION BY and ORDER BY clauses
- **CTEs:** Multi-level Common Table Expressions for complex query composition and optimization
- **Complex JOINs:** INNER, LEFT, RIGHT, FULL OUTER joins with conditional logic
- **Date Functions:** Date arithmetic, filtering, and grouping strategies
- **Aggregations:** SUM(), COUNT(), COUNT(DISTINCT), AVG(), MAX(), MIN() with GROUP BY
- **CASE Statements:** Conditional logic for business rule implementation
- **Subqueries:** Nested queries and correlated subqueries
- **String Functions:** SUBSTRING, CONCAT, TRIM, UPPER, LOWER for data manipulation

### Problem-Solving Approach
✅ **Business Understanding** - I analyze the business context before writing queries  
✅ **Query Optimization** - I use CTEs and window functions for efficient, readable queries  
✅ **Data Validation** - I verify results against expected outputs and business logic  
✅ **Code Quality** - I write clean, well-formatted SQL with meaningful aliases and comments  
✅ **Multiple Solutions** - I implement different approaches and choose the most efficient

## Featured Highlights

### Danny's Diner - Loyalty Program Analytics
Solved 10+ complex questions demonstrating:
- Ranking and partitioning for customer purchase analysis
- Time-based conditional logic for first-week bonus calculations
- Multi-level aggregations for customer lifetime value
- Member vs. non-member segmentation

```sql
-- Example: Sophisticated points calculation with time-based multipliers
WITH program_validity AS (
	SELECT 
		*,
		DATE(join_date + INTERVAL '6 days') AS valid_date
	FROM members
)
SELECT
	s.customer_id,
	SUM(CASE
		WHEN s.order_date BETWEEN p.join_date AND p.valid_date THEN m.price * 10 * 2
		WHEN m.product_name = 'sushi' THEN m.price * 10 * 2
		ELSE m.price * 10
	END) AS total_points
FROM sales s
JOIN program_validity p ON s.customer_id = p.customer_id
JOIN menu m ON s.product_id = m.product_id
WHERE s.order_date <= '2021-01-31'
GROUP BY s.customer_id;
```

### Clique Bait - Digital Analytics & Funnel Analysis
Demonstrated expertise in:
- User journey tracking and event sequence analysis
- Multi-step conversion funnel analysis
- Customer segmentation by behavior patterns
- Campaign performance metrics and attribution

## Why This Project Matters

This project demonstrates my ability to:

1. **Understand Complex Requirements** - Translate business questions into SQL solutions
2. **Write Production-Quality Code** - Clean, optimized, and well-documented queries
3. **Solve Hard Problems** - Handle multi-table joins, window functions, and complex logic
4. **Think Analytically** - Break down problems and design efficient solutions
5. **Deliver Results** - Provide accurate answers to complex data analysis questions

## Next Case Studies in Progress

- **Case Study #2:** Pizza Runner - Data cleaning and transformation
- **Case Study #3:** Foodie-Fi - Subscription analytics and retention
- **Case Study #4:** Data Bank - Running totals and financial calculations
- **Case Study #5:** Data Mart - Sales performance analysis
- **Case Study #7:** Balanced Tree Clothing Co. - Advanced product analytics
- **Case Study #8:** Fresh Segments - Complex aggregations and JSON

## Challenge Details

- **Creator:** [Danny Ma - Data With Danny](https://www.datawithdanny.com/)
- **Official Website:** https://8weeksqlchallenge.com/
- **Difficulty:** Intermediate to Advanced
- **Focus Areas:** Real-world SQL problem solving for analytics and data science roles

---

*This portfolio project demonstrates my practical SQL expertise for data analyst, data engineer, and database professional roles.*

