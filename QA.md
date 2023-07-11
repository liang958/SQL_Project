What are your risk areas? Identify and describe them.
1) Data validation: all_sessions table

1. Checking for the date format provided for all_sessions table are in a 
   valid date format YYYY-MM-DD

SELECT (CASE WHEN date IS NULL THEN NULL
		WHEN date IS NOT NULL
	    AND CAST(date AS text) NOT LIKE '[0-9][0-9][0-9][0-9]-[0-9][0-9]-[0-9][0-9]' THEN 1
	    ELSE 0
	    END) AS ve_date
FROM all_sessions

Ans:
All the date format is YYYY-MM-DD format


2. Checking for country, city column in all_sessions set (not set), 'not available in demo 
   data set' to NULL

SELECT COUNT(city)
FROM all_sessions
WHERE city = '(not set)' or city = 'not available in demo dataset' 

SELECT COUNT(country)
FROM all_sessions
WHERE country = '(not set)'  

Ans: output is 0, therefore all city = '(not set)' or city = 'not available in demo dataset'
and country have been updated to NLL


3. Verify the totalTransactionRevenue contains valid decimal or integer values

SELECT (CASE WHEN "totalTransactionRevenue" NOT BETWEEN 0 AND 1.0E20 THEN NULL
			ELSE "totalTransactionRevenue" END) AS totalTRevenue
FROM all_sessions

Ans:
totalTransactionRevenue column is not numeric, set to NLL


4. Checking for country and city column contain only alphabetic characters and have a length with 
   with a specified range

SELECT *
 FROM all_sessions
 WHERE LENGTH(country) BETWEEN 1 AND 50
       AND LENGTH(city) BETWEEN 1 AND 50
       AND country SIMILAR TO '[A-Za-z]{1,50}'
       AND city SIMILAR TO '[A-Za-z]{1,50}'

Ans: make sure country and city column contain only alphabetic characters and have a length with 
   with a specified range

5. validate the date

SELECT *
FROM all_sessions
WHERE date BETWEEN '2016-01-01' AND '2018-01-01'
      AND EXTRACT('month' FROM date) IN ('01', '02', '03', '04', '05', '06',
										 '07', '08', '09', '10', '11', '12')
	  AND EXTRACT('day' from date) IN ('01', '02', '03', '04', '05', '06',
		  '07', '08', '09', '10', '11', '12','13', '14', '15', '16', '17', '18',
		  '19', '20', '21', '22', '23', '24','25', '26', '27', '28', '29', '30', '31')

Ans: Validate the year, month, day in a valid range




6. Verify the ratio contains 0-1 values

SELECT (CASE WHEN ratio NOT BETWEEN 0 AND 1 THEN NULL
			ELSE ratio END) AS ratiocheck
FROM sales_report

Ans: ratio not between 0 and 1 set to NULL



7. Checking the unique fields

select "SKU",COUNT("SKU")
from products
Group by "SKU"
HAVING COUNT("SKU") > 2

Ans:
"SKU"/"productSKU" is unique key in products, sales_report, sales_by_sku tables


QA Process:
Describe your QA process and include the SQL queries used to execute it.
