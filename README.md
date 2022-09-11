# Amazon_Vine_Analysis

## Overview
The purpose of this challenge was to analyze Amazon reviews written by members of the paid Amazon Vine program. We needed to determine if there are any biases between Vine members and Non-Vine member's reviews. In order to decide if there were any biases towards favorable reviews from Vine members vs. non-members.

In this project, we will have access to approximately 50 datasets. Each one contains reviews of a specific product, from clothing apparel to wireless products. I chose https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Wireless_v1_00.tsv.gz and we needed to identify the percentage of 5-star ratings to total ratings

I used Google Colaboratory to import PySpark libraries to extract the dataset, transform the data, connect to AWS RDS instance and load the transformed data into pgAdmin

## Deliverable 1: Perform ETL on Amazon Product Reviews
•	Create a new database with Amazon RDS
•	In pgAdmin, run a new query to create the tables for your new database
  
  o	Customers_table
  <img width="1067" alt="Customers_df" src="https://user-images.githubusercontent.com/105124485/189511263-35bbe054-be96-423a-9273-5fb5f218dd48.png">

  o	Products_table
  <img width="912" alt="Products_df" src="https://user-images.githubusercontent.com/105124485/189511267-36b559f2-579e-4ca2-b343-2bfee0d16a33.png">

  o	Review_id_table
  <img width="1069" alt="Review_df" src="https://user-images.githubusercontent.com/105124485/189511275-5175a4e1-6d93-4a55-9bb5-631deb7e30e3.png">

  o	Vine_table
  <img width="1067" alt="Vine_df" src="https://user-images.githubusercontent.com/105124485/189511281-14eb1a6e-8085-4d18-9c97-90e3ac9994eb.png">

•	Create a Google Colab Notebook
•	Use the groupby() function on the customer_id column of the DataFrame
•	Count all the customer ids using the agg() function by chaining it to the groupby() function. After you use this function, a new column will be created, count(customer_id).
•	Rename the count(customer_id) column using the withColumnRenamed() function so it matches the schema for the customers_table in pgAdmin
•	Use the select() function to select the product_id and product_title, then drop duplicates with the drop_duplicates() function to retrieve only unique product_ids
•	Use the select() function to select the columns that are in the review_id_table in pgAdmin and convert the review_date column to a date
•	Use the select() function to select only the columns that are in the vine_table in pgAdmin
•	Load the newly created DataFrames into pgAdmin

<img width="255" alt="PG Admin - Customers" src="https://user-images.githubusercontent.com/105124485/189511294-e957ef1c-046e-4118-94b7-415b661691c3.png">

<img width="208" alt="PG Admin - Products" src="https://user-images.githubusercontent.com/105124485/189511296-15821270-179a-40ea-8d23-de24001ee61d.png">

<img width="511" alt="PG Admin - Vine" src="https://user-images.githubusercontent.com/105124485/189511337-5d251846-28f2-4e99-983a-4c376fd1b69b.png">

<img width="468" alt="PG Admin - Reviews" src="https://user-images.githubusercontent.com/105124485/189511431-5619daa0-2358-412a-9ba4-0e487e0d8293.png">

## Deliverable 2: Determine Bias of Vine Reviews
•	Filter the data and create a new DataFrame or table to retrieve all the rows where the total_votes count is equal to or greater than 20, but first delete zero values with dropna()
<img width="1050" alt="Total Votes" src="https://user-images.githubusercontent.com/105124485/189511404-5ca11feb-180a-4631-bb8e-4ee6ccfe7f56.png">

•	Filter the new DataFrame or table created and create a new DataFrame or table to retrieve all the rows where the number of helpful_votes divided by total_votes is equal to or greater than 50%.
<img width="1052" alt="Percent of Votes" src="https://user-images.githubusercontent.com/105124485/189511412-20b744f2-14bd-43d1-83a0-c7c65b5a61ae.png">

•	Create a new DataFrame or table that retrieves all the rows where a review was written as part of the Vine program (paid)
<img width="982" alt="Y Reviews" src="https://user-images.githubusercontent.com/105124485/189511376-38b78d4b-370a-4148-bd54-46814de9e265.png">

•	Create a new DataFrame or table that retrieves all the rows where a review was not part of the Vine program (unpaid)
<img width="972" alt="N Reviews" src="https://user-images.githubusercontent.com/105124485/189511379-58036395-8b96-4959-bbe9-f03ec20cc842.png">

•	Determine the total number of reviews, the number of 5-star reviews, and the percentage of 5-star reviews for the two types of review (paid vs unpaid)
<img width="1060" alt="Vine Reviews" src="https://user-images.githubusercontent.com/105124485/189511457-fc41e40e-bda2-44d6-be77-98fd9ae5681e.png">


•	I used PySpark to create and filter all the DataFrames

## Deliverable 3: A Written Report on the Analysis (README.md)
Enclosed

## Summary
Based on the results, Vine members did not display bias when rating their products bearing in mind that the number of 5-star ratings was about 10% less than Non-Vine members with 47% for Non-Vine members vs  36% for Vine members. We can assume that Vine customers are more analytical when submitting their reviews. Nonetheless, in order to support this assumption further, we should include all of the data rather than filtering it to a percentage of helpful vs. total votes like we did for this exercise. Reviewing all the data might give us additional information.
