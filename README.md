# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
SQL final project for Lighthouse Labs Data Science Flex Feb 19, 2024 Cohort. 
The purpose of this project is to demonstrate my understanding of SQL, data queries, data cleaning, and data representation. 
This will include creating databases from raw csv files, cleaning the data, advanced queries, QAing results, generating ERDs, and learning standard programs.

## Process
### 1. Uploaded data set to PgAdmin and created ecommerce schema. 
Used template tables to fit data to data types quickly.
### 2. Familiarized myself with data 
Creating a draft ERD and started working on questions, holding off on the data cleaning step but making notes of anything that requires revisit.
### 3. Data cleaning
Using the duplicated or missing values found in the last step, reviewed that those were covered and reviewed for additional cleaning
### 4. Starting with Questions
Return to working with data set and questions to produce results givne the reviewed data.
### 5. QA Data
Identified potential risk areas and checked that queries for results are not effect by any risk factors
### 6. Generated ERD and Charts from Results
Took query results to Excel to generate charts for better visual

### Assumptions

* Sessions with transactions are orders that actually occured

## Results

* The ecommerce data showed that this service is primarily used by customers from the United States,  with the highest purchased and highest revenue items being Nest products and accesories.

<br>
	<img src="https://i.imgur.com/iGeVKd3.png" alt="Country revenue" width="300">
<br>


* We see the most session visits coming from organic searches but we get the most revenue and sales from customers from direct and referral channels

<br>
	<img src="https://i.imgur.com/Q4qwQLs.png" alt="Sessions from Channels" width="300">
	<img src="https://i.imgur.com/6QWjB8Y.png" alt="Revenue from Channels" width="300">
<br>


* However, we are also missing cities on a large portion of transactions. We can see just how much is being 
excluded in the following transaction count and revenue charts

<br>
	<img src="https://i.imgur.com/OS3zKkh.png" alt="Not available transactions" width="300">
	<img src="https://i.imgur.com/NAM2jrQ.png" alt="Not available revenue" width="300">
<br>

With these results, we know the demogrpahic of the customers who generate revenue. This is useful to target sales and advertisements in specific cities with items that are more likely to sell. It is also useful on the other end, to target untapped locations and markets.
However, we should also consider how reliable the results are considering the volume of excluded data. 

## Challenges 
* Unknown data source, did not know what the purpose of it was, what tthe elements meant, and how the tables were connected if at all.
* New to Markdown and GitHub so two additional items to learn along the way of the project.
* Many duplicated values and many missing values. Messy data set. 
* Lack of time to access mentors for advice due to current schedule and responsibil


## Future Goals
* Better presentation of data and documention. So become more familiar with Markdown features, and understand better GitHub documentation standards and common practices
* Approach problems with more open mind and be less hesitant to ask for assistance or experience
* Practice to be better with cleaning and preparing a data set. Be smart and confident with fixing data, even when modifying original tables.
* There is a lot more data that can be extracted, my review did not analyze the sentiment scores of each product and how they vary across different variables. With more time, I continue making sense of all the information still untouched
* I was only able to make note of a couple of the required cleaning steps for the analytics table. Another goal would be to clean up the data better, and see what additional information can be gathered from there