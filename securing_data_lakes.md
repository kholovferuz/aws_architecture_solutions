 **<h3><p align="center"> Securing Data Lakes </p></h3>** 

**Solution Request**

A bank has several departments, each with its own operational databases. These databases use different technologies and do not connect to each other, so each department can only see its own data. To promote a data-driven culture, the bank decided to export data from these operational databases to a data lake on Amazon S3. The employees are now able to access data from all departments, and the bank is able to extract insights from the data lake by using Amazon Athena. The next step is to implement a security layer that restricts access on some sensitive data, such as account and routing numbers. To begin, the bank would like the sensitive data to be hidden from all non-director users. Directors will be able to see all data. The customer would like a solution that implements these security rules directly into the table's metadata catalog.

**Main AWS Services to be used**

  - Create an AWS **Glue crawler** to _ingest data._
  - _Create restrictions_ for **IAM users** with **Lake Formation**.
  - _Test restrictions_ by querying as different IAM users.

**Architecture**

![Securing Data Lakes](https://github.com/user-attachments/assets/fe525f35-6f6a-4577-a6c1-22d12658d722)

**Explanation of the architecture**

1. Internal and external sources deposit data to a company’s data lake hosted in an Amazon Simple Storage Service (Amazon S3) bucket. Much of the data contains personal and sensitive information, which must be secured from unauthorized access.
2. An AWS Glue crawler extracts, transforms, and loads the data into a table within an AWS Glue Data Catalog, which can then be queried by using Amazon Athena.
3. Before the data can be queried, certain columns that contain sensitive information must be restricted from unauthorized users. AWS Lake Formation is used to set these privileges for AWS Identity and Access Management (IAM) users.
4. When an IAM user, who has been restricted from the sensitive data, runs a SQL query on the table in Amazon Athena, no data from restricted columns is included in the returned results.
5. When an IAM user, with no restrictions on sensitive data, runs the same SQL query on the table in Athena, all data is included in the returned results.






