## Question 1: Which product are out of stock and have a restocking lead time of more than 10 days

SQL Queries:
```SQL
SELECT 
	sku,
	name,
	ordered_quantity,
	stock_level,
	restocking_lead_time
FROM 
	products
WHERE 
	ordered_quantity > stock_level AND 
	restocking_lead_time > 10;
```

Answer: 
The following products have been over ordered and have a long restocking lead time.

|sku                           |name                  |ordered_quantity|stock_level|restocking_lead_time|
|:-----------------------------|:---------------------|:---------------|:----------|:-------------------|
|GGOENEBQ079099                | Protect Smoke + CO White Battery Alarm-USA|999             |325        |11                  |
|GGOEGKAA019299                |Switch Tone Color Crayon Pen|1163            |388        |12                  |
|GGOEGDHC015299                |23 oz Wide Mouth Sport Bottle|402             |142        |12                  |
|GGOEGBJC019999                |Collapsible Shopping Bag|1184            |117        |11                  |


## Question 2: Which visitors have viewed more than 4 products

SQL Queries:
```SQL
SELECT 
	full_visitor_id, 
	COUNT(DISTINCT product_sku) AS products_viewed
FROM 
	all_sessions
GROUP BY 
	full_visitor_id
HAVING 
	COUNT(DISTINCT product_sku) > 4;
```

Answer:

|full_visitor_id               |products_viewed       |
|:-----------------------------|:---------------------|
|0769560476351515188           |7                     |
|0824839726118485274           |8                     |
|1957458976293878100           |6                     |
|3608475193341679870           |10                    |
|5684903298881626743           |6                     |
|9801276214964695322           |7                     |


## Question 3: Which products have not appeared in a sales report

SQL Queries: 
```SQL
WITH products_with_reports_cte AS (
	SELECT 
		DISTINCT product_sku
	FROM 
		sales_report
)
SELECT 
	sku, 
	name
FROM 
	products 
WHERE 
	sku NOT IN (
		SELECT product_sku FROM products_with_reports_cte
	);
```

Answer:
(638 Rows)


## Question 4: Rank the top 10 countries that spend the most average time in a session

SQL Queries:
```SQL
WITH sessions_time_cte AS (
	SELECT 
		country, 
		DATE_TRUNC('SECOND', AVG(time_on_site)) AS avg_session_time
	FROM all_sessions
	GROUP BY 
		country
	ORDER BY 
		avg_session_time DESC
)
SELECT *, 
	RANK() OVER (ORDER BY avg_session_time DESC)
FROM 
	sessions_time_cte
WHERE 
	avg_session_time IS NOT NULL
LIMIT 10;
```

Answer:

|country                       |avg_session_time      |rank|
|:-----------------------------|:---------------------|:---|
|Peru                          |00:14:19              |1   |
|Nigeria                       |00:12:32              |2   |
|Tunisia                       |00:12:06              |3   |
|Slovenia                      |00:11:36              |4   |
|Kenya                         |00:09:32              |5   |
|El Salvador                   |00:09:28              |6   |
|Trinidad & Tobago             |00:09:21              |7   |
|Jersey                        |00:08:38              |8   |
|Réunion                       |00:07:45              |9   |
|Morocco                       |00:07:37              |10  |


## Question 5: Determine which channels are being used for the sessions

SQL Queries:
```SQL
SELECT 
	channel_grouping, 
	COUNT(DISTINCT visit_id) AS Visit_count
FROM 
	all_sessions
GROUP BY 
	channel_grouping
ORDER BY 
	Visit_count DESC;
```

Answer:

|channel_grouping              |visit_count           |
|:-----------------------------|:---------------------|
|Organic Search                |8348                  |
|Direct                        |2862                  |
|Referral                      |2488                  |
|Paid Search                   |488                   |
|Affiliates                    |247                   |
|Display                       |121                   |
|(Other)                       |5                     |
