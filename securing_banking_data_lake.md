**<h3><p align="center"> Securing a Banking Data Lake </p></h3>** 


**Solution Request**

A bank would like to replicate data from their banking systems to a data lake. It’s vital, too, that they can manage data lake permissions, in a centralized way, at the data and metadata level.

**Main AWS Services to be used**

  - Use **Lake Formation blueprints** to _ingest data_ into a data lake.
  - Use **Lake Formation** _to set permissions_ in the data lake.
  - The data from the applications is stored in an **Amazon Aurora MySQL-Compatible Edition**
  - **AWS Glue Connector** _to access the database_

**Architecture**

![Securing a Banking Data Lake](https://github.com/user-attachments/assets/f57379b5-b783-471e-97cb-ca0072266ebe)

**Explanation of the architecture**

This solution uses AWS Lake Formation to create and manage a data lake from multiple data sources within the bank.
  1. The bank has multiple applications, covering deposits, loans, mortgages, and other services. The data from those applications is stored in an Amazon Aurora MySQL-Compatible Edition database.
  2. AWS Lake Formation is a fully managed service that helps you build, secure, and manage data lakes. Lake Formation streamlines and automates many of the complex manual steps that are usually required to create a data lake. These steps include collecting, cleansing, moving, and cataloging data, and then securely making that data available for analytics and machine learning.
  3. An AWS Data Catalog is created and used to house tables of data ingested from the banking applications.
  4. To help automate data ingestion, Lake Formation provides blueprints that create automated workflows. To create the desired workflow, blueprints need only data source, connectivity, and target information.
  5. The workflow in this solution uses an AWS Glue connector to access the databases that contain the needed information.
  6. Ingested data is used to create a set of tables in the Data Catalog and a data lake in Amazon S3.
  7. After the data is ingested and cataloged, Lake Formation can be used to grant granular access permissions to the data, depending on the user.
  8. With those permissions set, users can access the data that they need, without having access to all data in the data lake. User analyst or manager, for example, is granted access to specific data, can use Amazon Athena to perform SQL queries on that data.






