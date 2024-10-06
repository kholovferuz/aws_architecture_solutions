**<h3><p align="center">Collaboration with a data mesh</p></h3>**

**Solution Request**

As a leading reference in healthcare technology, the hospital has been asked by the Ministry of Health to build a data collaboration environment that connects the central and regional government health agencies, insurers, academic medical centers, and various care providers. The Ministry of Health wants a decentralized data architecture in which each data producer has the freedom to process data as they see fit, creating their own data products.

**Main AWS Services to be used**

- AWS Glue crawlers to populate the Data Catalog.
- AWS Lake Formation data locations and databases.
- granular access on tables in Lake Formation.
- running queries in Amazon Athena to test the granular access.


**Architecture**

![Collaboration with a Data Mesh vpd (1)](https://github.com/user-attachments/assets/17bfeb37-6bcb-4a93-9ef3-5ec458d2a236)

**Explanation of the architecture**

In this solution, a data mesh architecture is built using AWS Lake Formation. In a data mesh architecture, each data producer has the freedom to process the data as they see fit. 
<ins> Data mesh </ins> is a pattern for defining how organizations can organize around data domains with a focus on delivering data as a product. Each data domain owns and operates multiple data products with its own data and technology stack, which is independent from others.
Preferably, producer S3 buckets reside in different AWS accounts, but they can be in the same AWS account.

1. A centralized governance layer defines which data mesh participants have access to which data. 
2. Data producers extract and ingest the data they want to their own Amazon Simple Storage Service (Amazon S3) buckets. The producers are free to use the tools and technologies that seem most appropriate to them. 
3. An AWS Glue crawler, located in the central governance account, catalogs the data sent by each data producer, creating tables in different databases according to the type and origin of the data. Metadata, found by the AWS Glue crawler, is catalogued in the AWS Glue Data Catalog, which also resides in the central governance account. 
4. AWS Lake Formation is configured in the governance account to set data permissions according to rules defined by the Ministry of Health. The security rules defined for the data access are at the cell level; that is, access is at the level of columns and of rows (row filtering) in a database table.
5. Different IAM roles were created to access the data in a centralized data catalog by various departments in the Ministry of Health and Regional health agency.
6. Amazon Athena is used as the default service for queries, using standard SQL, while Amazon S3 is used as the decentralized storage option.

Preferably, the various data consumers use their own AWS accounts to access the data, respecting the rules defined in Lake Formation. 


