# Power-Platform: Interactive Business Intelligence Dashboard

<b>Project Overview</b></br>
Profits R Us is a fictitious business that I created to illustrate some of my capabilities. The premis of the company is how to maximize the profits. Every business owners knows there's two ways to increase profits 1) reduce costs 2) manage prices (markups).

The downfall of reducing costs is that a business can only reduce costs to a certain point. Sometimes the only way to reduce costs is rebuild the business from the ground up and in 99% of the cases this will not work. The other method is to manage markups.  Most sales team doesn't have the technical expertise to analyze the data. But will hiring an data analyst be cost benefit? In small to mid size business, no. The possible revenue generated would not offset the cost of the developer.

Profits R Us fills this gap. We look at your existing sales data and make recommended changes to the margins.  Your A customers (who buy's the most) should have the lowest margins because you want to keep them happy and keep them buying from you, not your competitors.  Your D customers should have the higest margins because they buy only few items because they just happened to stop in your store or land on your web page.  Profit R Us looks at this spread and offers suggestions on tweaking your markups to maximize your profits.

This repository is a work in progress. Power BI solution is designed to analyze sales data and make recommended changes to the sales margins based upon current sales data. 
The adjustments allow the business to capture lost revenue through improperly adjusted margins. Other dashboards within Power BI show the customers, inventory and sales activities.

The project transforms raw data into actionable insights through a series of automated ETL processes and intuitive visualizations.

The reason why it's called a work in progress is that software always changes. New features are always added such as machine learning, python, R and other tools and features.
As new screens are created the site can be updated.

<b>Technical Highlights</b></br>
Data Modeling: The source files are text files that are imported into a SQL server. 
The Star Schema is created with 6 fact tables and 15 dimension tables for optimized performance.
Stored procedures are used to process the raw sales transactions and build out the dimensional and fact tables.
In addition, there are data that must be excuded before any analysis can be done. Some of the possible excluded items can be return items, 
staff/employee sales, discounts, warehouse transfers and so on. In addition to these, business rules are created to handle unique exclusions.

Data Sources:
In this portfolio, the data starts out as text files and imported into SQL sever.  The data use stored proceedures to split the data into fact and dimensional data. MS Access is used to control the process, edit business rules to meet client's requirements and to kick off various stored proceedures. Once the data is "mined", Power BI takes the data and presents it into meanngful reports that can be used by leadership.

Advanced DAX: Develops custom measures for Time Intelligence (YoY, MoM growth), Current Year Sales, Customer Lifetime Value, Inventory Sales, Top 100, and many others.

Power Query (M): 
Conducts data cleansing, merges, table joins (primary and secondary), conditional formatting and any other features that are needed.

Machine Learning (ML): 
Power BI leverages machine learning capabilities to provide further insights of the existing data.

Marketing:
Leverage Power BI to analyze data that can target marketing clients with special promotions to bring back old customers or keep current customers happy.  

Pricing:
One thing business never wants to do is lose money on sales. By analyzing costs and sales data the sales team can zero in potential trouble spots.

<b>Screen Shots </b>

Sales Data Summary:
<img width="1350" height="756" alt="image" src="https://github.com/user-attachments/assets/8a1e20ff-497e-4ea8-b692-ceb944dc50e6" />

Customer Stats:
<img width="1346" height="753" alt="image" src="https://github.com/user-attachments/assets/880c22a3-e307-41d0-a778-dd48bbf8c2e5" />

Margins:
<img width="1167" height="669" alt="12MoMargins" src="https://github.com/user-attachments/assets/94992182-375a-474a-bec8-3221b92c8bd0" />

Cluster With Machine Learning and Python:
<img width="1341" height="756" alt="image" src="https://github.com/user-attachments/assets/7dc162b3-c789-47a1-a677-45cc55bf6b7a" />
