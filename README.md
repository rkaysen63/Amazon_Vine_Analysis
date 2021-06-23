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
* Data: 
  *  https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Watches_v1_00.tsv.gz
  *  2nd set for additional analyis: https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Furniture_v1_00.tsv.gz
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
The Amazon Vine program uses Vine Voices to provide customers unbiased reviews of Amazon products.  Vine Voices are customers that are invited to join the program based on their reviewer rank.  The Vine members receive free products from Amazon that are provided by participating vendors, but vendors cannot influence, modify or edit the reviews.  More about Amazon Vine is available at https://www.amazon.com/gp/vine/help.<br/>

Amazon's reviews datasets (https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt) are organized by product category. The "Watches" reviews dataset was selected for this analysis.  The purpose of this analysis is to determine if Amazon Vine members truly provide unbiased reviews of Amazon products, per Amazon's claim.<br/>

For the analysis, the Amazon reviews dataset for watches is extracted into a dataframe, `df`.  Then a smaller dataframe, `vine_df`, is created by selecting only 6 columns of the original `df`:  review_id, star_rating, helpful_votes, total_votes, vine, verified_purchase.  `vine_df` is filtered into a dataframe called `df_reviews20` that only includes rows where the total votes are 20 or more.  `df_reviews20` is filtered to create a dataframe called `df_helpful` where the number of helpful_votes divided by total_votes is equal to or greater than 50%.  Finally, `df_helpful` is divided into two dataframes:  `vine_Y_df` that contains only reviews by Vine members and `vine_N_df` that contains only reviews by non-Vine members.

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

Taken at face value, the results of this analysis show no bias by Amazon Vine members toward favorable reviews.  Approximately 1/3 of the Vine members gave 5-star reviews for watches whereas half of non-Vine members gave 5-star reviews.  However the following should be considered:
1. The total transformed dataset includes 8373 reviews.  The Vine reviews madeup less than 1% of all the reviews.  In other words, it's a very small dataset from which to draw conclusions.
2. The transformed dataframe, df_helpful, was filtered even further to include only those reviews where purchases were verified.  The number of Vine reviews decreased from a small number, 47, to 0.  In other words, the 47 5-star reviews by Vine members were possibly written about items that they had not purchased, which undermines the validity of their reviews.

<p align="center">
  <img src="additional_analysis/verified_df.png" width="700">  
</p> 

3. This analysis evaluates only one of approximately 50 Amazon reviews datasets.  It might be worth analyzing another set of data before reaching any conclusions about bias. A second review dataset, furniture reviews, was extracted to a dataframe and transformed in order to see how the results compare.  Please refer to the images below. A little over 1/2 of the Vine members gave 5-star reviews for Amazon furniture products.  A little under 1/2 of the non-vine members gave 5-star reviews for Amazon furniture products.  Again, no apparent bias based on face value.  The furniture dataset was approximately double the size of the watches dataset.  Similar to the watches dataset, the Vine reviews made up less than 1% of all the reviews. When filtered even further to select only those reviews where purchases were verified, the Vine reviews dropped significantly.  The Vine dataframe was reduced to only 3 rows and only 2 of those rows had 5-star reviews.  Again, this result casts doubt on the validity of Vine reviews.

<p align="center">
  <img src="additional_analysis/furniture_Y_percent_5star.png" width="700">
  <br/><br/> 
  <img src="additional_analysis/furniture_N_percent_5star.png" width="700">  
  <br/><br/> 
  <img src="additional_analysis/verified_furniture_df.png" width="700">  
</p><br/>

4. The original analysis only looks at favorable reviews.  What do poor reviews have to say?  To answer that question, poor reviews of both datasets were analyzed.  Please refer to the images below.  For both datasets, the poor Vine reviews, that is reviews rated 1 or 2 stars, were much less than the poor non-Vine reviews.  For the "Watches" dataset, poor Vine reviews were about half of the poor non-Vine reviews.  For the larger "Furniture" reviews dataset, the desparity was even greater.  For the "Furniture" reviews dataset only 1% of the Vine reviews are poor, wherease 26% of the non-Vine reviews were poor.  The percentage of poor non-Vine reviews for both datasets is roughly the same.

<p align="center">
  <img src="additional_analysis/watches_poor_reviews.png" width="650">
  <br/><br/> 
  <img src="additional_analysis/furniture_poor_reviews.png" width="800">   
</p><br/>

In conclusion, the data does not absolutely refute Amazon's claim that Vine Voices provide unbiased reviews, but it does appear that there is bias by Vine reviewers to give more favorable reviews than not.  At face value the results show highly favorable Vine reviews to be about the same or less than non-Vine reviews, possibly indicating no bias.  But, when the requirement of "verification of purchase" is considered, there's no or almost no Vine reviews to analyze, suggesting Vine bias because it would appear that Vine Voices are giving highly favorable reviews to products that they had not purchased and possibly have never tried.  Furthermore, when poor reviews are analyzed, it's clear that Vine Voices are more reluctant to give products a poor review than non-Vine "voices".


[Back to the Table of Contents](https://github.com/rkaysen63/Amazon_Vine_Analysis/blob/master/README.md#table-of-contents)
