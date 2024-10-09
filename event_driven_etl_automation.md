**<h3><p align="center"> Event-Driven ETL Automation </p></h3>** 

**Solution Request**

A logistics company wants to plan the purchase of fuel for its trucks based on the amount of cargo to be transported and the distance the trucks will travel. The company wants a daily report that contains aggregated information about the next day's deliveries, and it wants the process to be automated through a workflow.


**Main AWS Services to be used**

- Configure Lambda function to automatically start Step Functions workflow.
- Create Step Functions workflow to coordinate data analytics pipeline.
- S3 bucket to store landing, staging and consumption data
- Athena to query from consumption bucket
- AWS Glue for data cataloging and jobs
- SNS topic for sending notification emails to the admin


**Architecture**

![Event-Driven ETL Automation](https://github.com/user-attachments/assets/95bdd36a-b4d7-4da3-be30-f69a522ab4d0)




**Explanation of the architecture**

This solution uses AWS Step Functions to automate the data ingestion and data preprocessing for final consumption.

1. A shipment planning application runs on an AWS Lambda function. The application drops a JSON file into the landing bucket in Amazon Simple Storage Service (Amazon S3). This action invokes another Lambda function to start a Step Functions workflow.
2. Step Functions starts an AWS Glue job to convert the raw JSON file into a Parquet file. The newly created Parquet file is stored in the staging bucket in Amazon S3.
3. After the AWS Glue job is completed, Step Functions starts an AWS Glue crawler to discover the schema and metadata in the Parquet file. A new AWS Glue Data Catalog is created to store the metadata of this raw data.
4. A different AWS Glue job drops a column, customer_name, into the Parquet file and stores the result in a new file in the staging bucket in Amazon S3.
5. After the customer_name column is dropped, Step Functions starts a second AWS Glue crawler to extract the metadata and schema from the new data.
6. After the second AWS Glue crawler runs, Step Functions calls Amazon Athena to run a SQL query on top of the already enriched data. This query generates a report that provides the amount of fuel to be purchased for the next day. The report is stored in the consumption bucket in Amazon S3, and it can be downloaded as a CSV file.
7. At the end of the workflow, Step Functions calls Amazon Simple Notification Service (Amazon SNS) to send an email to subscribers. 





