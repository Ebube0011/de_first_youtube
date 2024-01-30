# Youtube Data Engineering Project
![Youtube_Practice_Project-Architecture](https://github.com/Ebube0011/de_first_youtube/assets/149321069/d4a4e487-fc72-4a89-8bf8-2d5bb37b6549)
This project was carried out to improve my knowledge in data engineering and AWS. It is an amazing project that helped me ask multiple questions and questioned my existing knowledge on what i thought i knew.
There were a few problems that this project was aimed at solving, the main one being to provide data to allow end users answer analytical questions on youtube videos and their performance. With the main question being "what factors affect how popular a youtube video will be?"
I learned how to build a data lake on top of object storage to store raw data for business needs, as well as how important data management is in projects like these to improve data discoverability. I also learned a lot with regards to data transformation, and how impactful it can be to downstream users.

This project is designed to take data ingested into the object storage, clean and process it, transform it so it is ready for consumption, and finally serve it in the form of a dashboard for end users to answer critical questions.
The project is done in 2 parts, self managed and cloud managed. This is to ensure i am not lazy and take certain things for granted, and also due to my curiosity to understand and improve. The focus is on the basics, to ensure I'm capable of adapting to each workload.

## Table of Contents
* Goal
* Cloud managed
  * Ingestion
  * Transformation
  * Serve
* Self managed
  * Ingestion
  * Transformation
  * Serve

### Goal
The goal of this project is to provide clean, reliable data for analytics to answer questions like 'what factors affect how popular a youtube video will be?'

### Cloud Managed
#### Ingestion
The data was gotten from a kaggle dataset and uploaded into the s3 bucket landing. The ingestion pattern used in this project is the ELT (extract, load, transform) pattern. As the data has already been extracted and loaded into the landing bucket, what is next is the transformation of said data. There are two main groups of data ingested; raw statistics, and reference data. AWS Glue crawler is used to crawl through both groups of raw data to get metadata and create tables in a raw data database inorder to explore the data for possible errors or missing data, and clean and transform the data. Issues arose with both datasets, aws lambda was used to filter a portion of the reference dataset, store it back into a new bucket with a parquet serialization (using the lambda func python file in the repository), and used aws glue to add the new data into a new database table for cleaned data. The raw statistics dataset underwent schema transformation using aws glue jobs, converted to parquet serialization, placed back into the bucket with cleaned data(using the pyspark python file in the repository), and used aws glue to add the data into the database table for cleaned data.
  Storage: data lake (object storage) to store data in its raw form.
  Data management: aws glue catalogue for discoverability.
  Security: IAM roles are created for services to perform their tasks.
  DataOps: Automated transformation using aws lambda trigger and aws glue scheduling, and Observability using aws cloudwatch to monitor performance metrics and report using aws       sns in the case of an incident.

#### Transformation
The data in the datalake is transformed using aws glue to perform joins on the two tables to produce the final data needed for analytics. The new data is placed in a seperate bucket ready to be served to analytics end users.
  Storage: data lake (object storage) to store the transformed data.
  Security: IAM roles are created for services to perform their tasks.
  Data management: aws glue catalogue for discoverability.
  DataOps: Automated transformation using aws lambda trigger and aws glue scheduling, and Observability using aws cloudwatch to monitor transformation duration and report using       aws sns in the case of an incident.

#### Serve
The Transformed data is served to the endusers in the form of a dashboard to visualize the performance of videos and their popularity.


## Credits
The project would no be possible without Darshil parmer's youtube videos.
