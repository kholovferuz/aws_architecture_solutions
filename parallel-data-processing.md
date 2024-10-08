**<h3><p align="center"> Parallel Data Processing </p></h3>**

**Solution Request**

The rideshare IT team wants to design and build a backend service to process data in parallel. They want to reward app users who travel more than 2 kilometers during a ride. They have three systems that should process ride information: account, coupons, and promotions services. They want the flexibility to add new systems if they need them. They want something simple to create this integration as fast as possible. Right now, they are using AWS Lambda for all APIs.

**Main AWS Services to be used**

- _Create an_ **Amazon SNS topic**.
- _Subscribe_ a **Lambda function** to the SNS topic.
- _Save ride info_ into a **DynamoDB** table
- **API Gateway** for two-way _real-time communications_


**Architecture**

![Parallel Data Processing-2](https://github.com/user-attachments/assets/7ea33b86-25f6-45f8-a478-6c26b5bf69a9)


**Explanation of the architecture**

In this solution, a backend application receives data through API calls and processes the data in parallel.

  1. The rideshare app sends ride information to the backend APIs. Amazon API Gateway receives the request and redirects it to an AWS Lambda function for processing.
  2. The request is processed by the Lambda function, which saves the data into an Amazon DynamoDB table. This action invokes a message to an Amazon Simple Notification Service (Amazon SNS) topic that contains the fields “coupon” and "distance", which are used for filtering.
  3. A Lambda function for the account service is a subscriber to the SNS topic. The function receives all messages sent to the topic because a filter is not configured.
  4. A Lambda function for the coupon service is a subscriber to the same SNS topic. This subscriber receives only messages that contain the "coupon" attribute.
  5. A Lambda function for the promotion service subscribes to the same SNS topic. This subscriber receives messages that contain the "distance" attribute and a value that is greater than 10.





