# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
This project is to use ETL process, obtain the reliable data for exploring 
and analyzing, and might be used to provide some business solutions. 


## Process

1. Data Extract and Explore
2. Data Cleaning 
3. Data Analyzing
4. Quality Assurance

## Results

1) For Data Cleaning:

Change inappropriate data unit for productprice and time, standardize the country, city name.



2) For Data Analyzing:

Based on the reliable data, we research the business insight. For example, 
1. The United States, Atlanta has the highest level of transaction revenues.

2. The average product quantity In Toronto is 661.5,  The average product quantity
in Vancouver is 395.

3.There might be have some patterns in the types (product categories) 
of products ordered from visitors in each city and country. For example,
There are many product categories in Toronto, 
and most of the orders are fro drinkware, fun, office categories
But in Vancouver, people don't buy too many products in four categories.

4. The best-selling products may be different in each country and city
For example, in Toronto, the top-selling product category
is the office, which probably makes sense. Best selling product in Ottawa
is men's t-shirts, which is a bit odd since summer isn't
hot and long there. But in any case, there is no women's category among the best-selling categories
in Canada. Overall, we can still find that YouTube's most popular
the best-selling product categories in Canada and globally.

5. There are not many revenue records in the table, but almost all of them are 
in the United States. After joining the tables we can find
cities such as Sunnyvale, Seattle, San Francisco, Chicago, and Mountain View are
the top 5 cities have the highest revenue.

6. 0.56% of website visitors actually make a purchase.


3) Quality Assurance:

In order to get the reliable results, Quality assurance process is used to check the completeness, uniqueness and consistency of the data.
The following QA steps are used for this project.
1. Checking for unique fields (productSKU).

2. Checking for the date format YYYY-MM_DD for all_sessions table.

3. Checking for country, city column in all_sessions table for “(not set)”, “not available in demo data set” to NULL.

4. Checking for country and city column contain only alphabetic characters and have a length with a specified range.

5. Verify the totalTransactionRevenue contains valid decimal or integer values.

6. Checking for the ratio only contains 0-1 values.

7. Checking for  the date, the year, month, day in a reasonable range. 





## Challenges 
The most challenges I faced in the project is to find the relationships between these tables, spend a lot of time in data quality assurance, 
and explore the business insight from the data

## Future Goals
To explore more detail in the data interactions, for example: Is there any other factors impact the vistors 
to buy the products. And I also would like to find out whether these data exploring can impact on business strategy.
