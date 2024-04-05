Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
Country Transaction Sum
``` SQL
SELECT	
	country, 
	SUM(total_transaction_revenue)/1000000 AS revenue
FROM 
	all_sessions 
WHERE 
	transactions IS NOT NULL
GROUP BY 
	country
ORDER BY 
	revenue DESC;
```

City Transaction Sum
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

Answer: 
	
 United States is the country with the highest revenue. San Francisco is the city with the highest revenue (however, a large portion of the revenue is not specified to a city, so our city conclusion may be inaccurate.)


|country                       |revenue               |
|:-----------------------------|:---------------------|
|United States                 |13154.17              |
|Israel                        |602                   |
|Australia                     |358                   |
|Canada                        |150.15                |
|Switzerland                   |16.99                 |


<br>

|city                          |revenue               |
|:-----------------------------|:---------------------|
|not available in demo dataset |6092.56               |
|San Francisco                 |1564.32               |
|Sunnyvale                     |992.23                |
|Atlanta                       |854.44                |
|Palo Alto                     |608                   |
|Tel Aviv-Yafo                 |602                   |
|New York                      |598.35                |
|Mountain View                 |483.36                |
|Los Angeles                   |479.48                |
|Chicago                       |449.52                |
|Seattle                       |358                   |
|Sydney                        |358                   |
|San Jose                      |262.38                |
|Austin                        |157.78                |
|Nashville                     |157                   |
|San Bruno                     |103.77                |
|Toronto                       |82.16                 |
|Houston                       |38.98                 |
|Columbus                      |21.99                 |
|Zurich                        |16.99                 |


**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
```SQL
SELECT 
	country, 
	ROUND(AVG(product_quantity),2) AS avg_products
FROM 
	all_sessions
WHERE 
	product_quantity IS NOT NULL
GROUP BY 	
	COUNTRY;
```

```SQL
SELECT 
	city, 
	ROUND(AVG(product_quantity),2) AS avg_products
FROM 
	all_sessions
WHERE 
	product_quantity IS NOT NULL
GROUP BY 
	city;
```

Answer:
The average of products for each order shown in tables below. Note that for some of these quantities, there were no transactions made.

|country                       |avg_products          |
|:-----------------------------|:---------------------|
|Argentina                     |1.00                  |
|Canada                        |1.00                  |
|Colombia                      |1.00                  |
|Finland                       |1.00                  |
|France                        |1.00                  |
|India                         |1.00                  |
|Ireland                       |1.00                  |
|Mexico                        |1.00                  |
|Spain                         |10.00                 |
|United States                 |4.02                  |

<br>

|city                          |avg_products          |
|:-----------------------------|:---------------------|
|(not set)                     |1.00                  |
|Ann Arbor                     |1.00                  |
|Atlanta                       |4.00                  |
|Bengaluru                     |1.00                  |
|Chicago                       |1.00                  |
|Columbus                      |1.00                  |
|Dallas                        |1.00                  |
|Detroit                       |1.00                  |
|Dublin                        |1.00                  |
|Houston                       |2.00                  |
|Los Angeles                   |1.00                  |
|Madrid                        |10.00                 |
|Mountain View                 |1.00                  |
|New York                      |1.17                  |
|not available in demo dataset |6.75                  |
|Palo Alto                     |1.00                  |
|Salem                         |8.00                  |
|San Francisco                 |1.00                  |
|San Jose                      |1.00                  |
|Seattle                       |1.00                  |
|Sunnyvale                     |1.00                  |




**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
Country Transactions Sum
```SQL
SELECT 
	country, 
	v2_Product_Category, 
	SUM(total_transaction_revenue)/1000000 AS totalspent
FROM 
	all_sessions
WHERE 
	transactions IS NOT NULL
GROUP BY 1, 2
ORDER BY 
	totalspent DESC;
```

City Transaction Sum
```SQL
SELECT 
	city, 
	v2_Product_Category, 
	SUM(total_transaction_revenue)/1000000 AS totalspent
FROM 
	all_sessions
WHERE 
	transactions IS NOT NULL AND city != 'not available in demo dataset'
GROUP BY 1, 2
ORDER BY 
	totalspent DESC;
```

Country Transaction Count
```SQL
SELECT 
	country, 
	v2_Product_Category, 
	COUNT(*) AS Count
FROM 
	all_sessions
WHERE 
	transactions IS NOT NULL
GROUP BY 1, 2
ORDER BY 
	Count DESC;
```

City Transaction Count
```SQL
SELECT 
	city, 
	v2_Product_Category, 
	COUNT(*) AS Count
FROM 
	all_sessions
WHERE 
	transactions IS NOT NULL AND city != 'not available in demo dataset'
GROUP BY 1, 2
ORDER BY 
	Count DESC;
```


Answer:
Nest products appear to be the most spent on item for most countries and the most spent on category overall. <br>
Nest products also seem to occur the most at the top of spending amounts, showing up 13 times in the top 20 spending categories

|country                        |v2_product_category    |totalspent |
|:------------------------------|:----------------------|:----------|
|United States                 |Home/Nest/Nest-USA/   |3753.09   |
|United States                 |Bags                  |1757.96   |
|United States                 |Nest-USA              |1685      |
|United States                 |Electronics           |1175.47   |
|United States                 |Home/Office/Notebooks & Journals/|849.7     |
|United States                 |Home/Accessories/Pet/ |747       |
|United States                 |Housewares            |649.24    |
|Israel                        |Home/Nest/Nest-USA/   |602       |
|Australia                     |Nest-USA              |358       |
|United States                 |Apparel               |269.27    |
|United States                 |Home/Apparel/Men's/Men's-T-Shirts/|221.51    |
|United States                 |${escCatTitle}        |213.97    |
|United States                 |Lifestyle             |183.94    |
|United States                 |Home/Apparel/Women's/Women's-T-Shirts/|178.88    |
|United States                 |Home/Shop by Brand/Android/|157       |
|United States                 |Home/Shop by Brand/Google/|149.49    |
|United States                 |Home/Accessories/Drinkware/|139.42    |
|United States                 |Home/Bags/            |137.21    |
|United States                 |Home/Apparel/Women's/ |116.48    |
|United States                 |Home/Drinkware/Water Bottles and Tumblers/|108.14    |
|United States                 |Home/Apparel/Kid's/Kid's-Infant/|107.97    |
|United States                 |Home/Apparel/Men's/   |103.77    |
|United States                 |Home/Drinkware/       |102.95    |
|Canada                        |Apparel               |82.16     |
|United States                 |Home/Apparel/Men's/Men's-Performance Wear/|81.96     |
|United States                 |Home/Apparel/Women's/Women's-Outerwear/|71.19     |
|Canada                        |Home/Apparel/Men's/Men's-Outerwear/|67.99     |
|United States                 |Home/Shop by Brand/   |57.99     |
|United States                 |Home/Apparel/Men's/Men's-Outerwear/|23.99     |
|United States                 |(not set)             |21.99     |
|United States                 |Home/Accessories/Fun/ |19.69     |
|United States                 |Home/Office/Writing Instruments/|19.58     |
|United States                 |Waze                  |18.94     |
|United States                 |Home/Apparel/         |17.99     |
|Switzerland                   |Home/Apparel/Men's/Men's-T-Shirts/|16.99     |
|United States                 |Home/Electronics/Electronics Accessories/|13.39     |


<br>

|city                          |v2_product_category   |totalspent|
|:-----------------------------|:---------------------|:---------|
|Atlanta                       |Bags                  |742.48    |
|Sunnyvale                     |Housewares            |649.24    |
|San Francisco                 |Home/Nest/Nest-USA/   |620.09    |
|Tel Aviv-Yafo                 |Home/Nest/Nest-USA/   |602       |
|Palo Alto                     |Home/Nest/Nest-USA/   |457       |
|Los Angeles                   |Home/Nest/Nest-USA/   |363       |
|Seattle                       |Home/Nest/Nest-USA/   |358       |
|Sydney                        |Nest-USA              |358       |
|Chicago                       |Nest-USA              |306       |
|San Francisco                 |Nest-USA              |202       |
|Sunnyvale                     |Nest-USA              |200       |
|Nashville                     |Nest-USA              |157       |
|San Francisco                 |Home/Shop by Brand/Android/|157       |
|Mountain View                 |Home/Nest/Nest-USA/   |156       |
|Mountain View                 |Nest-USA              |154       |
|San Jose                      |Home/Nest/Nest-USA/   |154       |
|New York                      |${escCatTitle}        |152       |
|Palo Alto                     |Nest-USA              |151       |
|San Francisco                 |Home/Accessories/Drinkware/|139.42    |
|New York                      |Home/Nest/Nest-USA/   |127       |
|San Francisco                 |Home/Bags/            |124       |
|Chicago                       |Lifestyle             |123.94    |
|Austin                        |Home/Shop by Brand/Google/|122       |
|Sunnyvale                     |Home/Nest/Nest-USA/   |120       |
|Los Angeles                   |Home/Apparel/Women's/ |116.48    |
|San Francisco                 |Home/Apparel/Women's/Women's-T-Shirts/|115.52    |
|Atlanta                       |Home/Apparel/Men's/Men's-T-Shirts/|111.96    |
|San Jose                      |Apparel               |108.38    |
|San Francisco                 |Home/Drinkware/Water Bottles and Tumblers/|108.14    |
|San Bruno                     |Home/Apparel/Men's/   |103.77    |
|Toronto                       |Apparel               |82.16     |
|New York                      |Home/Apparel/Men's/Men's-Performance Wear/|81.96     |
|Mountain View                 |Home/Apparel/Women's/Women's-Outerwear/|71.19     |
|New York                      |Home/Apparel/Men's/Men's-Outerwear/|67.99     |
|San Francisco                 |${escCatTitle}        |61.97     |
|New York                      |Home/Shop by Brand/   |57.99     |
|New York                      |Apparel               |51.33     |
|Mountain View                 |Apparel               |43.81     |
|Houston                       |Home/Drinkware/       |38.98     |
|Mountain View                 |Home/Apparel/Kid's/Kid's-Infant/|35.99     |
|Austin                        |Apparel               |35.78     |
|New York                      |Home/Apparel/Kid's/Kid's-Infant/|32.99     |
|San Francisco                 |Home/Apparel/Men's/Men's-Outerwear/|23.99     |
|Sunnyvale                     |Home/Apparel/Men's/Men's-T-Shirts/|22.99     |
|Columbus                      |(not set)             |21.99     |
|New York                      |Home/Apparel/Men's/Men's-T-Shirts/|19.59     |
|Chicago                       |Home/Office/Writing Instruments/|19.58     |
|Zurich                        |Home/Apparel/Men's/Men's-T-Shirts/|16.99     |
|Mountain View                 |Home/Electronics/Electronics Accessories/|13.39     |
|San Francisco                 |Home/Accessories/Fun/ |12.19     |
|Mountain View                 |Waze                  |8.98      |
|New York                      |Home/Accessories/Fun/ |7.5       |




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
```SQL
SELECT 
	country, 
	v2_product_name, 
	SUM(total_transaction_revenue)/1000000 AS totalspent
FROM 
	all_sessions
WHERE 
	transactions IS NOT NULL
GROUP BY 1, 2
ORDER BY 
	totalspent DESC;
```

```SQL
SELECT 
	city, v2_product_name, 
	SUM(total_transaction_revenue)/1000000 AS totalspent
FROM 
	all_sessions
WHERE 
	transactions IS NOT NULL
GROUP BY 1, 2
ORDER BY 
	totalspent DESC;
```

Answer:
Similar to results from the top categories, we can see that Nest products are still at the top. Both the sum of transactions and sum of revenue were 
considered for both categories and product, since the higher cost of Nest products could skew the results. Only showed one of each and the results are similar. 

|country                       |v2_product_name       |n_ordered|
|:-----------------------------|:---------------------|:--------|
|United States                 |Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel|7        |
|United States                 |Nest® Cam Outdoor Security Camera - USA|5        |
|United States                 |Nest® Cam Indoor Security Camera - USA|3        |
|United States                 |Nest® Learning Thermostat 3rd Gen-USA|3        |
|United States                 |Google Sunglasses     |2        |
|United States                 |Google Men's 100% Cotton Short Sleeve Hero Tee Navy|2        |
|United States                 |Nest® Protect Smoke + CO White Wired Alarm-USA|2        |
|United States                 |Nest® Protect Smoke + CO White Battery Alarm-USA|2        |
|United States                 |Reusable Shopping Bag |2        |
|United States                 |Google Men's 100% Cotton Short Sleeve Hero Tee Black|2        |
|United States                 |Nest® Learning Thermostat 3rd Gen-USA - White|2        |
|United States                 |Android Men's Vintage Henley|1        |
|United States                 |Android Rise 14 oz Mug|1        |
|United States                 |Android Women's Fleece Hoodie|1        |
|United States                 |Android Women's Short Sleeve Tri-blend Badge Tee Light Grey|1        |
|United States                 |Compact Bluetooth Speaker|1        |
|United States                 |Crunch Noise Dog Toy  |1        |
|United States                 |Google Bongo Cupholder Bluetooth Speaker|1        |
|United States                 |Google Infant Zip Hood Pink|1        |
|United States                 |Google Laptop and Cell Phone Stickers|1        |
|United States                 |Google Men's  Zip Hoodie|1        |
|United States                 |Google Men's 100% Cotton Short Sleeve Hero Tee White|1        |
|United States                 |Google Men's Bike Short Sleeve Tee Charcoal|1        |
|United States                 |Google Men's Short Sleeve Badge Tee Charcoal|1        |
|United States                 |Google Men's Short Sleeve Hero Tee Heather|1        |
|United States                 |Google Men's Short Sleeve Performance Badge Tee Pewter|1        |
|United States                 |Google Men's Vintage Badge Tee Sage|1        |
|United States                 |Google Men's Vintage Badge Tee White|1        |
|United States                 |Google Men's Vintage Tank|1        |
|United States                 |Google Onesie Red/Graphite|1        |
|United States                 |Google Tri-blend Hoodie Grey|1        |
|United States                 |Google Women's 3/4 Sleeve Baseball Raglan Heather/Black|1        |
|United States                 |Google Women's Scoop Neck Tee White|1        |
|United States                 |Google Women's Short Sleeve Hero Tee Heather|1        |
|United States                 |Google Women's Short Sleeve Hero Tee White|1        |
|United States                 |Google Zipper-front Sports Bag|1        |
|United States                 |Grip Kit Cable Organizer|1        |
|United States                 |Leatherette Journal   |1        |
|United States                 |Nest® Protect Smoke + CO Black Battery Alarm-USA|1        |
|United States                 |Nest® Protect Smoke + CO Black Wired Alarm-USA|1        |
|United States                 |Rubber Grip Ballpoint Pen 4 Pack|1        |
|United States                 |SPF-15 Slim & Slender Lip Balm|1        |
|United States                 |Waterproof Backpack   |1        |
|United States                 |Waze Dress Socks      |1        |
|United States                 |Waze Mobile Phone Vent Mount|1        |
|United States                 |Waze Mood Original Window Decal|1        |
|United States                 |Windup Android        |1        |
|United States                 |YouTube Luggage Tag   |1        |
|Australia                     |Nest® Cam Indoor Security Camera - USA|1        |
|United States                 |YouTube Men's Short Sleeve Hero Tee Charcoal|1        |
|Canada                        |Google Men's  Zip Hoodie|1        |
|Canada                        |Google Men's 3/4 Sleeve Raglan Henley Grey|1        |
|Israel                        |Nest® Protect Smoke + CO Black Wired Alarm-USA|1        |
|Switzerland                   |YouTube Men's 3/4 Sleeve Henley|1        |
|United States                 |20 oz Stainless Steel Insulated Tumbler|1        |
|United States                 |22 oz YouTube Bottle Infuser|1        |
|United States                 |26 oz Double Wall Insulated Bottle|1        |
|United States                 |Android 17oz Stainless Steel Sport Bottle|1        |
|United States                 |Android Infant Short Sleeve Tee Pewter|1        |
|United States                 |Android Men's Long Sleeve Badge Crew Tee Heather|1        |


<br>

|city                          |v2_product_name       |n_ordered|
|:-----------------------------|:---------------------|:--------|
|not available in demo dataset |Nest® Protect Smoke + CO White Wired Alarm-USA|2        |
|not available in demo dataset |Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel|2        |
|Austin                        |Google Men's 100% Cotton Short Sleeve Hero Tee Black|1        |
|Austin                        |Google Men's 100% Cotton Short Sleeve Hero Tee Navy|1        |
|Chicago                       |Google Sunglasses     |1        |
|Chicago                       |Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel|1        |
|Chicago                       |Rubber Grip Ballpoint Pen 4 Pack|1        |
|Columbus                      |Google Men's Short Sleeve Badge Tee Charcoal|1        |
|Houston                       |26 oz Double Wall Insulated Bottle|1        |
|Los Angeles                   |Google Women's Short Sleeve Hero Tee White|1        |
|Los Angeles                   |Nest® Cam Outdoor Security Camera - USA|1        |
|Mountain View                 |Android Infant Short Sleeve Tee Pewter|1        |
|Mountain View                 |Android Women's Fleece Hoodie|1        |
|Mountain View                 |Google Men's Bike Short Sleeve Tee Charcoal|1        |
|Mountain View                 |Google Men's Vintage Badge Tee Sage|1        |
|Mountain View                 |Grip Kit Cable Organizer|1        |
|Mountain View                 |Nest® Learning Thermostat 3rd Gen-USA|1        |
|Mountain View                 |Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel|1        |
|Mountain View                 |Waze Mobile Phone Vent Mount|1        |
|Nashville                     |Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel|1        |
|New York                      |Google Laptop and Cell Phone Stickers|1        |
|New York                      |Google Men's  Zip Hoodie|1        |
|New York                      |Google Men's 100% Cotton Short Sleeve Hero Tee White|1        |
|New York                      |Google Men's Short Sleeve Performance Badge Tee Pewter|1        |
|New York                      |Google Men's Vintage Tank|1        |
|New York                      |Google Onesie Red/Graphite|1        |
|New York                      |Nest® Cam Outdoor Security Camera - USA|1        |
|New York                      |Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel|1        |
|New York                      |YouTube Luggage Tag   |1        |
|not available in demo dataset |22 oz YouTube Bottle Infuser|1        |
|not available in demo dataset |Android Men's Long Sleeve Badge Crew Tee Heather|1        |
|not available in demo dataset |Android Women's Short Sleeve Tri-blend Badge Tee Light Grey|1        |
|not available in demo dataset |Compact Bluetooth Speaker|1        |
|not available in demo dataset |Crunch Noise Dog Toy  |1        |
|not available in demo dataset |Google Bongo Cupholder Bluetooth Speaker|1        |
|not available in demo dataset |Google Infant Zip Hood Pink|1        |
|not available in demo dataset |Google Men's 100% Cotton Short Sleeve Hero Tee Black|1        |
|not available in demo dataset |Google Men's 100% Cotton Short Sleeve Hero Tee Navy|1        |
|not available in demo dataset |Google Sunglasses     |1        |
|not available in demo dataset |Google Women's Short Sleeve Hero Tee Heather|1        |
|not available in demo dataset |Google Zipper-front Sports Bag|1        |
|not available in demo dataset |Leatherette Journal   |1        |
|not available in demo dataset |Nest® Cam Indoor Security Camera - USA|1        |
|not available in demo dataset |Nest® Learning Thermostat 3rd Gen-USA|1        |
|not available in demo dataset |Nest® Learning Thermostat 3rd Gen-USA - White|1        |
|not available in demo dataset |Nest® Protect Smoke + CO White Battery Alarm-USA|1        |
|not available in demo dataset |Reusable Shopping Bag |1        |
|not available in demo dataset |Waze Dress Socks      |1        |
|not available in demo dataset |Waze Mood Original Window Decal|1        |
|not available in demo dataset |YouTube Men's Short Sleeve Hero Tee Charcoal|1        |
|Palo Alto                     |Nest® Cam Outdoor Security Camera - USA|1        |
|Palo Alto                     |Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel|1        |
|Palo Alto                     |Nest® Learning Thermostat 3rd Gen-USA - White|1        |
|San Bruno                     |Google Men's Vintage Badge Tee White|1        |
|San Francisco                 |20 oz Stainless Steel Insulated Tumbler|1        |
|San Francisco                 |Android 17oz Stainless Steel Sport Bottle|1        |
|San Francisco                 |Android Rise 14 oz Mug|1        |
|San Francisco                 |Google Tri-blend Hoodie Grey|1        |
|San Francisco                 |Google Women's 3/4 Sleeve Baseball Raglan Heather/Black|1        |
|San Francisco                 |Google Women's Scoop Neck Tee White|1        |
|San Francisco                 |Nest® Cam Outdoor Security Camera - USA|1        |
|San Francisco                 |Nest® Learning Thermostat 3rd Gen-USA|1        |
|San Francisco                 |Nest® Protect Smoke + CO Black Battery Alarm-USA|1        |
|San Francisco                 |Nest® Protect Smoke + CO White Battery Alarm-USA|1        |
|San Francisco                 |Waterproof Backpack   |1        |
|San Francisco                 |Windup Android        |1        |
|San Jose                      |Google Men's  Zip Hoodie|1        |
|San Jose                      |Nest® Cam Outdoor Security Camera - USA|1        |
|Seattle                       |Nest® Cam Indoor Security Camera - USA|1        |
|Sunnyvale                     |Android Men's Vintage Henley|1        |
|Sunnyvale                     |Nest® Cam Indoor Security Camera - USA|1        |
|Sunnyvale                     |Nest® Protect Smoke + CO Black Wired Alarm-USA|1        |
|Sunnyvale                     |SPF-15 Slim & Slender Lip Balm|1        |
|Sydney                        |Nest® Cam Indoor Security Camera - USA|1        |
|Tel Aviv-Yafo                 |Nest® Protect Smoke + CO Black Wired Alarm-USA|1        |
|Toronto                       |Google Men's 3/4 Sleeve Raglan Henley Grey|1        |
|Atlanta                       |Google Men's Short Sleeve Hero Tee Heather|1        |
|Zurich                        |YouTube Men's 3/4 Sleeve Henley|1        |
|Atlanta                       |Reusable Shopping Bag |1        |


**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

```SQL
SELECT 
	country,
	city,
	ROUND((SUM(total_transaction_revenue / 1000000 * sentiment_score * sentiment_magnitude)::DECIMAL),2) AS Impact
FROM 
	all_sessions JOIN 
	products ON product_sku = sku
WHERE 
	transactions IS NOT NULL
GROUP BY 
	country, city;
```


Answer:
Taking the impact of revenue spent as the product of the revenue, sentiment score, and sentiment magnitude for each product, we 
can see that united states has had the most positive impact overall, with only canada having some negative impact. 

|country                       |city                  |impact|
|:-----------------------------|:---------------------|:-----|
|United States                 |not available in demo dataset|929.24|
|United States                 |San Francisco         |335.06|
|United States                 |Palo Alto             |228.45|
|United States                 |Los Angeles           |224.79|
|United States                 |New York              |205.00|
|United States                 |San Jose              |168.27|
|United States                 |Sunnyvale             |102.20|
|United States                 |Atlanta               |78.37 |
|United States                 |Chicago               |56.40 |
|United States                 |Mountain View         |55.84 |
|United States                 |Austin                |41.28 |
|United States                 |Nashville             |23.55 |
|United States                 |Seattle               |21.48 |
|Australia                     |Sydney                |21.48 |
|United States                 |Columbus              |16.93 |
|United States                 |Houston               |15.59 |
|United States                 |San Bruno             |5.19  |
|Switzerland                   |Zurich                |1.02  |
|Canada                        |New York              |-2.72 |




