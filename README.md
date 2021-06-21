# Amazon Vine Analysis

<p align="center">
  <a href="#">Amazon Watches</a>
  <br/><br/> 
  <img src="images/amazon_watches.png" width="800">
</p>
  
## Table of Contents
* [Overview](https://github.com/rkaysen63/Amazon_Vine_Analysis/blob/master/README.md#overview)
* [Resources](https://github.com/rkaysen63/Amazon_Vine_Analysis/blob/master/README.md#resources)
* [Results](https://github.com/rkaysen63/Amazon_Vine_Analysis/blob/master/README.md#results)
* [Summary](https://github.com/rkaysen63/Amazon_Vine_Analysis/blob/master/README.md#summary)

## Resources:    
* Data: https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Watches_v1_00.tsv.gz
* Tools: 
  * Python
  * Colaboratory (Colab) notebook for writing code
  * PostgreSQL database engine
  * pgAdmin platform to set up database tables and query data
  * AWS Console for big data management
  * Apache Spark to perform ETL on big data
* Screen shot of watches from https://www.amazon.com/s?k=watches&ref=nb_sb_noss_1
* Lesson Plan: UTA-VIRT-DATA-PT-02-2021-U-B-TTH, Module 16 Challenge

## Overview:
The Amazon Vine program uses Vine Voices to provide customers unbiased reviews of Amazon products.  Vine Voices are customers that are invited to join the program based on their reviewer rank.  The Vine members receive free products from Amazon that are provided by participating vendors, but vendors cannot influence, modify or edit the reviews.  More about Amazon Vine is available at https://www.amazon.com/gp/vine/help.

Amazon's review datasets (https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt) are organized by product category. The "Watches" dataset was selected for this analysis that proposes to determine if Amazon Vine members provide more favorable reviews than non-Vine members.

## Results:
### ETL

* **Extract:**<br/>
<p align="center">
  <a href="#">Extract Amazon Review Dataset, "Watches", as a Dataframe (df)</a>
  <br/><br/> 
  <img src="images/del_1_etl/df.png" width="1200">
</p>    

* **Transform:**<br/>
  Transform df into four dataframes: **customers_df, products_df, review_id_df, vine_df**      
  
<p align="center">
  <a href="#">customers_df</a>
  <br/><br/> 
  <img src="images/del_1_etl/customers_df.png" width="800">
  <br/><br/> 
  <a href="#">products_df</a>
  <br/><br/> 
  <img src="images/del_1_etl/products_df.png" width="800">
  <br/><br/>
  <a href="#">review_id_df</a>
  <br/><br/>   
  <img src="images/del_1_etl/review_id_df.png" width="1000">
  <br/><br/> 
  <a href="#">vine_df</a>
  <br/><br/> 
  <img src="images/del_1_etl/vine_df.png" width="800">  
</p>   

* **Load:**<br/>
  Load the four dataframes into respective tables in pgAdmin:  **customers_table, products_table, review_id_table, vine_table**    

<p align="center">
   <a href="#">schema</a>
  <br/><br/> 
  <img src="images/del_1_etl/watches_database.png" width="350">
   <br/><br/>  
  <a href="#">customers_table</a>
  <br/><br/> 
  <img src="images/del_1_etl/customers_table.png" width="350">
  <br/><br/> 
  <a href="#">products_table</a>
  <br/><br/> 
  <img src="images/del_1_etl/products_table.png" width="350">
  <br/><br/>
  <a href="#">review_id_table</a>
  <br/><br/>   
  <img src="images/del_1_etl/review_id_table.png" width="500">
  <br/><br/> 
  <a href="#">vine_table</a>
  <br/><br/> 
  <img src="images/del_1_etl/vine_table.png" width="575">  
</p>    

### Determine Bias of Vine Reviews

<p align="center">
  <a href="#">DataFrame (vine_df) created by transforming a dataframe (df) that was extracted from an Amazon Reviews dataset for Watches</a>
  <br/><br/> 
  <img src="images/del_1_etl/vine_df.png" width="800">  
</p>    

<p align="center">
  <a href="#">DataFrame (df_reviews20) created from vine_df where there are 20 or more total votes</a>
  <br/><br/> 
  <img src="images/del_2_vine_analysis/df_reviews20.png" width="700">  
</p>  

<p align="center">
  <a href="#">Dataframe (df_helpful) created from df_reviews20 where the percentage of helpful_votes is equal to or greater than 50%</a>
  <br/><br/> 
  <img src="images/del_2_vine_analysis/df_helpful.png" width="700">  
</p> 

<p align="center">
  <a href="#">Dataframe (vine_Y_df) that only includes Vine reviews</a>
  <br/><br/> 
  <img src="images/del_2_vine_analysis/vine_Y_df.png" width="700">  
</p> 

<p align="center">
  <a href="#">Dataframe (vine_N_df) that only includes non-Vine reviews</a>
  <br/><br/> 
  <img src="images/del_2_vine_analysis/vine_N_df.png" width="700">  
</p> 

<p align="center">
  <a href="#">Pecentage of 5-Star reviews of total Vine reviews.</a>
  <br/><br/> 
  <img src="images/del_2_vine_analysis/Y_percent_5star.png" width="700">
  <br/><br/> 
  <a href="#">Pecentage of 5-Star reviews of total non-Vine reviews.</a>
  <br/><br/> 
  <img src="images/del_2_vine_analysis/N_percent_5star.png" width="700">  
</p> 

### Analysis of Vine Reviews

* Number of Reviews
  * There are 47 Vine reviews.
  * There are 8326 non-Vine reviews.

* 5-Star Reviews
  * Of the 47 Vine reviews, 15 received 5 stars.
  * Of the 8326 non-Vine reviews, 4321 received 5 stars.

* Percentage of 5-Star Reviews
  * 32% of the Vine reviews received 5 stars.
  * 52% of the non-Vine reviews received 5 stars.

## Summary:

Summary: In your summary, state if there is any positivity bias for reviews in the Vine program. Use the results of your analysis to support your statement. Then, provide one additional analysis that you could do with the dataset to support your statement.



[Back to the Table of Contents](https://github.com/rkaysen63/Amazon_Vine_Analysis/blob/master/README.md#table-of-contents)
