**<h3><p align="center">  Daily Batch Extraction</p></h3>** 

**Solution Request**

A supermarket generates thousands of sales entries each day which have to be queried. The analytics department is concerned about possibly overloading transactional database servers. Their real-time transactional data is currently stored in Amazon Aurora. They would like to be able to cross-reference data from their current system with data from other sources in the future. But, right now they want a solid analytics solution for the data they already have. 

**Main AWS Services to be used**

We will use data lakes (**Amazon S3**) to store data that is extracted in batches from one or more data sources and staged for later use when creating business analytics and reports.

**AWS Glue** and **AWS Glue Studio** were designed for this task. We we'll create jobs that run on a set schedule to extract any new data and store it in the data lake. 

We can then use **Amazon Athena** to query and analyze the data in the data lake to gain new insights into the business.

We can design **AWS Glue jobs** to clean up data in the process. We can remove inconsistencies, such as missing fields, badly formatted data, or duplicate records, so that data lake is as clean as possible for higher quality query results.


**Architecture**

![Daily Batch Extraction (4)](https://github.com/user-attachments/assets/e5b746a7-8a3c-45e5-b75e-0692e20ac268)


**Explanation of the architecture**

This solution uses _AWS Glue_ to extract, transform, and load data from the _Amazon Relational Database Service_ (Amazon RDS) to a _Simple Storage Service_ (Amazon S3) bucket. It then uses _Amazon Athena_ to run on-demand queries.

  1. An AWS Glue crawler is used to extract raw data from Amazon RDS.  The data schema is inferred and imported into the AWS Glue Data Catalog.
  2. The data is transformed by an AWS Glue job, removing personally identifiable information (PII)—in this case, the date of birth—before archival storage in an Amazon S3 bucket. 
  3. Users run queries, as needed, on the data by using the Amazon Athena query editor, which retrieves schema info from the Data Catalog. 
  4. Processed query data is saved to a different S3 bucket for later on-demand reporting use.
