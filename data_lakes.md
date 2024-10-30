**<h3><p align="center"> Data Lakes </p></h3>** 

**Solution Request**

An e-commerce store has a high amount of cart abandonment on a daily basis. They delete these records from their database to save storage space. The IT manager wants to find a cost-effective storage solution for these records that they can directly access to analyze the data.


**Main AWS Services to be used**

  - Use **Amazon S3** as the data lake storage layer.
  - Configure an _event notification_ to invoke a **Lambda function**.
  - Configure Amazon **EventBridge ** to _invoke_ a **Lambda function.**


**Architecture**

![Data Lakes](https://github.com/user-attachments/assets/50608784-5feb-4c84-af43-017d13399c5c)

**Explanation of the architecture**

This solution demonstrates a simplified data lake architecture. It contains a layer for raw data (raw zone), a layer for consumable data (consumption zone), and three distinct applications that ingest, process, and consume the data.

  1. The e-commerce backend application is an AWS Lambda function that ingests data into the raw zone bucket in Amazon Simple Storage Service (Amazon S3).
  2. After the raw data is ingested into the data lake, the processing layer is ready to start transforming the data and sending it to the consumption zone S3 bucket. This bucket contains the transformed data, ready to be consumed.
  3. When the data is ready to be consumed, the promotions application accesses the data directly in the data lake and aggregates it further to provide abandonment data for each customer. This data can be used to identify which product discounts to send to customers.
  





