### What are your risk areas? Identify and describe them.
* Check data was inserted into data base from csv correctly. IE no information lost from incorrectly assigned  data types. 
* Check Duplicate Entries are accounted for correctly in the queries.
* Ensure that WHERE filters are being implemented correctly and as expected.
* Missing/Null values
* Incorrect representation of data

### QA Process:
Describe your QA process and include the SQL queries used to execute it.

Review the data types in the tables and ensure they match the type of data being provided.
Review the null values and determined there wasn't enough information to complete any more information, missing information will not be accounted for
Review that there are no duplicates and that query pulls the expected number of entries and aggregate functions are correct
Document and fix any discovered faults in queries (No additional faults found)
Removal of less meaningful data such as the data with no city provided when reviewing data over cities.


### QA Code:

#### Question 1

Checking for duplicates 

```SQL

SELECT 
	full_visitor_id, 
	COUNT(*) 
FROM all_sessions
WHERE transactions IS NOT NULL
GROUP BY full_visitor_id
HAVING COUNT(full_visitor_id) > 1
-- List of full id with multiple purchases. 

SELECT * FROM all_sessions 
WHERE full_visitor_id = '3764227345226401562'

SELECT DISTINCT * FROM all_sessions WHERE transactions IS NOT NULL
-- 81 rows as expected. 
```

The full id '3764227345226401562' had multiple transactions but the products are different, confirming not duplicate

<br>
Less meaningful data
For the query on the cities, we can see that there is a large quantity under 'not available in demo dataset'. 

<br>
	<img src="https://i.imgur.com/NAM2jrQ.png" alt="Country revenue NA highlighted" width="300">
<br>

This is not useful for our analytics, but it is important to consider for the purpose and usability of our dataset. 
A query without the excluded data is below, which shows better the revenue distribution of the available cities

``` SQL
SELECT 
	city, 
	SUM(total_transaction_revenue)/1000000 AS revenue
FROM 
	all_sessions
WHERE 
	transactions IS NOT NULL
GROUP BY 
	city
ORDER BY 	
	revenue DESC;
```


<br>
	<img src="https://i.imgur.com/e6GuqVw.png" alt="Country revenue NA highlighted" width="300">
<br>






#### Self Question Q5
```SQL
SELECT 
	COUNT (DISTINCT full_visitor_id) AS FullCount, 
	COUNT(DISTINCT visit_id) AS IDCount
FROM all_sessions;
-- Shows more distinct full id


SELECT 
	full_visitor_id,
	COUNT (DISTINCT full_visitor_id) AS FullCount, 
	COUNT(DISTINCT visit_id) AS IDCount
FROM all_sessions
GROUP BY full_visitor_id
HAVING COUNT (DISTINCT full_visitor_id) != COUNT(DISTINCT visit_id);
-- Shows full visitor id with multiple visit id
```

The queries above determines that there are more distinct visit_id than full_visit_id, selecting visit_id will give cover all the results, so there are no fixes required.

For the revenue section, the coalesce function was added so that the order of the channels would display in order correctly. 

### If I had more time, I would:
* Communicate and get the insight of more experienced data scientists (use the request assistance to ask more questions). I let my 
day responsibilities push everything later into the night when mentor hours were no longer available. This would be a great resource to 
understand and gain more confidence with the dataset get some insight what results would be useful and on how others might approach it. 
* Clean up data better, normalize/remove duplicates in and across the tables. Sort the tables, split the all_sessions table into more manageable tables (star schema with transaction info at the center, products info (can attach products table), commerce info, visitor info)
* Present cleaner data, learn how to use markdown better. 
* Push more often with smaller changes so there is a record of versions in case something goes wrong along the way as opposed to saving everything on pc and then doing one large push at the end. Also understand better how the standards to setting up documentation.