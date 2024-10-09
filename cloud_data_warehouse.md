**<h3><p align="center"> Cloud Data Warehouse </p></h3>** 

**Solution Request**

A game studio is planning to offer more in-game purchased items to increase revenues. 
Before they can come up with a strategy, their marketing manager wants to understand the current players’ 
in-game purchase behavior. They have been capturing player data from their most successful games and storing 
it in a data lake built on Amazon S3. The data is semi-structured and contains nested data structures. They want 
to convert this data into a structured format and ingest it into a cloud data warehouse that supports a low query 
response time. Their customers are growing very fast. They want to run repeated queries on a very large dataset 
that requires a very low response time.  As a data engineer what would you suggest to them? 


**Main AWS Services to be used**

- Create an **AWS Glue job** to _flatten the data_.
- Use **Amazon Redshift Spectrum** _to query_ the flattened data.
- Create a **materialized** view _to query_ data.
- **Kinesis Data Firehose** _for ingesting_ game data into S3 bucket
- **Athena** _to query flattened data_ directly in S3


**Architecture**

![Cloud Data Warehouse](https://github.com/user-attachments/assets/3369560e-cdd6-4ae9-87bc-1194511c8b82)

**Explanation of the architecture**

This solution transforms semi-structured data into relational tables so that you can query the transformed data in an Amazon Simple Storage Service (Amazon S3) bucket, using Amazon Redshift Spectrum, without the need to move the data into a data warehouse.

1. Amazon Kinesis Data Firehose is a fully managed service that you can use to deliver real-time streaming data to destinations such as Amazon S3, Amazon Redshift, Amazon OpenSearch Service, Splunk, and any custom HTTP endpoint.
2. Players' game data is sent to Kinesis Data Firehose and stored in a data lake built on Amazon S3. This semi-structured JavaScript Object Notation (JSON) data contains nested data structures. 
3. Amazon Athena is an interactive query service that helps you analyze data in Amazon S3 by using standard Structured Query Language (SQL).
4. You can create a job in AWS Glue to process the data by applying a built-in transformation to flatten the nested data structure. A job in AWS Glue consists of the business logic that performs extract, transform, and load (ETL) work.
5. The flattened data is stored in another S3 bucket (consumption zone) of the data lake.
6. You can analyze the flattened data stored in Amazon S3 by running SQL queries directly in Athena.
7. Amazon Redshift is a fully managed, petabyte-scale data warehouse service in the cloud. Amazon Redshift uses SQL to analyze data across data warehouses, operational databases, and data lakes. You can access data lakes from an Amazon Redshift cluster by creating Amazon Redshift external schemas.
8. Amazon Redshift provides seamless integration between data warehouses and data lakes running on AWS by using Amazon Redshift Spectrum. Redshift Spectrum resides on dedicated Amazon Redshift servers that are independent of your cluster. You can query Amazon S3 flattened data without having to load the data into Amazon Redshift tables.
9. You can create a materialized view to speed up a query that is predictable and repeated. Amazon Redshift returns the precomputed results from the materialized view without having to access the base tables. The query results are returned much faster compared to when you retrieve the same data from the base tables. You can create more than one materialized view based on your data analytics needs.





