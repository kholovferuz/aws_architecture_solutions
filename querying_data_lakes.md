**<h3><p align="center"> Querying the Data Lake </p></h3>** 

**Solution Request**

A financial institution recently created a data lake to ingest transactions from all across the city. A credit card issuer sends logs of transactions, which are stored in Amazon S3. The financial institution's fraud department wants a fast, scalable solution to analyze these logs for suspicious transactions.


**Main AWS Services to be used**

  -  _Query for suspicious_ credit card transactions.
  -  Ingest CSV-formatted data into an **S3 bucket**.
  -  Create an **Athena table** that contains _transaction data._
  -  Create an **Athena table** that contains only _suspicious transactions._

**Architecture**

![Querying the Data Lake](https://github.com/user-attachments/assets/4a88e607-5244-4ba4-b326-7267ea9fcc2a)

**Explanation of the architecture**


  1. An AWS Lambda function generates credit card transaction data, as a comma-separated values (CSV) file, and saves it to an ingestion bucket in Amazon Simple Storage Service (Amazon S3).
  2. The user runs a SQL query on the file, using Amazon Athena to create a database table that contains the credit card transactions. The query results are saved to an S3 staging bucket.
  3. The user then runs another SQL query, using Athena to search for suspicious transactions. The query creates another table and stores the data in the staging bucket.
  4. Users in the fraud department create SQL queries and run them on the suspicious transactions table in Athena. These query results are also saved to the staging bucket.
  5. After the fraudulent transactions are identified, a SQL query is run to drop the suspicious transactions table.






