**<h3><p align="center"> Populating the Data Catalog </p></h3>** 

**Solution Request**

A pharmacy chain recently built a data lake on AWS. The pharmacy seeks a solution that will automatically organize the data lake, support schema evolution, and keep a history of changes. 

**Main AWS Services to be used**

  - _Create a database_ in the **AWS Glue Data Catalog.**
  - Create and run **AWS Glue crawler** in the Data Catalog.
  - Use **Amazon Athena** to _query data_ in the table.
  - _Rerun the crawler_ to update the **Data Catalog table**.

**Architecture**

![Populating the Data Catalog](https://github.com/user-attachments/assets/356d7758-61fe-490d-b1c6-2c5a474cec11)

**Explanation of the architecture**
This solution uses AWS Glue to discover and catalog metadata from an Amazon Simple Storage Service (Amazon S3) data lake into a central AWS Glue Data Catalog. Amazon Athena can then directly query the data lake by using the Data Catalog.
  1. The inventory management application, running on an AWS Lambda function, sends new data to the Amazon S3 data lake.
  2. AWS Glue crawlers run periodically to detect the availability of new data as well as changes to existing data, including table definition changes. Crawlers automatically add new tables, new partitions to existing tables, and new versions of table definitions.
  3. After the Data Catalog is updated, you can use Athena to directly query and view the updated data.
  4. In the Data Catalog, you can also change data types and column names, add and remove columns, and then view these changes in Athena.






