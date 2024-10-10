**<h3><p align="center"> Ingesting streaming exchange data in near real-time </p></h3>**

**Solution Request**

A financial company processes billions of records from the NASDAQ stock exchange, and their current on-premises 
database is not able to provide near real-time data to the clients. They want to implement a solution that can 
process their daily transaction reports so that, after the market closes, data can be consumed by billing and 
reporting processes before the markets open the next morning. 


**Main AWS Services to be used**

- Configure **Data Firehose** to _ingest_ and _convert_ transaction records.
- Configure a **crawler** and **Data Catalog** to _manage_ updates.
- Use **Amazon Redshift Spectrum** to _query_ the data lake.
- Create **materialized views** in Amazon Redshift.

**Architecture**

![Ingesting streaming exchange data in near real-time-2](https://github.com/user-attachments/assets/389bc36e-708d-4380-a7fe-b354287adb7e)


**Explanation of the architecture**

This solution uses Amazon Redshift to process billing reports in a modern data architecture where data can be queried in a data warehouse and data lake.

1. The data starts in transactional databases where a series of ingestion applications, placed next to the databases, send the data as it is generated to Amazon Data Firehose.
2. AWS Cloud9 is a cloud-based integrated development environment (IDE). It can be used to write, run, and debug code with just a browser. In this solution, it is used to run a mock data generator script.
3. Firehose captures, transforms, and delivers the streaming data to an Amazon S3 data lake. Firehose transforms the captured JSON data into the Parquet format to optimize query performance and storage.
4. Amazon S3 is used for long-term storage. Lifecycle rules and storage tiers can be used to optimize cost. Recent data can be accessed through Amazon Athena and Amazon Redshift Spectrum. 
5. Amazon S3 is used for long-term storage. Lifecycle rules and storage tiers can be used to optimize cost. Recent data can be accessed through Amazon Athena and Amazon Redshift Spectrum. 
6. The Data Catalog is a central repository that can store structural and operational metadata for all data assets.
7. Redshift Spectrum is a feature of Amazon Redshift that can be used to run queries against exabytes of unstructured data in Amazon S3. When a query is issued, it goes to the Amazon Redshift SQL endpoint, which generates and optimizes a query plan.






