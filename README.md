# Power-Platform: Interactive Business Intelligence Dashboard


<a href="https://htmlpreview.github.io/?https://github.com/Rusty112358/Power-Platform/blob/main/profits-r-us-sales-deck.html"> Sample Sales Deck</a>
<h3>Profits R Us: Strategic Margin Optimization & BI Ecosystem</h3>
<b>Project Overview</b></br>
Profits R Us is a specialized Proof of Concept (PoC) demonstrating the intersection of data engineering and strategic financial management. While traditional growth strategies focus on cost reduction—which often hits a floor of diminishing returns—this project focuses on the higher-leverage driver: <b>Dynamic Markup Management</b>
</br>
<b>Scenario</b></br>
A customer (Fred) comes in and buys milk all the time.  He knows the price of milk at 5 different stores because he regularly gets it for his family of 6. Every week he goes out and gets 2 or 3 gallons. Every once in a while he'll get a box of donuts. Because he's buying a lot of milk, he's price conscious, not so much with donuts. The goal for Fred is to protect the price of milk, but if the price of donuts goes up 10 cents, that won't hurt financially because it's a sometimes purchase. 
 
If Sally buys a lot of donuts for the studio production, she's very conscious of the price and if it goes up a penny, she'll be shopping somewhere else.  So the price of donuts needs to be protected for her.  Whereas, if the price goes up by 10 cents on milk, that's ok because she rarely buys the milk. The odds of her going price shopping for milk is very low. It's a lot more convient to buy the milk there at the same time vs going to another store which will take more time just to save a few pennies.

For someone who walks off the street and goes shopping, as the store owner, you want to give your customer the best prices but not at the cost of your business. For these individuals, they would get the higher price. Once they become your regular customers, you can adjust the prices to "preferred" customers. 

With flat pricing, it's one price for everyone and the store owner is losing money because they don't have the preferred pricing structure. This is why many of the larger retailers do their special pricing for contractors, store owners, gov't or school districts. This is the same as the "Loyal" customer pricing with their reward cards. 

<b>The Business Case</b></br>
Small to mid-sized enterprises (SMEs) often lack the capital to sustain a full-time data science department, yet they lose significant revenue to "flat" pricing models. Profits R Us bridges this gap by providing high-level analytical oversight without the overhead of a dedicated developer, ensuring the <b>Return on Investment (ROI)</b> remains positive for smaller operations.

<b>Technical Implementation & Strategy</b></br>
This repository features an end-to-end <b>Power BI ecosystem</b> designed to transform raw transactional data into a sophisticated pricing engine.

Automated ETL Pipeline: Robust data transformation processes convert fragmented sales records into structured, actionable datasets.

Segmented Margin Logic: The solution implements a tiered pricing strategy based on <b>Customer Lifetime Value</b> and buying patterns:

Tier A (High Volume): Optimized for retention and competitive defense through lean margins.

Tier D (Low Frequency): Optimized for <b>maximum margin capture</b>, identifying "walk-in" traffic where price sensitivity is lower.

360° Operational Dashboards: Beyond pricing, the solution provides total visibility into Inventory Lifecycle, Marketing, customer acquisition trends, and sales velocity.

<b>Vision & Scalability</b></br>
As a <b>Work in Progress</b>, this project is designed for continuous integration of modern data science tools. Future iterations will expand the tech stack to include:

    Predictive Modeling: Utilizing <b>Python and R</b> for advanced demand forecasting.

    Machine Learning: Implementing automated clustering for granular, AI-driven customer segmentation.

<b>Tools Utilized</b></br>
Data Modeling: The source files are text files that are imported into a SQL server 2022. 
The Star Schema is created with 6 fact tables and 15 dimension tables for optimized performance.
Stored procedures are used to process the raw sales transactions and build out the dimensional and fact tables.
In addition, there are data that must be excuded before any analysis can be done. Some of the possible excluded items can be return items, staff/employee sales, discounts, warehouse transfers and so on. In addition to these, business rules are created to handle unique exclusions.

Data Sources:
The process starts with the client text files that are download from their systems. Only four files are needed, Inventory, Sales, Customer and Sales Matrix.

Power BI:
Data/Graphical tool use to display data in logical and meaningful ways for leadership to make informed decisions.

Power BI - Row level security:
Restrict the viewing of data to the appropriate users.

Power BI - Advanced DAX: 
Develops custom measures for Time Intelligence (YoY, MoM growth), Current Year Sales, Customer Lifetime Value, Inventory Sales, Top 100, and many others.

Power App:
Power App is used to interact with the clients allowing them to adjust criterias such as what to exclude from the sales analysis: employee purchases, department transfers and so on.

Power Automate:
Power Automate manages the data pipeline from the clients' raw text files to processing new/updated data into SQL Server.

MS Access:
Allows the admin/technical staff to run and update the various processes by kicking off various stored proceedures individually or batch processes.

Power Query (M): 
Conducts data cleansing, merges, table joins (primary and secondary), conditional formatting and any other features that are needed.

Machine Learning (ML): 
Power BI leverages machine learning capabilities to provide further insights of the existing data.

AI Agents:
An agent is a software program or system designed to perceive its environment, make decisions, and take actions to achieve specific goals autonomously. These agents operate without direct human intervention and can be classified based on their characteristics, such as being reactive or proactive, and operating in fixed or dynamic environments.

Marketing:
Leverage Power BI to analyze data that can target marketing clients with special promotions to bring back old customers and keep current customers happy.  

Pricing:
One thing businesses never wants to do is lose money on sales. By analyzing costs and sales data, the sales team can zero-in potential trouble spots.

<b>SQL Server SSMS v22</b></br>
SSMS is an integrated environment developed by Microsoft for managing, administering, and configuring all components of SQL infrastructure.

SSRS:
SQL Server Reporting Services v2022 is a solution that customers deploy on their own premises for creating, publishing, and managing reports, then delivering them to the right users in various ways: Email, mobile device, and web browsers. SSRS can produce simple reports or data extraction for imports to other tools such as Power BI or Excel. For this demo, SSRS is not used because there are far better tools such as Excel, Power BI, Tableau, etc can be used. Below are samples SSRS reports.

<img width="730" height="654" alt="image" src="https://github.com/user-attachments/assets/37e622e9-2f15-4dcf-acae-de18328b98e6" />

<img width="734" height="659" alt="image" src="https://github.com/user-attachments/assets/f6ba2122-451b-496c-ba87-bce85f92327e" />



<b>SQL Server v2022</b></br>
<b>Sample of complex CTE <br>For the top 1000 items sold and what were the other items that were purchased with those items.</b>

```
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


<b>Screen Shots </b>

Sales Data Summary:
<img width="1350" height="756" alt="image" src="https://github.com/user-attachments/assets/8a1e20ff-497e-4ea8-b692-ceb944dc50e6" />

Customer Stats:
<img width="1346" height="753" alt="image" src="https://github.com/user-attachments/assets/880c22a3-e307-41d0-a778-dd48bbf8c2e5" />

Margins:
<img width="1167" height="669" alt="12MoMargins" src="https://github.com/user-attachments/assets/94992182-375a-474a-bec8-3221b92c8bd0" />

Cluster With Machine Learning and Python:
<img width="1341" height="756" alt="image" src="https://github.com/user-attachments/assets/7dc162b3-c789-47a1-a677-45cc55bf6b7a" />
