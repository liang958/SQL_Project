Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

SELECT country, city, "totalTransactionRevenue"
FROM all_sessions
WHERE country is NOT NULL AND city is NOT NULL
	  AND "totalTransactionRevenue" = 
	  (SELECT MAX("totalTransactionRevenue") 
	   FROM all_sessions 
	   WHERE country is NOT NULL AND city is NOT NULL)

Answer:
In United States, Atlanta



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

SELECT a.country, a.city, AVG(p."orderedQuantity") 
FROM all_sessions a 
JOIN products p on a."productSKU" = p."SKU" AND p."orderedQuantity" != 0
GROUP BY country, city
ORDER BY country, city



Answer:

In Toronto, the average product quantity is 661.5,
IN Vancouver, the average is 395



**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:


SELECT a.country, a.city, "v2ProductCategory", SUM(p."orderedQuantity") 
FROM all_sessions a 
JOIN products p on a."productSKU" = p."SKU" AND p."orderedQuantity" != 0
GROUP BY country, city, "v2ProductCategory"
ORDER BY country, city, "v2ProductCategory"



Answer:
There might be have some patterns. For example, in Canada, every city
product category is different. In toronto, there are many product categories, 
most of orders are in drinkware, fun, office categories. But in Vancouver,
people don't buy too much products, categories only have four.





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries1:

WITH cal_total AS
 (SELECT a.country, a.city, "v2ProductCategory" productcategory , 
 SUM(p."orderedQuantity") total_quantity
 FROM all_sessions a 
 JOIN products p on a."productSKU" = p."SKU" AND p."orderedQuantity" != 0
 GROUP BY country, city, "v2ProductCategory"
 ORDER BY country, city, "v2ProductCategory"
) ,

cal_max AS
 (SELECT ca.country, ca.city, MAX(total_quantity) max_orderquantity 
 FROM cal_total ca 
 GROUP BY country, city
 ORDER BY country, city
)


SELECT ct.country, ct.city, ct.productcategory, cm.max_orderquantity
FROM cal_total ct
JOIN cal_max cm ON ct.country=cm.country 
	AND ct.city = cm.city
	AND ct.total_quantity = cm.max_orderquantity
ORDER BY ct.country, cm.city


SQL Queries2:


WITH cal_total AS
 (SELECT a.country, a.city, "v2ProductCategory" productcategory , 
 SUM(p."orderedQuantity") total_quantity
 FROM all_sessions a 
 JOIN products p on a."productSKU" = p."SKU" AND p."orderedQuantity" != 0
 GROUP BY country, city, "v2ProductCategory"
 ORDER BY country, city, "v2ProductCategory"
) ,

cal_min AS
 (SELECT ca.country, ca.city, MIN(total_quantity) min_orderquantity 
 FROM cal_total ca 
 GROUP BY country, city
 ORDER BY country, city
)


SELECT ct.country, ct.city, ct.productcategory, cm.min_orderquantity
FROM cal_total ct
JOIN cal_min cm ON ct.country=cm.country 
	AND ct.city = cm.city
	AND ct.total_quantity = cm.min_orderquantity
ORDER BY ct.country, cm.city


Answer:
There might be have some patterns. For example, in Canada, every city
top selling product is different. In toronto, top selling product category
is office, it might be make sense. In ottawa, the top selling product
category is men's t-shirt, it is a little be werid, as the summer is not
hot and long there. But anyway, there is no woman's category in top selling 
category in Canada. Overall we still can find that YouTube is most popular
top selling product category in Canada and Worldwide.
In SQL Querlies 2, we find that T-shirt is minum product order in many cities in Canada .




**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

WITH ext_revenue AS
	(SELECT *
	 FROM analytics
	 WHERE revenue > 0)
	 
SELECT country, city, SUM(revenue) as total_revenue
FROM all_sessions al
JOIN ext_revenue er ON al."fullVisitorId" = er."fullvisitorId"
		AND al."visitId" = er."visitId"
GROUP BY country, city
ORDER BY total_revenue DESC

Answer:
There are not many revenue records in the tables.However, Almost all of the revenue
records are in the United States. After we join the table, we can find that 
sunnyvale, seattle, san francisco, chicago, mountain view these cities are the 
top 5 cities generated the highest revenue.







