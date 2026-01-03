# Power-Platform: Interactive Business Intelligence Dashboard

<b>Project Overview:</b></br>
Profits R Us is a fictitious business that I created to illustrate some of my capabilities.

This repository is a work in progress. Power BI solution is designed to analyze sales data and make recommended changes to the sales margins based upon current sales data. 
The adjustments allow the business to capture loss revenue through improperly adjusted margin. Other dashboards within Power BI show the customers, inventory and sales activities.

The project transforms raw data into actionable insights through a series of automated ETL processes and intuitive visualizations.

The reason why it's called a work in progress is that software always changes, new features are always added such as machine learning, python, R and other tools and features.
As new screens are created the site can be updated.

<b>Technical Highlights</b></br>
Data Modeling: The source files are text files that are imported into a SQL server. 
The Star Schema is created with 6 fact tables and 15 dimension tables for optimized performance.
Stored procedures are used to process the raw sales transactions and build out the dimensional and fact tables.
In addition, there are data that must be excuded before any analysis can be done. Some of the possible excluded items can be return items, 
staff/employee sales, discounts, warehouse transfers and so on. In addition to these, business rules are created to handle unique exclusions.

Data Sources:
In this portfolio, the data starts out as text files and imported into SQL sever.  The data use stored proceedures to split the data into fact and dimensional data. MS Access is used to control the process, edit business rules to meet client's requirements and to kick off various stored proceedures. Once the data is "mined", Power BI takes the data and presents it into meanngful reports that can be used by leadership.

Advanced DAX: Develops custom measures for time intelligence (YoY, MoM growth), Current Year Sales, Customer Lifetime Value, Inventory Sales, Top 100, and many others.

Power Query (M): 
Conducted extensive data cleaning, merges, table joins (primary and secondary), conditional formatting and any other features that is needed.

Machine Learning (ML): 
Power BI leverages machine learning capabilities to provide further insights of the existing data.

<b>Screen Shots</b>

Summary of the sales data
<img width="1161" height="621" alt="MainPage" src="https://github.com/user-attachments/assets/a5739733-9f7a-4260-aa3c-b5d75c073361" />

Customer Stats:
<img width="1167" height="655" alt="CustSales" src="https://github.com/user-attachments/assets/6123ddcf-24a5-4517-8403-658ca01b67a3" />

Margins:
<img width="1167" height="669" alt="12MoMargins" src="https://github.com/user-attachments/assets/94992182-375a-474a-bec8-3221b92c8bd0" />

Cluster With Power BI And Python:
<img width="1345" height="743" alt="image" src="https://github.com/user-attachments/assets/50bef176-ae71-460d-8016-9f7808ecc2c0" />
