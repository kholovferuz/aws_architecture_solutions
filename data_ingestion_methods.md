**<h3><p align="center"> Data Ingestion Methods </p></h3>** 


**Solution Request**

In a package delivery company, a package tracking application is receiving lots of streaming data. Managing the data stream with current resources is getting expensive. Data analysts need the clickstream data, but they are concerned about the budget and the amount of resources required to operate effectively. They are also forecasting a huge growth. They need a solution to speed up data ingestion and transformation.

**Main AWS Services to be used**

  - _Create_ an **Amazon Data Firehose** stream.
  - _Configure_ clickstream data preprocessing with **AWS Lambda.**
  - _Configure_ clickstream storage into an **Amazon S3 bucket.**
  - _Create_ an Amazon Managed Service for **Apache Flink application.**

**Architecture**

![Data Ingestion Methods](https://github.com/user-attachments/assets/056aa221-d047-4442-b8a3-0cff3b068b26)

**Explanation of the architecture**

This solution uses Amazon Data Firehose to ingest, transform, and make real-time data available for business analysis. Data Firehose reliably loads streaming data into data lakes, data stores, and analytics services. Amazon Kinesis is a fully managed service that automatically scales to match data throughput. Kinesis requires no ongoing administration.
  1. A source application generates data from activities on a webpage. The data is represented by a sequence of clicks on each website link (clickstream data).
  2. The data is sent to Data Firehose, which runs a custom transformation through an AWS Lambda function. The transformed data is sent to its destination.
  3. After the data is stored in Amazon S3, AWS Glue can be used to catalog the data and its schema, and continually make updates as new data arrives. An AWS Glue crawler is used to discover new data and schema changes. After the crawler runs, the new data is ready to be queried by Amazon Athena.
  4. Amazon Athena is an interactive query service that can be used to analyze data directly in Amazon S3 by using standard SQL.
  5. Another Lambda function is used to receive and save the data to an Amazon DynamoDB table, which serves as the data source for one or more analytics dashboard applications.






