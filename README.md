# E-COMMERCE-RETAIL-DATA-ANALYSIS_SQL

This GitHub repository contains SQL queries and scripts for performing data analysis on e-commerce retail datasets. SQL is utilized to extract, transform, and analyze data stored in relational databases, providing insights into various aspects. This project enhances the metrics related to customer behavior, product performance, sales, and more.
    
![eCommerce-Cartoon](https://github.com/SLJyothi/E-COMMERCE-RETAIL-DATA-ANALYSIS/assets/164232591/d66f7760-f646-4f1e-addd-6c81a6ca4b76)

# Databases Used:
 # Customer 
 Houses a detailed customer database schema with fields including date of birth (DOB), customer ID, gender, and city. Provides SQL queries and scripts for comprehensive customer insights, segmentation, and 
 analytics to drive data-driven business decisions.

 # Transactions
 Dedicated to fetching and analyzing transactional data from a comprehensive table. The table encompasses essential fields like transaction ID, date, mode, store type, product sub-code, rate, taxes, total amount, 
 and return amount. This repository offers SQL queries and scripts tailored for extracting, processing, and interpreting transaction data. It aims to provide valuable insights into customer purchasing behavior, 
 product performance, and financial metrics, enabling businesses to make informed decisions and optimize sales strategies."

 # Prod_cat_info
 Retrieving and analyzing data from a product category table. The table includes key information such as product category, sub-category, and product sub-code. This repository offers SQL queries and scripts 
 designed to efficiently fetch and process this data. It aims to provide businesses with insights into product preferences, category trends, and customer purchasing behavior. By leveraging this repository, 
 organizations can better understand their product landscape and tailor their marketing and inventory strategies to meet customer demands effectively.
 
# Tools Used: SQL, SQL Server

# Business Needs: 
The primary business objective is to gain insights into customer behavior using point-of-sale (POS) data from our retail store. Through comprehensive data analysis, we aim to uncover purchasing trends, product 
preferences, and customer segmentation. This analysis will enable us to optimize inventory levels, tailor marketing campaigns, and enhance the overall shopping experience. By understanding customer behavior more deeply, we strive to make informed decisions that drive sales growth, increase profitability, and build stronger relationships with our customers."

# Business Object 1 
## Which channel is most frequently used for transactions?
 ### -(Code)
 SELECT TOP 1 store_type AS most_frequent_channel, COUNT(*) AS transaction_count FROM Transactions group by store_type order by COUNT(*) DESC
   ## -(Result)
   
  ### ![BO1](https://github.com/SLJyothi/E-COMMERCE-RETAIL-DATA-ANALYSIS/assets/164232591/fd7c06cf-eac0-411d-983e-31f0b0302ee9)


 ## -(Object Result) 
The analysis of transaction data from the 'Transactions' table reveals that the store type 'most_frequent_channel' is the most popular channel based on transaction count. The query identified the store type with the highest number of transactions, providing valuable insights into customer preferences and channel effectiveness. This information can be utilized by the retail store to prioritize marketing efforts, optimize inventory for the most frequented channels, and enhance overall business strategies to capitalize on the most popular sales channels and drive revenue growth.
      
# Business Object 2
## What is the count of Male and Female customers in the database?
 ### -(Code)
SELECT Gender, COUNT(*) AS Count FROM Customers GROUP BY Gender;
 ## -(Result)
 
## ![BO2](https://github.com/SLJyothi/E-COMMERCE-RETAIL-DATA-ANALYSIS/assets/164232591/5e8c1828-102a-4722-8b69-e36adc6d49c9)


## -(Object Result) 
The analysis of customer data from the 'Customers' table provides a breakdown of gender distribution among customers. The query grouped customers by gender and counted the number of occurrences for each gender category. This data offers valuable insights into the demographic composition of the customer base, allowing for targeted marketing strategies and personalized promotions. Understanding the gender distribution can help the retail store tailor its product offerings, advertising campaigns, and customer engagement initiatives to better resonate with different customer segments, ultimately driving sales and enhancing customer satisfaction."

# Business Object 3
## From which city do we have the maximum number of customers and how many?
 ### -(Code)
SELECT TOP 1 city_code AS city_code , COUNT(*) AS number_customer FROM customers GROUP BY city_code ORDER BY COUNT(*) DESC;
 ## -(Result)

 ## ![image](https://github.com/Himanshu2112000/Data_Analysis_Retail_business_SQL/assets/164239242/648cc03c-181e-4a43-a364-240c17aac812)

 ## -(Object Result)  
The analysis of customer data from the 'Customers' table reveals the city with the highest number of customers based on city_code. The query identified the city_code with the largest customer base, providing critical insights into regional customer distribution. This information can be leveraged to focus marketing efforts, tailor promotions, and optimize inventory to meet the demands of the most populated city. Understanding the geographic distribution of customers enables the retail store to implement targeted strategies, expand market reach, and enhance customer engagement to drive sales and foster brand loyalty in key regions.
    
# Business Object 4
## How many sub-categories are there under the Books category?
  ### -(Code)
 Select count(*) as no_subcategory from prod_cat_info where prod_cat = 'books'
  ## -(Result)

  ## ![image](https://github.com/Himanshu2112000/Data_Analysis_Retail_business_SQL/assets/164239242/1bb3ad41-baf0-4c7f-9d96-64df012db9a6)

  ## -(Object Result)
 The query on 'prod_cat_info' indicates the count of subcategories under the 'books' category. This insight informs inventory and marketing 
 decisions, helping the retail store to diversify and optimize its 'books' product range based on customer preferences and demand.
  
# Business Object 5
## What is the maximum quantity of products ever ordered?
  ### -(Code)
  SELECT p.prod_cat, COUNT(qty) AS no_product_category FROM Transactions t JOIN prod_cat_info p ON t.prod_subcat_code = p.prod_sub_cat_code 
  GROUP BY p.prod_cat;
   ## -(Result)

 ## ![image](https://github.com/Himanshu2112000/Data_Analysis_Retail_business_SQL/assets/164239242/84c446bd-3415-4088-aa69-1420805e2f91)

  ## -(Object Result)
 The query joins 'Transactions' with 'prod_cat_info' to count products by category. Grouped by product category (p.prod_cat), it provides 
 insights into the distribution of product categories based on the quantity of transactions. This analysis aids in understanding purchasing 
 patterns and helps optimize inventory for different product categories to enhance sales and customer satisfaction.

# Business Object 6
## What is the net total revenue generated in categories Electronics and Books?
   ### -(Code)
  select distinct sum(t.total_amt) as total_revenue,pc.prod_cat from Transactions t join prod_cat_info pc on t.prod_cat_code = 
  pc.prod_cat_code where pc.prod_cat in ('electronics','books') group by pc.prod_cat
   ## -(Result)
   
## ![image](https://github.com/Himanshu2112000/Data_Analysis_Retail_business_SQL/assets/164239242/73ff53b2-6538-49d1-b5a0-1f43cbea1b20)

 ## -(Object Result)
The query calculates the total revenue for distinct product categories, specifically 'electronics' and 'books', by joining 'Transactions' with 'prod_cat_info' on matching product category codes. The results offer insights into revenue generated from these two product categories individually. This analysis assists in evaluating the performance of 'electronics' and 'books' segments and guiding targeted marketing and inventory strategies to optimize sales and profitability
 
   
# Business Object 7
## How many customers have >10 transactions with us, excluding returns?
  ### -(Code)
select  cust_id, count(cust_id) as no_trans_by_customer from Transactions where total_amt > 0 group by cust_id
having count(*) > 10
   ## -(Result)

## ![image](https://github.com/Himanshu2112000/Data_Analysis_Retail_business_SQL/assets/164239242/0cf64ce9-3f24-4353-86e0-dddd7395dddd)

 ## -(Object Result) 
The query identifies customers with more than 10 transactions where the total amount spent is greater than zero. It counts the number of transactions (no_trans_by_customer) for each customer (cust_id) and filters the results to focus on loyal or frequent customers. This analysis provides insights into customer behavior and purchasing frequency, aiding in customer segmentation, targeted marketing, and personalized engagement strategies to enhance customer loyalty and drive sales.

# Business Object 8
## What is the combined revenue earned from the "Electronics" & "Clothing" categories, from "Flagship stores"?
  ### -(Code)
select sum(t.total_amt) as total_revenue from Transactions t join prod_cat_info pc on t.prod_cat_code = pc.prod_cat_code
where pc.prod_cat in ('electronics','clothing')  group by t.Store_type having t.Store_type = 'Flagship store'
  ## -(Result)

  ## ![image](https://github.com/Himanshu2112000/Data_Analysis_Retail_business_SQL/assets/164239242/18bdbe6e-a841-4f94-9f64-bc630ca1e397)

 ## -(Object Result)
The query calculates the total revenue from transactions related to 'electronics' and 'clothing' product categories, specifically for the 'Flagship store' store type. By joining 'Transactions' with 'prod_cat_info' based on matching product category codes, it provides insights into revenue generated from these categories at flagship stores. This analysis assists in evaluating the performance of specific product categories at flagship locations, guiding inventory management and promotional strategies to optimize sales and profitability.

# Business Object 9
## What is the total revenue generated from "Male" customers in "Electronics" category? Output should display total revenue by prod sub-cat.
  ### -(Code)
select sum(t.total_amt) as M_total_revenue from Transactions t join customers c on c.customer_Id = t.cust_id join prod_cat_info p on t.prod_cat_code = p.prod_cat_code where c.Gender ='M' group by p.prod_cat having  p.prod_cat = 'electronics'
  ## -(Result)

  ## ![image](https://github.com/Himanshu2112000/Data_Analysis_Retail_business_SQL/assets/164239242/8f294ff2-5fba-4d21-be77-421193a07b9b)

## -(Object Result)
The query calculates the total revenue from transactions related to the 'electronics' product category specifically for male customers. By joining 'Transactions', 'customers', and 'prod_cat_info' tables, it provides insights into the revenue generated from 'electronics' purchases made by male customers. This analysis helps in understanding male purchasing behavior in the electronics category, guiding targeted marketing campaigns and inventory strategies to cater to this specific customer segment and optimize sales.

 # Business Object 10
## What is percentage of sales and returns by product sub category; display only top 5 sub categories in terms of sales?
  ### -(Code)
select top 5 (prod_subcat), ROUND(sum(total_amt),2) as Sales_amount from Transactions as T inner join prod_cat_infO as P on T.prod_cat_code = P.prod_cat_code  where T.total_amt > 0 group by prod_subcat order by Sales_amount desc'
  ## -(Result)

  ## ![image](https://github.com/Himanshu2112000/Data_Analysis_Retail_business_SQL/assets/164239242/d333aace-eeb4-4f19-b43a-e491e663ce1b)

 ## -(Object Result)
 The query identifies the top 5 product subcategories based on sales amount from the 'Transactions' table, where the total amount is greater than zero. By joining 'Transactions' with 'prod_cat_info', it calculates and rounds the total sales amount for each product subcategory. This analysis offers insights into the best-performing product subcategories, guiding inventory management, marketing strategies, and product promotions to optimize sales and enhance profitability
 
# Business Object 11
## For all customers aged between 25 to 35 years find what is the net total revenue generated by these consumers in last 30 days of transactions from max transaction date available in the data?
  ### -(Code)
with ABC
as(select top 30 (tran_date), sum(total_amt) as Total_amount from Customers as C inner join Transactions as T on T.cust_id = C. customer_id
where datediff(year,DOB, getdate()) between 25 and 35 group by tran_date order by tran_date desc) select sum(Total_amount) as Final_revenue from ABC

  ## -(Result)

  ## ![image](https://github.com/Himanshu2112000/Data_Analysis_Retail_business_SQL/assets/164239242/faf6240f-6833-4f86-bb93-70b0a2093ca2)

 ## -(Object Result) 
 "The query calculates the total revenue generated from transactions by customers aged between 25 and 35 years old, considering the top 30 transaction dates based on total amount. It uses a Common Table Expression (CTE) named 'ABC' to first identify the top transaction dates within the specified age range. The main query then sums up the 'Total_amount' from the CTE to provide the final revenue generated from this customer segment. This analysis assists in understanding the spending behavior of young to middle-aged customers, guiding targeted marketing and promotional strategies to optimize sales and customer engagement.
 

 # Business Object 12
## Which product category has seen the max value of returns in the last 3 months of transactions??
  ### -(Code)
select prod_cat, count(Qty) as No_of_returns from Transactions as T inner join prod_cat_info as P on T.prod_cat_code = P.prod_cat_code
where total_amt < 0 and datediff(month, '2014-09-01', tran_date) = 3 group by prod_cat
  ## -(Result)

  ## ![image](https://github.com/Himanshu2112000/Data_Analysis_Retail_business_SQL/assets/164239242/5ff026f8-7d12-46a5-927e-0e045ed8ed8a)

## -(Object Result)
The query calculates the number of returns for each product category within a specific three-month period, starting from September 1, 2014. It joins the 'Transactions' table with 'prod_cat_info' based on matching product category codes and filters transactions where the total amount is less than zero, indicating returns. This analysis provides insights into return rates for different product categories during the specified period, helping to identify potential issues with product quality, customer satisfaction, or inventory management that may require attention and optimization strategies to reduce returns and enhance profitability.
 
# Business Object 13
## Which store-type sells the maximum products; by value of sales amount and by quantity sold?
  ### -(Code)
select top 1(Store_type), count(Qty) as No_of_products, sum(total_amt) as Amount from Transactions
where total_amt > 0 group by Store_type order by No_of_products desc
  ## -(Result)

  ## ![image](https://github.com/Himanshu2112000/Data_Analysis_Retail_business_SQL/assets/164239242/78a269d6-1c01-43f0-bbce-b8285c2cd769)

## -(Object Result) 
The query identifies the store type with the highest number of sold products and corresponding total sales amount from the 'Transactions' table. It filters transactions where the total amount is greater than zero to focus on successful sales. The results are grouped by store type and sorted in descending order based on the number of products sold. This analysis offers insights into the performance of different store types in terms of sales volume and revenue, guiding strategies to optimize sales, inventory management, and promotional activities to drive profitability and business growth.
 
# Business Object 14
## What are the categories for which average revenue is above the overall average?
  ### -(Code)
select prod_cat, round(avg(total_amt), 2) as Averages from Transactions T inner join prod_cat_info P on T.prod_cat_code = P.prod_cat_code
group by prod_cat having avg(total_amt) > (select avg(total_amt) from Transactions)
  ## -(Result)

  ## ![image](https://github.com/Himanshu2112000/Data_Analysis_Retail_business_SQL/assets/164239242/df1e5c7c-57c4-430e-9f2b-ebc3f5c13fcf)

## -(Object Result) 
The query calculates the average transaction amount for each product category from the 'Transactions' table, joining with 'prod_cat_info' based on matching product category codes. The results are filtered to include only product categories with an average transaction amount greater than the overall average transaction amount across all categories. This analysis identifies product categories that perform above the average, providing insights to focus on high-performing categories for inventory management, marketing strategies, and promotional activities to optimize sales and profitability.

# Business Object 15
## Find the average and total revenue by each subcategory for the categories which are among top 5 categories in terms of quantity sold.
  ### -(Code)
  select top 5(prod_cat), count(Qty)as Quantity_sold from Transactions T inner join prod_cat_info P on T.prod_cat_code = T.prod_cat_code 
  where total_amt > 0 group by prod_cat order by Quantity_sold desc
  ## -(Result)

  ## ![image](https://github.com/Himanshu2112000/Data_Analysis_Retail_business_SQL/assets/164239242/a0dea646-624c-4d70-8ecc-58fe68ac0f20)

## -(Object Result)
The query identifies the top 5 product categories based on the quantity of products sold from the 'Transactions' table. It joins 'Transactions' with 'prod_cat_info' based on matching product category codes and filters transactions where the total amount is greater than zero, focusing on successful sales. The results are grouped by product category and sorted in descending order based on the quantity sold. This analysis provides insights into the best-selling product categories, guiding inventory management, marketing strategies, and promotional activities to optimize sales and enhance profitability.

# Recommendations
Based on the previous result, here are some recommendations for the business:

#### Inventory Management:
Prioritize stocking and replenishing the top 5 best-selling product categories to ensure product availability and meet customer demand effectively.

#### Marketing Strategies:
Allocate a higher marketing budget and promotional efforts towards the identified top-performing product categories to capitalize on their popularity and drive sales.

#### Product Bundling: 
Consider creating product bundles or packages incorporating items from the top-selling categories to encourage higher sales and increase average transaction value.

#### Customer Engagement: 
Develop targeted marketing campaigns and personalized promotions for the top-selling product categories to engage customers and enhance their shopping experience.

#### Supplier Negotiations:
Negotiate better terms with suppliers for the top-performing product categories to improve profit margins and reduce costs.

#### Inventory Analysis: 
Conduct a detailed inventory analysis to identify slow-moving items in other categories and consider reevaluating their placement, pricing, or promotion strategies to boost sales.

#### Cross-Selling Opportunities:
Explore cross-selling opportunities by recommending products from the top-performing categories to customers purchasing items from other categories to increase average transaction value.

By implementing these recommendations, the business can optimize its sales strategies, improve inventory turnover, enhance customer satisfaction, and ultimately drive profitability and growth
