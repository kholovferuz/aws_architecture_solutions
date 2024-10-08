**<h3><p align="center"> Resilience Compliance</p></h3>**

**Solution Request**

A bank has started migrating applications to the cloud, and they would like to update their architecture to ensure that these applications are resilient to failure. They'd also like to increase availability and ensure that data and applications can be restored in the event of a disaster. The solutions architecture must also meet regulatory and compliance obligations.

**Main AWS Services to be used**

- Ensure S3 versioning is enabled.
- Create an AWS Backup plan and assign resources.
- Configure Auto Scaling for dynamic scaling.
- Amazon Textract for text detection and analysis
- DynamoDB to save raw label data from Amazon Textract
- RDS to save processed data for use by other aws services
- Amazon S3 bucket to keep a request image file


**Architecture**

![Resilience Compliance](https://github.com/user-attachments/assets/520797e8-793e-4bfd-845e-de7958d6846d)


**Explanation of the architecture**

This solution uses multiple AWS services to add resilience and fault tolerance to the applications. AWS Backup, for example, centralizes and automates the application’s codes and database.

1. End users upload a loan request image into the application.
2. An application load balancer (ALB) can distribute incoming traffic across multiple targets, such as Amazon Elastic Compute Cloud (EC2) instances across multiple availability zones (AZs). If any individual EC2 instance or AZ suffers degraded performance, the ALB will route requests to healthy targets.
3. AWS Auto Scaling can use scaling plans to configure a set of instructions for scaling resources. To configure Amazon EC2 instances that are launched by the Auto Scaling group, a launch template or launch configuration can be specified. Dynamic scaling creates target-tracking scaling policies for the resources in the scaling plan. These scaling policies adjust resource capacity in response to live changes in resource utilization.
4. The application servers save the raw loan request image to a bucket in Amazon Simple Storage Service (Amazon S3), an object storage service offering industry-leading scalability, data availability, security, and performance.
5. The loan request image is then sent to Amazon Textract for analysis. Amazon Textract, using the same resilient infrastructure as these other AWS services, adds document text detection and analysis to applications.
6. The raw labels received from Amazon Textract are saved in Amazon DynamoDB, a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability.
7. The processed data is then saved in Amazon Relational Database Service (Amazon RDS) for further use by other services. In addition to its AWS global infrastructure, Amazon Aurora, which is part of the Amazon RDS managed database service, offers features to help support data resiliency and backup needs. Aurora Replicas are independent endpoints in an Aurora database (DB) cluster, best used for scaling read operations and increasing availability.
8. AWS Backup is a fully-managed service that helps centralize and automate data protection across AWS services, in the cloud, and on premises.
9. In AWS Backup, a backup vault is a container that stores and organizes backups. AWS Backup Vault Lock is an optional feature that can provide additional security and control over backup vaults.
10. In AWS Backup, a backup plan is a policy expression that defines when and how to back up AWS resources, including, for example, Amazon DynamoDB tables or Amazon Elastic File System (Amazon EFS) file systems.
11. Resource assignment specifies which resources AWS Backup will protect using a backup plan. AWS Backup provides basic default settings and fine-grained controls to assign resources to a backup plan.





