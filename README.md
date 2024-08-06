# Sales Data Analysis on Superstore

## Introduction
Superstore is a retail business located in the United States. They sell furniture, office supplies, and technology products with a vareity of subcategories. This data explores the sales, profit and geographical information of orders. 

#### Business Questions
* How many unique sales and customers has the superstore had?
* What percent of profit does each category and sub-category provide?
* Which region is the most profitable?
* Which city has the highest number of sales?
* Which segment has the most sales?
* Most popular shipping method? 

## Data Exploration
First, we'll explore the basic information of the data. 

```sql
--First 10 rows of data
SELECT * FROM superstore
LIMIT 10;
```

row_id|order_id|order_date|ship_date|ship_mode|customer_id|customer_name|segment|country|city|state|postal_code|region|product_id|category|sub_category|product_name|sales|quantity|discount|profit|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
1|CA-2016-152156|2016-11-08|2016-11-11|Second Class|CG-12520|Claire Gute|Consumer|United States|Henderson|Kentucky|42420|South|FUR-BO-10001798|Furniture|Bookcases|Bush Somerset Collection Bookcase|262|2|0|41.9136
2|CA-2016-152156|2016-11-08|2016-11-11|Second Class|CG-12520|Claire Gute|Consumer|United States|Henderson|Kentucky|42420|South|FUR-CH-10000454|Furniture|Chairs|Hon Deluxe Fabric Upholstered Stacking Chairs, Rounded Back|731.9|3|0|219.582
3|CA-2016-138688|2016-06-12|2016-06-16|Second Class|DV-13045|Darrin Van Huff|Corporate|United States|Los Angeles|California|90036|West|OFF-LA-10000240|Office Supplies|Labels|Self-Adhesive Address Labels for Typewriters by Universal|14.6|2|0|6.8714
4|US-2015-108966|2015-10-11|2015-10-18|Standard Class|SO-20335|Sean O Donnell|Consumer|United States|Fort Lauderdale|Florida|33311|South|FUR-TA-10000577|Furniture|Tables|Bretford CR4500 Series Slim Rectangular Table|957.6|5|0.45|-383.031
5|US-2015-108966|2015-10-11|2015-10-18|Standard Class|SO-20335|Sean O Donnell|Consumer|United States|Fort Lauderdale|Florida|33311|South|OFF-ST-10000760|Office Supplies|Storage|Eldon Fold  N Roll Cart System|22.4|2|0.2|2.5164
6|CA-2014-115812|2014-06-09|2014-06-14|Standard Class|BH-11710|Brosina Hoffman|Consumer|United States|Los Angeles|California|90032|West|FUR-FU-10001487|Furniture|Furnishings|Eldon Expressions Wood and Plastic Desk Accessories, Cherry Wood|48.9|7|0|14.1694
7|CA-2014-115812|2014-06-09|2014-06-14|Standard Class|BH-11710|Brosina Hoffman|Consumer|United States|Los Angeles|California|90032|West|OFF-AR-10002833|Office Supplies|Art|Newell 322|7.3|4|0|1.9656
8|CA-2014-115812|2014-06-09|2014-06-14|Standard Class|BH-11710|Brosina Hoffman|Consumer|United States|Los Angeles|California|90032|West|TEC-PH-10002275|Technology|Phones|Mitel 5320 IP Phone VoIP phone|907.2|6|0.2|90.7152
9|CA-2014-115812|2014-06-09|2014-06-14|Standard Class|BH-11710|Brosina Hoffman|Consumer|United States|Los Angeles|California|90032|West|OFF-BI-10003910|Office Supplies|Binders|DXL Angle-View Binders with Locking Rings by Samsill|18.5|3|0.2|5.7825
10|CA-2014-115812|2014-06-09|2014-06-14|Standard Class|BH-11710|Brosina Hoffman|Consumer|United States|Los Angeles|California|90032|West|OFF-AP-10002892|Office Supplies|Appliances|Belkin F5C206VTEL 6 Outlet Surge|114.9|5|0|34.47

```sql
--Bottom 10 rows of data
SELECT * FROM superstore
ORDER BY row_id desc
LIMIT 10;
```
row_id|order_id|order_date|ship_date|ship_mode|customer_id|customer_name|segment|country|city|state|postal_code|region|product_id|category|sub_category|product_name|sales|quantity|discount|profit|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
9994|CA-2017-119914|2017-05-04|2017-05-09|Second Class|CC-12220|Chris Cortes|Consumer|United States|Westminster|California|92683|West|OFF-AP-10002684|Office Supplies|Appliances|Acco 7-Outlet Masterpiece Power Center, Wihtout Fax/Phone Line Protection|243.2|2|0|72.948
9993|CA-2017-121258|2017-02-26|2017-03-03|Standard Class|DB-13060|Dave Brooks|Consumer|United States|Costa Mesa|California|92627|West|OFF-PA-10004041|Office Supplies|Paper|It s Hot Message Books with Stickers, 2 3/4  x 5 |29.6|4|0|13.32
9992|CA-2017-121258|2017-02-26|2017-03-03|Standard Class|DB-13060|Dave Brooks|Consumer|United States|Costa Mesa|California|92627|West|TEC-PH-10003645|Technology|Phones|Aastra 57i VoIP phone|258.6|2|0.2|19.3932
9991|CA-2017-121258|2017-02-26|2017-03-03|Standard Class|DB-13060|Dave Brooks|Consumer|United States|Costa Mesa|California|92627|West|FUR-FU-10000747|Furniture|Furnishings|Tenex B1-RE Series Chair Mats for Low Pile Carpets|92|2|0|15.6332
9990|CA-2014-110422|2014-01-21|2014-01-23|Second Class|TB-21400|Tom Boeckenhauer|Consumer|United States|Miami|Florida|33180|South|FUR-FU-10001889|Furniture|Furnishings|Ultra Door Pull Handle|25.2|3|0.2|4.1028
9989|CA-2017-163629|2017-11-17|2017-11-21|Standard Class|RA-19885|Ruben Ausman|Corporate|United States|Athens|Georgia|30605|South|TEC-PH-10004006|Technology|Phones|Panasonic KX - TS880B Telephone|206.1|5|0|55.647
9988|CA-2017-163629|2017-11-17|2017-11-21|Standard Class|RA-19885|Ruben Ausman|Corporate|United States|Athens|Georgia|30605|South|TEC-AC-10001539|Technology|Accessories|Logitech G430 Surround Sound Gaming Headset with Dolby 7.1 Technology|80|1|0|28.7964
9987|CA-2016-125794|2016-09-29|2016-10-03|Standard Class|ML-17410|Maris LaWare|Consumer|United States|Los Angeles|California|90008|West|TEC-AC-10003399|Technology|Accessories|Memorex Mini Travel Drive 64 GB USB 2.0 Flash Drive|36.2|1|0|15.2208
9986|CA-2015-100251|2015-05-17|2015-05-23|Standard Class|DV-13465|Dianna Vittorini|Consumer|United States|Long Beach|New York|11561|East|OFF-SU-10000898|Office Supplies|Supplies|Acme Hot Forged Carbon Steel Scissors with Nickel-Plated Handles, 3 7/8  Cut, 8 L|55.6|4|0|16.124
9985|CA-2015-100251|2015-05-17|2015-05-23|Standard Class|DV-13465|Dianna Vittorini|Consumer|United States|Long Beach|New York|11561|East|OFF-LA-10003766|Office Supplies|Labels|Self-Adhesive Removable Labels|31.5|10|0|15.12

There is a wide variety of data with differences of state, category, product, and other numerical values.
Each row represents an order which contains an item (and quanitity), the sales, discount, profit, mode of shipment, customer segment, and geographical infomation.

## Exploratory Data Analysis
### 1. How many unique sales has the superstore had?
```sql
SELECT 
	COUNT(DISTINCT row_id) AS unique_sales
FROM superstore;
```
|unique_sales|
|---|
|9993|

### 2. How many unique customers has the superstore had?
```sql
SELECT 
	COUNT(DISTINCT customer_id) AS unique_customers 
FROM superstore
```
|unique_customers|
|---|
|793|

### 3. How much profit does each category provide?
```sql
SELECT category,
	ROUND((SUM(profit) / NULLIF(SUM(sales) - SUM(discount), 0)) * 100) AS profit_percentage
FROM superstore
GROUP BY category
ORDER BY profit_percentage desc
```
|category|profit_percentage|
|---|---|
|OFfice Supplies| 17 | 
|Technology| 17 | 
|Furniture| 2 | 
### 4. How much profit does each sub-category provide?
```sql
SELECT sub_category,
	ROUND((SUM(profit) / NULLIF(SUM(sales) - SUM(discount), 0)) * 100) AS profit_percentage
FROM superstore
GROUP BY sub_category
ORDER BY profit_percentage desc
```
|sub_category|profit_percentage|
|---|---|
|Labels| 45 | 

### 5. Which region is the most profitable?
```sql
SELECT region,
ROUND(SUM(profit)) AS total_profit
FROM superstore
GROUP BY region
ORDER BY total_profit desc
```
|region|total_profit|
|---|---|
|West| 108418 | 
|East| 91535 | 
|South| 46749 | 
|Central|39706 |

## 6. Which city has the highest number of sales?
```sql
SELECT city,
ROUND(SUM(sales)) AS sales
FROM superstore
GROUP BY city
ORDER BY sales desc
LIMIT 10
```
|city|sales|
|---|---|
|New York City|256373|
|Los Angeles|175855|
|Seattle|119543|
|San Francisco|112674|
|Philadelphia|109079|
|Houston|64506|
|Chicago|48541|
|San Diego|47522|
|Jacksonville|44714|
|Springfield|43055|

## 7. Which city has the lowest number of sales?
## 8. Which segment has the most sales?
## 9. Most popular shipping method?
