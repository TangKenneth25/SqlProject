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




### QA Code:

#### Question 1
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
-- Almost looked like there was a duplicate but the products are different

SELECT DISTINCT * FROM all_sessions WHERE transactions IS NOT NULL
-- 81 rows as expected. 
```


#### Question 3
```SQL
SELECT DISTINCT country, v2_Product_Category FROM all_sessions
WHERE transactions IS NOT NULL
--36 of 36 rows, no duplicates, no nulls. 

```




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


### If I had more time, I would:
* Communicate and get the insight of more experienced data scientists (use the request assistance to ask more questions). I let my 
day responsibilities push everything later into the night when mentor hours were no longer available. This would be a great resource to 
understand and gain more confidence with the dataset get some insight what results would be useful and on how others might approach it. 
* Clean up data better, normalize/remove duplicates in and across the tables. Sort the tables, split the all_sessions table into more manageable tables (star schema with transaction info at the center, products info (can attach products table), commerce info, visitor info)
* Present cleaner data, learn how to use markdown better. 
* Push more often with smaller changes so there is a record of versions in case something goes wrong along the way as opposed to saving everything on pc and then doing one large push at the end. Also understand better how the standards to setting up documentation.