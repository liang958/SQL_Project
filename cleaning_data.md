What issues will you address by cleaning the data?


1. Standardize the time 
   In all_sessions table, convert time column to timestamp
2. Standardize the country, city name
   In all_sessions table, in city column, set "not available in demo dataset" or '(not set)' to NULL
   In all_sessions table, in country column, set "(not set)" to NULL
3. Change Inappropriate data unit
   In all_sessions table, productprice unit should /1000000



Queries:
Below, provide the SQL queries you used to clean your data.
1.

SELECT TO_TIMESTAMP(time)
FROM all_sessions

Covert integer time value to the standard time format

2.
  
UPDATE all_sessions
SET city = NULL
WHERE city = 'not available in demo dataset' OR city = '(not set)'

UPDATE all_sessions
SET country = NULL
WHERE country = '(not set)'



3.

UPDATE all_sessions
SET "productPrice" = "productPrice"/1000000


