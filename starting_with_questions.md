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

SELECT a.country, a.city, AVG(p."orderedQuantity")  average
FROM all_sessions a 
JOIN products p on a."productSKU" = p."SKU" AND p."orderedQuantity" != 0
	AND country IS NOT NULL AND city IS NOT NULL 
GROUP BY country, city
ORDER BY country, city



Answer:

In Toronto, the average product quantity is 662,
IN Vancouver, the average is 395



**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:


SELECT a.country, a.city, "v2ProductCategory" category, SUM(p."orderedQuantity")  total_order
FROM all_sessions a 
JOIN products p on a."productSKU" = p."SKU" AND p."orderedQuantity" != 0
	AND country IS NOT NULL AND city IS NOT NULL
GROUP BY country, city, "v2ProductCategory"
ORDER BY country, city, "v2ProductCategory"


Answer:
There might have some patterns. Youtube is most popular category in worldwide.
But each city product category is different. In toronto, there are many product categories, 
most of orders are in drinkware, fun, office categories. But in Vancouver,
people  only buy products in four categories.





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries1:

WITH cal_total AS
 (SELECT a.country, a.city, "v2ProductName" productname , 
 SUM(p."orderedQuantity") total_quantity
 FROM all_sessions a 
 JOIN products p on a."productSKU" = p."SKU" AND p."orderedQuantity" != 0
 GROUP BY country, city, "v2ProductName"
 ORDER BY country, city, "v2ProductName"
) ,

cal_max AS
 (SELECT ca.country, ca.city, MAX(total_quantity) max_orderquantity 
 FROM cal_total ca 
 GROUP BY country, city
 ORDER BY country, city
)


SELECT ct.country, ct.city, ct.productname, cm.max_orderquantity
FROM cal_total ct
JOIN cal_max cm ON ct.country=cm.country 
	AND ct.city = cm.city
	AND ct.total_quantity = cm.max_orderquantity
ORDER BY ct.country, cm.city


SQL Queries2:


WITH cal_total AS
 (SELECT a.country, a.city, "v2ProductName" productname , 
 SUM(p."orderedQuantity") total_quantity
 FROM all_sessions a 
 JOIN products p on a."productSKU" = p."SKU" AND p."orderedQuantity" != 0
 GROUP BY country, city, "v2ProductName"
 ORDER BY country, city, "v2ProductName"
) ,

cal_min AS
 (SELECT ca.country, ca.city, MIN(total_quantity) min_orderquantity 
 FROM cal_total ca 
 GROUP BY country, city
 ORDER BY country, city
)


SELECT ct.country, ct.city, ct.productname, cm.min_orderquantity
FROM cal_total ct
JOIN cal_min cm ON ct.country=cm.country 
	AND ct.city = cm.city
	AND ct.total_quantity = cm.min_orderquantity
ORDER BY ct.country, cm.city


Answer:

Top selling product is different in each country and city. In toronto, top selling product 
is custom decals. In ottawa, the top selling product
is men's t-shirt, it is a little be werid, as the summer is not
hot and long there. But anyway, there is no woman's category in top selling 
category in Canada.



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







