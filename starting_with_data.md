Question 1: Is there any fullvisitorid when he visited the site, look at more than one product(find all duplicate records)?

SQL Queries:

SELECT "fullVisitorId",COUNT("fullVisitorId")
FROM all_sessions
GROUP BY "fullVisitorId"
HAVING COUNT("fullVisitorId") > 1


Answer: 
Yes, there are some individual fullvisitorids look at two or more products.



Question 2: find the total number of unique visitors (`fullVisitorID`)

SQL Queries:

SELECT SUM(DISTINCT("fullvisitorId"))
FROM analytics

Answer:
total number of unique visitor:5.4317770745469E+23 in analytics table

Question 3: find the total number of unique visitors by referring sites

SQL Queries:

SELECT COUNT(DISTINCT("fullVisitorId"))
FROM all_sessions
WHERE "channelGrouping" = 'Referral'

Answer:

the total number: 2419


Question 4: find each unique product viewed by each visitor

SQL Queries:

SELECT "productSKU", "fullVisitorId"
FROM all_sessions
GROUP BY "productSKU", "fullVisitorId"
ORDER BY "productSKU", "fullVisitorId"


Answer:
Remove 19 duplicate records with same visitor viewed the same product.


Question 5: compute the percentage of visitors to the site that actually makes a purchase

SQL Queries:

WITH total_num AS
	(SELECT COUNT(DISTINCT("fullVisitorId")) AS buyer_count
	FROM all_sessions
	WHERE transactions = 1
	)
	

SELECT 
	 100.0*(SELECT buyer_count FROM total_num)/COUNT(DISTINCT("fullVisitorId"))
FROM all_sessions


Answer:
0.56%

Question 6: Find the date in reasonable range


SQL Queries:

SELECT *
FROM all_sessions
WHERE date BETWEEN '2016-01-01' AND '2018-01-01'
      AND EXTRACT('month' FROM date) IN ('01', '02', '03', '04', '05', '06',
										 '07', '08', '09', '10', '11', '12')
	  AND EXTRACT('day' from date) IN ('01', '02', '03', '04', '05', '06',
		  '07', '08', '09', '10', '11', '12','13', '14', '15', '16', '17', '18',
		  '19', '20', '21', '22', '23', '24','25', '26', '27', '28', '29', '30', '31')

Ans: validate year, month and day


Question 7: Find the total number for ratio between 0 and 1

SQL Queries:

SELECT COUNT(ratio)
FROM sales_report
WHERE ratio BETWEEN 0 and 1

Ans: total number is 374


Question 8: find the total transaction revenue for each fullVisitorId 
SELECT "fullvisitorId",SUM(CASE WHEN "totalTransactionRevenue" NOT BETWEEN 0 AND 1.0E20 THEN NULL
			ELSE "totalTransactionRevenue" END) AS totalRevenue
FROM all_sessions
GROUP BY "fullVisitorId"


Question 9: Find the unique fields

SELECT "SKU",COUNT("SKU")
FROM products
Group by "SKU"
HAVING COUNT("SKU") > 2

Ans:
In products table "SKU" is unique key
"productSKU" in unique key in sales_report, sales_by_sku tables

