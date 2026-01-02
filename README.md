# Power-Platform: Interactive Business Intelligence Dashboard

Project Overview
This repository is a work in progress Power BI solution designed to analyze sales data and make recommended changes to the sales margins based upon current sales data. 
The adjustments allows the business to capture loss revenue through bad margin practices. Other dashboards shows the customers, inventory and sales activities.

The project transforms raw data into actionable insights through a series of automated ETL processes and intuitive visualizations.

The reason why it's called a work in progress, software always changes, new features are always added such as machine learning, python, R and other tools and features.
As new screens are created the site will get updated.

<b>Technical Highlights</b></br>
Data Modeling: The source files are text files that are imported into a sql server. 
The Star Schema is created with 6 fact tables and between 15 dimension tables for optimized performance.
Stored procedures are used to process the raw sales transactions and build out the dimensional and fact tables.
In addition there are data that must be excuded before any analysis can be done.  Return items, 
staff/employee sales, discounts, warehouse transfers and so on. In addition to these, Business rules are created to handle unique exclusions.

Advanced DAX: Developed custom measures for Time Intelligence (YoY, MoM growth), Current year sales, Customer Lifetime Value, Inventory sales, Top 100, and many others.

Power Query (M): 
Conducted extensive data cleaning, including [e.g., unpivoting, merging queries, and conditional formatting].
