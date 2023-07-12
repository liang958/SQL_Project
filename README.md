# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
This project is to use ETL process, obtain the reliable data for exploring 
, analyzing, and providing business insights. 


## Process

1. Data Extract and Explore
2. Data Cleaning 
3. Data Analyzing
4. Quality Assurance

## Results

1) For Data Cleaning:

Change inappropriate data unit for productprice and time, 
Set '(not set)', 'not available in demo data' to NULL in the country, city name.



2) For Data Analyzing:

Based on the reliable data, we research the business insights. For example, 
1. The United States, Atlanta has the highest level of transaction revenues.

2. The average product quantity In Toronto is 661.5,  The average product quantity
in Vancouver is 395.

3.There might have some patterns. Youtube is most popular category in worldwide.
But each city product category is different. In toronto, there are many product categories, 
most of orders are in drinkware, fun, office categories. But in Vancouver,
people  only buy products in four categories.


4. Top selling product is different in each country and city. In toronto, top selling product 
is custom decals. In ottawa, the top selling product
is men's t-shirt, it is a little be werid, as the summer is not
hot and long there. But anyway, there is no woman's category in top selling 
category in Canada.


5. There are not many revenue records in the table, but almost all of them are 
in the United States. After joining the tables we can find
cities such as Sunnyvale, Seattle, San Francisco, Chicago, and Mountain View are
the top 5 cities have the highest revenue.

6. 0.56% of website visitors actually make a purchase.


3) Quality Assurance:

In order to get the reliable results, Quality assurance process is used to check the completeness, uniqueness and consistency of the data.
The following QA steps are used for this project.
1. Checking for unique fields (productSKU, SKU).

2. Checking for date format YYYY-MM_DD for all_sessions table.

3. Checking for country, city column in all_sessions table for “(not set)”, “not available in demo data" set to NULL.

4. Checking for country and city column contain only alphabetic characters and have a length with a specified range.

5. Verify the totalTransactionRevenue contains valid decimal or integer values.

6. Checking for the ratio only contains 0-1 values.

7. Checking for date, the year, month, day in a reasonable range. 





## Challenges 
The most challenges I faced in the project is to find the relationships between these tables, I spend a lot of time in data quality assurance, 
and explore the business insight from the data

## Future Goals
I would like to continue to explore data in depth, and find out
whether the results can impact on business strategy.