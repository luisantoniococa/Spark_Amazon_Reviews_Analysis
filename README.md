# Spark_Amazon_Reviews_Analysis

### Background
Many of Amazon's shoppers depend on product reviews to make a purchase. Amazon makes these datasets publicly available. However, they are quite large and can exceed the capacity of local machines to handle. One dataset alone contains over 1.5 million rows; with over 40 datasets, this can be quite taxing on the average local computer. 

### Overview
The goal of this Project is to perform the ETL process completely in the cloud and upload a DataFrame to an RDS instance. The second goal is to use PySpark and SQL to perform a statistical analysis of selected data.

### Introduction
Based in information of the dataset we are going to load the dataset in a Google colab notebook. Alse we are going to install spark, the jdk and java in the google colab to be able to run this big data tasks.

#### Connecting to the Database
+ Initially, a connection was made to the AWS RDS postgres database thru pyspark. 
+ For this example 2 notebooks were created to retrieve the big data from amazon S3 buckets that contained gz files
+ The data for Jewerly and Home Entertainment was retrieve and save into a spark instance.
#### ETL Process
+ The Schemata was identified and imported from the S3 bucket file. It can ve observed bellow the identified structure

![Schemata_sql](https://github.com/luisantoniococa/Spark_Big_Data_Amazon_Reviews_Analysis/blob/master/Schemata_screenshot.png)

+ Next, 4 SQL tables were created with queries 
  + customers
  + products
  + review_id_table
  + vine_table
  find queries at this [sql_file](https://github.com/luisantoniococa/Spark_Big_Data_Amazon_Reviews_Analysis/blob/master/schema_amazon_reviews.sql)
+ Data from the S3 buckets was transformed in dataframes to fit the tables
  * Drop na values and duplicates were applied
  * Trasnformed text date to date format

+ Lastly, a connection to the AWS RDS postgres database server was created to load the new dataframes in the respectively tables.
#### Data Analysis
+ A new notebook was created and connected to AWS RDS postgres thru spark
+ The schemata for vine tables created earlier was imported.
+ The data was imported to a spark dataframe and filtered by helpful votes that are more than 20.
+ A ratio between total votes and helpful votes was created. The most helpful review by percentages plot can be observed below:

![bar_plot](https://github.com/luisantoniococa/Spark_Big_Data_Amazon_Reviews_Analysis/blob/master/percent_barplot.png)

+ 2 new dataframes were created that divided the data by if the are vine associated or not(paid or unpaid). The summary of those tables can be observed below

![vine_summaries](https://github.com/luisantoniococa/Spark_Big_Data_Amazon_Reviews_Analysis/blob/master/Vine_reviews_summaries.png)

+ Lastly a ratio of 5 stars reviews with vine or non vine was created and the summaries can be shown below:

![5_stars_reviews](https://github.com/luisantoniococa/Spark_Big_Data_Amazon_Reviews_Analysis/blob/master/5starsReviewsPaid_vs_Unpaid.png)

## Conclusion
We were able to determine important insights from the amazon reviews. We found out that about 50 percent of the products sent to the vine reviwers have 5 stars. For further analysis we can include a NLP from the data and identified which are the most generous reviewers from the amazon website.
