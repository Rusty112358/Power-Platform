# Power-Platform: Interactive Business Intelligence Dashboard


<a href="https://htmlpreview.github.io/?https://github.com/Rusty112358/Power-Platform/blob/main/profits-r-us-sales-deck.html"> Sample Sales Deck</a>

## Profits R Us — Strategic Margin Optimization & BI Ecosystem

---

## Project Overview

**Profits R Us** is a full end-to-end Proof of Concept (PoC) demonstrating the intersection of data engineering and strategic financial management.

Traditional growth strategies often focus on cost reduction — but cost cutting hits a floor of diminishing returns. This project focuses on a higher-leverage driver: **Dynamic Markup Management**. By analyzing customer buying behavior and segmenting pricing tiers intelligently, businesses can protect margins on price-sensitive items while capturing maximum value on low-sensitivity purchases.

---

## The Business Problem

Consider two customers:

- **Fred** buys milk for his family of 6 every week — he knows the price at five different stores and is highly price-conscious about milk. He occasionally picks up donuts without thinking about the price.
- **Sally** buys donuts regularly for a studio production and watches that price closely. She rarely buys milk and won't price-shop for it.
- **Walk-in customers** shop infrequently and have low price sensitivity across the board.

With **flat pricing**, the store owner is leaving money on the table — they can't protect margins on high-sensitivity items for loyal customers while capturing premium pricing from occasional buyers. This is exactly why major retailers offer contractor pricing, government/school district pricing, and loyalty reward programs.

**Profits R Us solves this for small and mid-sized enterprises (SMEs)** that lack the capital for a full data science department but still need sophisticated pricing intelligence.

---

## Technical Stack

### Data Architecture

| Component | Details |
|---|---|
| **Source Data** | Client text files (Inventory, Sales, Customer, Sales Matrix) |
| **Database** | SQL Server 2022 |
| **Schema** | Star Schema — 6 fact tables, 15 dimension tables |
| **ETL** | Stored procedures for raw data processing, dimensional modeling, and business rule exclusions |

**Business rule exclusions handled:** return items, employee/staff sales, discounts, warehouse transfers, and custom client-specific rules.

---

### Tools & Technologies

**Power BI**
- Interactive dashboards for leadership decision-making
- Row-Level Security (RLS) restricting data views by user role
- Advanced DAX measures: Time Intelligence (YoY, MoM growth), Current Year Sales, Customer Lifetime Value, Inventory Sales, Top 100 analysis, and more
- Machine Learning integration for customer clustering and predictive insights

**Power Apps**
- Client-facing interface allowing users to configure exclusion criteria (employee purchases, department transfers, etc.) without technical intervention

**Power Automate**
- Manages the full data pipeline from raw client text files through to processed SQL Server tables
- Automated triggers for new and updated data ingestion

**Power Query (M)**
- Data cleansing, merges, table joins (primary and secondary), conditional formatting, and custom transformations

**MS Access**
- Administrative tool for technical staff to execute stored procedures individually or as batch processes

**SQL Server 2022 / SSMS v22**
- Complete SQL infrastructure management, administration, and configuration
- Complex CTEs, stored procedures, and dimensional modeling

---

## Pricing Strategy: Tiered Margin Logic

The solution implements a four-tier pricing engine based on **Customer Lifetime Value** and purchase frequency:

| Tier | Customer Type | Pricing Strategy |
|---|---|---|
| **Tier A** | High-volume loyal customers | Competitive/lean margins — retention and loyalty |
| **Tier B** | Customer Group to Specific Item  (Contractors, Gov't, etc) | Preferred pricing — reward engagement |
| **Tier C** | Customer Group to Item Group (Plumbing, HVAC, Electrical, etc) | Preferred pricing — reward engagement |
| **Tier D** | Walk-in / infrequent buyers | Maximum margin capture — low price sensitivity |

---

## Key Features

- **360° Operational Dashboards** — Inventory lifecycle, marketing performance, customer acquisition trends, and sales velocity
- **Customer Lifetime Value (CLV) Analysis** — Identify your most valuable customers and protect those relationships
- **Dynamic Markup Management** — Item-level and customer-segment-level pricing controls
- **Machine Learning Clustering** — Python and Power BI integration for AI-driven customer segmentation
- **Marketing Analytics** — Target promotions to win back lapsed customers and reward active ones
- **Margin Protection Alerts** — Identify pricing trouble spots before they impact profitability

---
## SSRS Sample
<img width="730" height="654" alt="image" src="https://github.com/user-attachments/assets/37e622e9-2f15-4dcf-acae-de18328b98e6" />

<img width="734" height="659" alt="image" src="https://github.com/user-attachments/assets/f6ba2122-451b-496c-ba87-bce85f92327e" />



## Sample SQL — Complex CTE

**Top 1,000 items sold and what other items were co-purchased with them:**

```sql
	WITH Top1000Items as (
    SELECT  Top (@TopItems)
        ItemID, 
        SUM(Units_Sold) AS total_quantity
    FROM 
        [P2_Test].[dbo].[RawClean]
    Group by
        ItemID
    Order by 
        SUM(Units_Sold) Desc
    )
    , TopSellingItems AS (
    SELECT 
        Invoice_Number,
        rc.ItemID ID, 
        SUM(Units_Sold) AS total_quantity
    FROM 
        [P2_Test].[dbo].[RawClean] rc
    join
        Top1000Items ti on ti.ItemID = rc.ItemID
--   where
--       ItemID = '15667'
    GROUP BY 
        Invoice_Number,
        rc.ItemID
--    having count(Invoice_Number) > 1
--    ORDER BY 
--        total_quantity DESC
)
, RankedPurchases AS (
    SELECT
        tsi.ID,
        p.ItemID,
        SUM(p.Units_Sold) AS purchased_quantity
        , RANK() OVER (PARTITION BY tsi.ID ORDER BY tsi.ID, SUM(p.Units_Sold) DESC) AS rank
    FROM 
        [P2_Test].[dbo].[RawClean] p
    JOIN 
        TopSellingItems tsi ON p.Invoice_Number = tsi.Invoice_Number
    GROUP BY 
        tsi.ID,
        p.ItemID 
)
SELECT 
    rp.*
Into Top1000Items
FROM 
    RankedPurchases rp
WHERE 
    rp.rank <= @TopRank
ORDER BY 
    rp.ID,
    rp.rank,
    rp.ItemID, 
    rp.purchased_quantity;

```


## Some of the Power BI Screen Shots

Sales Data Summary:
<img width="1350" height="756" alt="image" src="https://github.com/user-attachments/assets/8a1e20ff-497e-4ea8-b692-ceb944dc50e6" />

Customer Stats:
<img width="1346" height="753" alt="image" src="https://github.com/user-attachments/assets/880c22a3-e307-41d0-a778-dd48bbf8c2e5" />

Margins:
<img width="1167" height="669" alt="12MoMargins" src="https://github.com/user-attachments/assets/94992182-375a-474a-bec8-3221b92c8bd0" />

Cluster With Machine Learning and Python:
<img width="1341" height="756" alt="image" src="https://github.com/user-attachments/assets/7dc162b3-c789-47a1-a677-45cc55bf6b7a" />
