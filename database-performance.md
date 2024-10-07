**<h3><p align="center"> Database performance </p></h3>** 

**Solution Request**

Database administrators in an insurance company are complaining that they spend too much time with operational tasks, such as patching and managing database infrastructure, instead of innovating for customers. They want a new cloud solution that can ensure the systems are resilient and highly available in case of a disaster. Moreover, the analytics team wants that data performance is not impacted with each read load while constantly running real-time queries and big data analytics. What could be the solution for the problem of the insurance company?

**Main AWS Services to be used**

  - Create an **Amazon RDS** for MySQL instance.
  - Enable **backups** to the database.
  - Enable **multiple AZs** for the Amazon RDS deployment.
  - Create **a read replica** for the customer.


**Architecture**

![Databases in Practice](https://github.com/user-attachments/assets/ed34d7d7-3edf-499d-85cd-98dbcec825f3)

**Explanation of the architecture**

This solution uses Amazon Relational Database Service (Amazon RDS), which is fully managed and removes the need for manual database infrastructure provisioning and maintenance.

  1. Amazon RDS automates backups, database snapshots, and host replacement to reduce the administrative burden.
  2. To achieve high availability, we will deploy databases across multiple Availability Zones (AZs). In a Multi-AZ deployment, Amazon RDS automatically creates a primary DB (database) instance and synchronously replicates the data to an instance in a different AZ.
  3. When it detects a failure, Amazon RDS automatically fails over to a standby instance in a different AZ, without manual intervention. 
  4. For read-heavy database workloads, we can create one or more read-only replicas of a DB instance. This way, we can serve high-volume application read traffic from multiple copies of data, increasing aggregate read throughput.




