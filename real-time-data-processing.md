**<h3><p align="center"> Real-time data processing</p></h3>** 

**Solution Request**

The city administration wants to improve the efficiency of its wind farm. When a wind generator fails, it takes a long time to identify the fault, send a maintenance team, and carry out the repair. The administration wants to anticipate possible defects in the wind turbines to provide preventive maintenance.

**Main AWS Services to be used**

- Deploy **Kinesis Data Streams** _to ingest data_ from data sources. 
- Create a **Kinesis Data Analytics for Apache Flink** application _to detect anomalies_.
- Write **application output records** to a configured external destination.
- **DynamoDB tables** _to store_ the ingested data and anomalies data.
- **SNS topic** for _sending alert_ to the maintenance team in case of anomaly detection


**Architecture**

![Real-time data processing-2](https://github.com/user-attachments/assets/1d74ac39-7a0b-48fe-b9ed-880f38e7875b)




**Explanation of the architecture**

This solution uses Managed Apache Flink for real-time processing and detection of anomalies in wind speed data for preventive maintenance on a wind farm.

  1. Wind speed sensor data is sent directly to Amazon Kinesis Data Streams, a service that collects and processes large streams of data records in real time.
  2. An Amazon Managed Apache Flink application processes and analyzes the data from Kinesis Data Streams. An Apache Flink application is a Java or Scala application that is created with the Apache Flink framework. 
  3. An AWS Lambda function is set as the external destination in the Kinesis Data Analytics application. The function code takes the processed data and parses it into records in an Amazon DynamoDB table. The data includes the wind farm location, wind speed, and the assigned anomaly score.
  4. A second Lambda function scans the DynamoDB table and filters for anomalies.  For each discovered anomaly, the function publishes a notification message to an Amazon SNS topic.
  5. For each anomaly, subscribers to the SNS topic receive a notification email. In this case, the maintenance team is alerted and dispatched to the wind farm.



