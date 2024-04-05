# What issues will you address by cleaning the data?
With this data set, I did not have the time or resources to fully understand the data. I do not know if there is a reason or if any additional information can be gathered from the original data 
(ie if there is a reason or a specific source where data is missing, if there is a reason why the currency is x1000000, etc)
With that in mind, I opted not to make any changes to the tables and cleaned my queuries with modifications to my queries. 
Also note that only a couple of issues with the data was addressed and these considerations are by no means complete.

### Addressing Duplicate entries

Queries that use the DISTINCT KEYWORD on specific elements to exclude duplicate values

```SQL
SELECT DISTINCT * FROM analytics;
--1739308 of 4301122 rows, many duplicate rows in analytics table

SELECT DISTINCT(*) FROM all_sessions;
--15134 of 15134 rows
SELECT DISTINCT(full_visitor_id) FROM all_sessions;
--14223 of 15134 rows, couple repeated visits but no duplicate rows


--All unique visitors
SELECT DISTINCT(full_visitor_id) 
FROM (
	SELECT DISTINCT(full_visitor_id)
	FROM all_sessions
	--14223 rows
	
	UNION
	
	SELECT DISTINCT(full_visitor_id)
	FROM analytics
	--120018 rows
	)
ORDER BY full_visitor_id;
--130345 rows (out of 134241)


SELECT DISTINCT(sku) FROM products;
--1092 rows, no dupes in this table

SELECT DISTINCT (product_sku) FROM sales_by_sku;
--462 rows, no dupes in this table

SELECT DISTINCT (product_sku) FROM sales_report;
--454 rows, no dupes in this table */


```

### Addressing some missing data in all_sessions table

From the first query we van verify the following ecommerce action steps corresponds to the ecommerce action option as shown below: 
	1. Billing and Shipping
	2. Payment
	3. Review
	
```SQL
--Verify correlation
SELECT 
	ecommerce_action_step, 
	ecommerce_action_option
FROM 
	all_sessions
WHERE 	
	ecommerce_action_option IS NOT NULL

--Query to Fill Data
SELECT 
	ecommerce_action_step, 
	COALESCE(ecommerce_action_option,
		CASE 
			WHEN ecommerce_action_step = 1 THEN 'Billing and Shipping'
			WHEN ecommerce_action_step = 2 THEN 'Payment'
			WHEN ecommerce_action_step = 3 THEN 'Review'
		END) AS Filled_eao
FROM all_sessions
```

There also seems to be some correlation between ecommers action type and page path level 1 but there are some inconsistencies.

### Addressing data that required modifications
The revenue and currency columns are all multiplied by 1000000. So each time revenue is pulled we need to divide by 1000000.

```SQL
SELECT total_transaction_revenue/1000000 
FROM all_sessions 
WHERE transactions IS NOT NULL
```

Time in all_sessions table is in a wide range of integers, cannot identify appropriate adjustment or type to convert to proper form, left as integers until further understanding.
