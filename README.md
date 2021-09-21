Project 3 : DataWarehousing on Cloud
 
1) Purpose of the Database : 
The major purpose of this project is to implement a data warehouse in the AWS. Nowadays data is growing at a rapid pace and we need to scale according to the demand. So, Implementing the data warehouse on the cloud is a feasible option so I have designed a redshift data warehouse which collects information from various sources which are present in S3 i.e multiple files. 
 
Project Flow:
I have created the staging tables and fact and dimension tables in redshift and loaded the data from s3 into staging tables and then performed dimensional modeling. Insert queries are written so that data is inserted from staging tables into the fact and dimension tables.
 
We have created an IAM role with full admin access and redshift cluster using python AWS SDK and copied the credentials in dwh.cfg file so that we can connect to the cluster. 
 
We run the create_tables.py file so that tables are created and then we run the etl.py file to load the data into fact and dimension tables. I have connected to the cluster using the query editor and ran some basic queries to verify that the data is loaded.
 
2) Database Schema:
We have 2 staging tables 
Staging_events: to store all the event data
Staging_songs: To store all the songs data
 
Fact Table:
Songplays: Which contains most of the songs played information
 
Dimension Tables : 
Users, Songs, Artists, Time 
 
I have used all the primary keys in each table as a sort key so that the data is organized and split into each slice which makes it faster for join operations. The distribution type used is all so that all the small dimension tables are splitted on each node.
 
The ETL pipeline built is quite simple which inserts the records into fact and dimension tables. 
 
3) Sample Queries :
 
Query 1: Top 3 locations to which most artists belong to 
select distinct count(artist_id) as count, location from artists group by location order by count desc limit 3;
Result : 
4811


147
London, England
146
Los Angeles, CA

