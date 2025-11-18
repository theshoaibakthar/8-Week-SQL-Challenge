# Danny's Diner SQL Case Study

<div style="display: flex; justify-content: center;">
    <img src="../IMG/case_study1.png" alt="Case Study 1" width="400"/>
</div>

**Status:** ✅ Completed | **SQL Dialect:** PostgreSQL 13

---

## 🎯 Problem Statement

A newly opened Japanese restaurant needed to analyze customer transaction data to drive strategic decisions on their loyalty program. The challenge: write sophisticated SQL queries to extract actionable insights about customer behavior, spending patterns, and membership impact from a normalized relational database.

**Key Constraint:** All answers must be derived from a single SQL statement per question, requiring careful query composition and optimization.

---

## 🗂️ Project Structure

```
1_Dannys_Diner/
├── README.md                              # This file
├── Queries/
│   ├── tables.sql                         # Database schema definition
│   ├── 1_Case_Study_Qns.sql               # All 10 case study queries
│   └── 2_Bonus_qns.sql                    # 2 advanced bonus queries
│
└── Solution/
    ├── 1_Case_Study_Qns.md                # Solutions with detailed explanations
    └── 2_Bonus_Qns.md                     # Bonus solutions with approaches
```

---

## 📊 Data Model

Three normalized tables with transactional relationships:

| Table | Purpose | Key Fields |
|-------|---------|-----------|
| **sales** | Customer transactions | customer_id, order_date, product_id |
| **menu** | Product catalog | product_id, product_name, price |
| **members** | Loyalty program enrollment | customer_id, join_date |

📐 **ER Diagram:**
![erd1](../IMG/erd1.png)

📝 **Schema:** [tables.sql](Queries/tables.sql)

---

## 🧠 Problem-Solving Approach

### Query Complexity Progression
The case study is structured to build progressively:

1. **Foundational Queries (Q1-Q4)** - Basic aggregations and joins
2. **Intermediate Queries (Q5-Q8)** - Window functions, CTEs, and temporal logic
3. **Advanced Queries (Q9-Q10)** - Complex business rule implementation with conditional logic
4. **Bonus Queries** - Denormalization and conditional ranking patterns

### Key Techniques Applied
- **Window Functions** - DENSE_RANK(), RANK() with PARTITION BY for ranking within groups
- **CTEs (Common Table Expressions)** - Multi-stage query composition for clarity and reusability
- **Complex JOINs** - LEFT JOINS with conditional filtering to handle non-members
- **CASE Statements** - Conditional aggregation for business logic (loyalty multipliers, membership status)
- **Date Arithmetic** - Interval calculations for membership eligibility windows
- **Subqueries** - Nested queries for filtering ranked results

---

## 🎯 Solutions Overview

### **10 Core Case Study Questions**

#### Group 1: Customer & Product Fundamentals (Q1-Q4)
**What you'll find in [Solution Q1-Q4](Solution/1_Case_Study_Qns.md#1-what-is-the-total-amount-each-customer-spent-at-the-restaurant):**
- Total spending aggregation
- Visit frequency counting (DISTINCT dates)
- First purchase identification (window functions)
- Most popular product overall (ORDER BY + LIMIT)

#### Group 2: Member-Centric Analysis (Q5-Q8)
**What you'll find in [Solution Q5-Q8](Solution/1_Case_Study_Qns.md#5-which-item-was-the-most-popular-for-each-customer):**
- Favorite product per customer (CTEs + window ranking)
- First post-membership purchase (temporal filtering)
- Pre-membership purchase analysis (date comparisons)
- Member onboarding spending patterns

#### Group 3: Loyalty Points Logic (Q9-Q10)
**What you'll find in [Solution Q9-Q10](Solution/1_Case_Study_Qns.md#9-if-each-1-spent-equates-to-10-points-and-sushi-has-a-2x-points-multiplier-how-many-points-would-each-customer-have):**
- **Q9:** Multi-condition CASE logic for loyalty multipliers
- **Q10:** 🔥 **Most Complex** - Time-windowed bonus calculation combining:
  - First-week membership 2x multiplier (with interval arithmetic)
  - Product-specific multipliers (sushi 2x)
  - Temporal filters (end of month)
  - Multi-table joins with business rules

### **2 Advanced Bonus Challenges**

**What you'll find in [Solution Bonus](Solution/2_Bonus_Qns.md):**

| Bonus | Challenge | SQL Techniques |
|-------|-----------|-----------------|
| **Bonus 1: Join All The Things** | Create denormalized view showing member status at purchase time | 3-table LEFT JOINs, temporal CASE logic |
| **Bonus 2: Rank All The Things** | Apply conditional ranking (NULL for non-members) | Nested CTEs, conditional window functions |

---

## 🛠️ Technical Skills Used

### SQL
✅ **Window Functions** - Properly scoped PARTITION BY and ORDER BY for ranking logic  
✅ **CTEs** - Staged query composition for readability and maintenance  
✅ **Date Operations** - Interval arithmetic (`join_date + INTERVAL '6 days'`) for business windows  
✅ **Conditional Aggregation** - CASE statements within SUM() for multi-rule calculations  
✅ **Join Strategies** - LEFT JOINs to handle non-members while preserving data  
✅ **Set Operations** - GROUP BY with aggregation functions (COUNT, SUM, COUNT DISTINCT)  

### Problem-Solving
✅ **Requirement Analysis** - Interpreting business rules (e.g., "first week" = 7-day window including join date)  
✅ **Edge Case Handling** - Customers on different membership timelines; non-members still in dataset  
✅ **Multi-Step Logic** - Q10 requires combining 3 different point multiplier rules into one aggregation  
✅ **Query Optimization** - Using CTEs to avoid recalculating intermediate results  

---

## 📈 Business Insights Extracted

Through these queries, I extracted actionable insights like:

- **Customer A:** $76 total spend, loyal to ramen (3x purchases), early member → 1,370 loyalty points
- **Customer B:** Most frequent visitor (6 visits) with balanced menu preferences → 820 loyalty points  
- **Customer C:** No membership, low engagement ($36 spent, 2 visits) → **retention opportunity**
- **Product Star:** Ramen dominates with 8 purchases (50% of transactions)
- **Pre-membership Behavior:** Members spent $25-$40 before joining → strong onboarding ROI potential

These weren't just data points—they represent the kind of strategic analysis that drives business decisions on loyalty program expansion and personalization.

---

## 📚 Complete Solutions & Explanations

🔗 **[Full Case Study Solutions (Q1-Q10)](Solution/1_Case_Study_Qns.md)** - Each query includes SQL code, result tables, and logical explanation  
🔗 **[Bonus Solutions](Solution/2_Bonus_Qns.md)** - Advanced queries with strategic approaches  
🔗 **[All Queries Source Code](Queries/1_Case_Study_Qns.sql)** - Ready-to-run SQL files

---

## 📖 Case Study Reference

- **Original Source:** [8weeksqlchallenge.com/case-study-1](https://8weeksqlchallenge.com/case-study-1/)
- **Created By:** [Danny Ma - Data With Danny](https://www.datawithdanny.com/)

