A company's legacy application is currently relying on a single-instance Amazon RDS MySQL database without encryption. Due to new compliance requirements, all existing and new data in this database must be encrypted.

How should this be accomplished?

Report Content Errors

A

Create an Amazon S3 bucket with server-side encryption turned on. Move all the data to Amazon S3. Delete the RDS instance.

B

Configure RDS Multi-AZ mode with encryption at rest turned on. Perform a failover to the standby instance to delete the original instance.

C

Take a snapshot of the RDS instance. Create an encrypted copy of the snapshot. Restore the RDS instance from the encrypted snapshot.

D

Create an RDS read replica with encryption at rest turned on. Promote the read replica to primary and switch the application over to the new primary. Delete the old RDS instance.

A user is designing a new service that receives location updates from 3,600 rental cars every hour. The cars upload their location to an Amazon S3 bucket. Each location must be checked for distance from the original rental location.

Which services will process the updates and automatically scale?

Report Content Errors

A

Amazon EC2 and Amazon Elastic Block Store (Amazon EBS)

B

Amazon Data Firehose and Amazon S3

C

Amazon Elastic Container Service (Amazon ECS) and Amazon RDS

D

Amazon S3 events and AWS Lambda

A company wants to deploy an additional Amazon Aurora MySQL DB cluster for development purposes. This cluster will be used several times a week for a few minutes upon request to debug production query issues. The company wants to keep overhead low for this resource.

Which solution meets the company's requirements MOST cost-effectively?

Report Content Errors

A

Purchase a Reserved Instance for the DB instances.

B

Run the DB instances on Aurora Serverless.

C

Create a stop/start schedule for the DB instances.

D

Create an AWS Lambda function to stop DB instances if there are no active connections.

A company built a food ordering application that captures user data and stores it for future analysis. The application's static front-end is deployed on an Amazon EC2 instance. The front-end application sends the requests to the backend application running on a separate EC2 instance. The backend application then stores the data in Amazon RDS.

What should a solutions architect do to decouple the architecture and make it scalable?

Report Content Errors

A

Use Amazon S3 to serve the static front-end application, which sends requests to Amazon EC2 to run the backend application. The backend application will process and store the data in Amazon RDS.

B

Use Amazon S3 to serve the static front-end application and write requests to an Amazon Simple Notification Service (Amazon SNS) topic. Subscribe the backend Amazon EC2 instance HTTP/S endpoint to the topic, and process and store the data in Amazon RDS.

C

Use an EC2 instance to serve the static front-end application and write requests to an Amazon SQS queue. Place the backend instance in an Auto Scaling group, and scale based on the queue depth to process and store the data in Amazon RDS.

D

Use Amazon S3 to serve the static front-end application and send requests to Amazon API Gateway, which writes the requests to an Amazon SQS queue. Place the backend instances in an Auto Scaling group, and scale based on the queue length to process and store the data in Amazon RDS.

A company wants to create an audio version of its product manual. The product manual contains custom product names and abbreviations. The product manual is divided into sections.

Which solution will meet these requirements with the LEAST operational overhead?

Report Content Errors

A

Use Amazon Polly. Build custom lexicons for the product names and abbreviations. Use the StartSpeechSynthesisTask API operation for each section of the product manual.

B

Use Amazon Polly. Build custom Speech Synthesis Markup Language (SSML) for the product names and abbreviations. Use the StartDocumentTextDetection API operation for each section of the product manual.

C

Use Amazon Textract. Build custom Speech Synthesis Markup Language (SSML) for the product names and abbreviations. Use the StartDocumentTextDetection API operation for each section of the product manual.

D

Use Amazon Textract. Build custom lexicons for the product names and abbreviations. Use the StartTranscriptionJob API operation for each section of the product manual.

A solutions architect is designing a new workload in which an AWS Lambda function will access an Amazon DynamoDB table.

What is the MOST secure means of granting the Lambda function access to the DynamoDB table?

Report Content Errors

A

Create an IAM role with the necessary permissions to access the DynamoDB table. Assign the role to the Lambda function.

B

Create a DynamoDB user name and password and give them to the developer to use in the Lambda function.

C

Create an IAM user, and create access and secret keys for the user. Give the user the necessary permissions to access the DynamoDB table. Have the developer use these keys to access the resources.

D

Create an IAM role allowing access from AWS Lambda. Assign the role to the DynamoDB table.

A company is developing a data lake solution in Amazon S3 to analyze large-scale datasets. The solution makes infrequent SQL queries only. In addition, the company wants to minimize infrastructure costs.

Which AWS service should be used to meet these requirements?

Report Content Errors

A

Amazon Athena

B

Amazon Redshift Spectrum

C

Amazon RDS for PostgreSQL

D

Amazon Aurora

A solutions architect is designing a solution that involves orchestrating a series of Amazon Elastic Container Service (Amazon ECS) tasks. The tasks run on an ECS cluster that uses Amazon EC2 instances across multiple Availability Zones. The output and state data for all tasks must be stored. The amount of data that each task outputs is approximately 10 MB, and hundreds of tasks can run at a time. As old outputs are archived and deleted, the storage size will not exceed 1 TB.

Which storage solution should the solutions architect recommend to meet these requirements with the HIGHEST throughput?

Report Content Errors

A

An Amazon DynamoDB table that is accessible by all ECS cluster instances

B

An Amazon Elastic Block Store (Amazon EBS) volume that is mounted to the ECS cluster instances

C

An Amazon Elastic File System (Amazon EFS) file system with Bursting Throughput mode

D

An Amazon Elastic File System (Amazon EFS) file system with Provisioned Throughput mode

An application runs on Amazon EC2 instances in multiple Availability Zones behind an Application Load Balancer. The load balancer is in public subnets. The EC2 instances are in private subnets and must not be accessible from the internet. The EC2 instances must call external services on the internet. Each Availability Zone must be able to call the external services, regardless of the status of the other Availability Zones.

How should these requirements be met?

Report Content Errors

A

Create a NAT gateway attached to the VPC. Add a route to the gateway that connects to each private subnet route table.

B

Configure an internet gateway. Add a route to the gateway that connects to each private subnet route table.

C

Create a NAT instance in the private subnet of each Availability Zone. Update the route tables for each private subnet to direct internet-bound traffic to the NAT instance.

D

Create a NAT gateway in each Availability Zone. Update the route tables for each private subnet to direct internet-bound traffic to the NAT gateway.

A company is using Amazon DynamoDB to stage its product catalog, which is 1 TB in size. A product entry consists of an average of 100 KB of data, and the average traffic is about 250 requests each second. A database administrator has provisioned 3,000 read capacity units (RCUs) of throughput.

However, some products are popular among users. Users are experiencing delays or timeouts because of throttling. The popularity is expected to continue to increase, but the number of products will stay constant.

What should a solutions architect do as a long-term solution to this problem?

Report Content Errors

A

Increase the provisioned throughput to 6,000 RCUs.

B

Use DynamoDB Accelerator (DAX) to maintain the frequently read items.

C

Augment DynamoDB by storing only the key product attributes, with the details stored in Amazon S3.

D

Change the partition key to consist of a hash of the product key and product type instead of just the product key.

An application launched on Amazon EC2 instances needs to publish personally identifiable information (PII) about customers using Amazon Simple Notification Service (Amazon SNS). The application is launched in private subnets within an Amazon VPC.

What is the MOST secure way to allow the application to access service endpoints in the same AWS Region?

Report Content Errors

A

Use an internet gateway.

B

Use AWS PrivateLink.

C

Use a NAT gateway.

D

Use a proxy instance.

An online photo application lets users upload photos and perform image editing operations. The application is built on Amazon EC2 instances and offers two classes of service: free and paid. Photos submitted by paid users are processed before those submitted by free users. Photos are uploaded to Amazon S3 and the job information is sent to Amazon SQS.

Which configuration should a solutions architect recommend?

Report Content Errors

A

Use one SQS FIFO queue. Assign a higher priority to the photos from paid users so they are processed first.

B

Use two SQS FIFO queues: one for paid users and one for free users. Set the free queue to use short polling and the paid queue to use long polling.

C

Use two SQS standard queues: one for paid users and one for free users. Configure the application on the Amazon EC2 instances to prioritize polling for the paid queue over the free queue.

D

Use one SQS standard queue. Set the visibility timeout of the photos from paid users to zero. Configure the application on the Amazon EC2 instances to prioritize visibility settings so photos from paid users are processed first.

A company runs a website on Amazon EC2 instances behind an ELB Application Load Balancer. Amazon Route 53 is used for the DNS. The company wants to set up a backup website with a message including a phone number and email address that users can reach if the primary website is down.

How should the company deploy this solution?

Report Content Errors

A

Use Amazon S3 website hosting for the backup website and a Route 53 failover routing policy.

B

Use Amazon S3 website hosting for the backup website and a Route 53 latency routing policy.

C

Deploy the application in another AWS Region and use ELB health checks for failover routing.

D

Deploy the application in another AWS Region and use server-side redirection on the primary website.

A solutions architect is designing a hybrid application using the AWS Cloud. The network between the on-premises data center and AWS will use an AWS Direct Connect (DX) connection. The application connectivity between AWS and the on-premises data center must be highly resilient.

Which DX configuration should be implemented to meet these requirements?

Report Content Errors

A

Configure a DX connection with a VPN on top of it.

B

Configure a DX connection using the most reliable DX partner.

C

Configure multiple virtual interfaces on top of a DX connection.

D

Configure DX connections at multiple DX locations.

A company wants to measure the effectiveness of its recent marketing campaigns. The company performs batch processing on .csv files of sales data and stores the results in an Amazon S3 bucket once every hour. The S3 bucket contains petabytes of objects. The company runs one-time queries in Amazon Athena to determine which products are most popular on a particular date for a particular region. Queries sometimes fail or take longer than expected to finish running.

Which actions should a solutions architect take to improve the query performance and reliability? (Select TWO.)

Report Content Errors

A

Reduce the S3 object sizes to less than 128 MB.

B

Partition the data by date and region in Amazon S3.

C

Store the files as large, single objects in Amazon S3.

D

Use Amazon Kinesis Data Analytics to run the queries as part of the batch processing operation.

E

Use an AWS Glue extract, transform, and load (ETL) process to convert the .csv files into Apache Parquet format.

Review & Finalize Section

Question

A company is using AWS Site-to-Site VPN connections for secure connectivity to its AWS Cloud resources from on-premises locations. Due to an increase in traffic across the VPN connections to the Amazon EC2 instances, users are experiencing slower VPN connectivity. The network team reports that the internet connection used for the VPN has additional unused throughput.

Which solution will improve the VPN throughput?

Report Content Errors

A

Implement multiple customer gateways for the same network.

B

Configure a virtual private gateway with equal cost multipath routing and multiple channels.

C

Use a transit gateway with equal cost multipath routing and add additional VPN tunnels.

D

Increase the number of tunnels in the VPN configuration.

A restaurant reservation application needs to access a waiting list. When a customer tries to reserve a table, and none are available, the customer application will put the user on the waiting list, and the application will notify the customer when a table becomes free. The waiting list must preserve the order in which customers were added to the waiting list.

Which service should the solutions architect recommend to store this waiting list?

Report Content Errors

A

Amazon Simple Notification Service (Amazon SNS)

B

AWS Step Functions invoking AWS Lambda functions

C

A FIFO queue in Amazon Simple Queue Service (Amazon SQS)

D

A standard queue in Amazon Simple Queue Service (Amazon SQS)

A database architect is designing an online gaming application that uses a simple, unstructured data format. The database must have the ability to store user information and to track the progress of each user. The database must have the ability to scale to millions of users throughout the week.

Which database service will meet these requirements with the LEAST amount of operational support?

Report Content Errors

A

Amazon RDS Multi-AZ

B

Amazon Neptune

C

Amazon DynamoDB

D

Amazon Aurora

An application team has started using Amazon EMR to run batch jobs, using datasets located in Amazon S3. During the initial testing of the workload, a solutions architect notices that the account is starting to accrue NAT gateway data processing costs.

How can the team optimize the cost of the workload?

Report Content Errors

A

Detach the NAT gateway from the subnet where the Amazon EMR clusters are running.

B

Replace the NAT gateway with a customer gateway.

C

Replace the NAT gateway with an S3 VPC endpoint.

D

Configure a network ACL on the subnets where the Amazon EMR clusters are running to open access to Amazon S3.

A solutions architect is designing a secure cloud-based application that uses Amazon EC2 instances within a VPC. The application uses other supported AWS services within the same Region. The network traffic between the instances and AWS services must remain private and must not travel across the public internet.

Which service or resource will meet the security requirement with the MOST operational efficiency?

Report Content Errors

A

Internet gateway

B

NAT gateway

C

VPC endpoint

D

AWS Direct Connect

A solutions architect is responsible for a new highly available three-tier architecture on AWS. An Application Load Balancer distributes traffic to two different Availability Zones with an auto scaling group that consists of Amazon EC2 instances and a Multi-AZ Amazon RDS DB instance. The solutions architect must recommend a multi-Region recovery plan with a recovery time objective (RTO) of 30 minutes. Because of budget constraints, the solutions architect cannot recommend a plan that replicates the entire architecture. The recovery plan should not use the secondary Region unless necessary.

Which disaster recovery strategy will meet these requirements?

Report Content Errors

A

Backup and restore

B

Multi-site active/active

C

Pilot light

D

Warm standby

A company has an application running as a service in Amazon Elastic Container Service (Amazon ECS) using the Amazon EC2 launch type. The application code makes AWS API calls to publish messages to Amazon Simple Queue Service (Amazon SQS).

What is the MOST secure method of giving the application permission to publish messages to Amazon SQS?

Report Content Errors

A

Use AWS Identity and Access Management (IAM) to grant SQS permissions to the role used by the launch configuration for the Auto Scaling group of the ECS cluster.

B

Create a new IAM user with SQS permissions. Then update the task definition to declare the access key ID and secret access key as environment variables.

C

Create a new IAM role with SQS permissions. Then update the task definition to use this role for the task role setting.

D

Update the security group used by the ECS cluster to allow access to Amazon SQS.

A company's website receives 50,000 requests each second. The company wants to use multiple applications to analyze the navigation patterns of the website users so that the experience can be personalized.

Which AWS service or feature should a solutions architect use to collect page clicks for the website and process them sequentially for each user?

Report Content Errors

A

Amazon Kinesis Data Streams

B

Amazon Simple Queue Service (Amazon SQS) standard queue

C

Amazon Simple Queue Service (Amazon SQS) FIFO queue

D

AWS CloudTrail

During a review of business applications, a solutions architect identifies a critical application with a relational database that was built by a business user and is running on the user's desktop. To reduce the risk of a business interruption, the solutions architect wants to migrate the application to a highly available, multi-tiered solution in AWS.

What should the solutions architect do to accomplish this with the LEAST amount of disruption to the business?

Report Content Errors

A

Create an import package of the application code for upload to AWS Lambda, and include a function to create another Lambda function to migrate data into an Amazon RDS database.

B

Create an image of the user's desktop and migrate it to Amazon EC2 using VM Import. Place the EC2 instance in an Auto Scaling group.

C

Pre-stage new Amazon EC2 instances running the application code on AWS behind an Application Load Balancer and an Amazon RDS Multi-AZ DB instance.

D

Use AWS Database Migration Service (AWS DMS) to migrate the backend database to an Amazon RDS Multi-AZ DB instance. Migrate the application code to AWS Elastic Beanstalk.

A company is planning to use Amazon S3 to store images uploaded by its users. The images must be encrypted at rest in Amazon S3. The company does not want to spend time managing and rotating the keys, but it does want to control who can access those keys.

What should a solutions architect use to accomplish this?

Report Content Errors

A

Server-Side Encryption with encryption keys stored in an S3 bucket

B

Server-Side Encryption with Customer-Provided Keys (SSE-C)

C

Server-Side Encryption with encryption keys stored in AWS Systems Manager Parameter Store

D

Server-Side Encryption with AWS KMS-Managed Keys (SSE-KMS)

A solutions architect needs to allow developers to have SSH connectivity to web servers. The requirements are as follows:

* Limit access to users originating from the corporate network.  
* Web servers cannot have SSH access directly from the internet.  
* Web servers reside in a private subnet.

Which combination of steps must the architect complete to meet these requirements? (Select TWO.)

Report Content Errors

A

Create a bastion host that authenticates users against the corporate directory.

B

Create a bastion host with security group rules that only allow traffic from the corporate network.

C

Attach an IAM role to the bastion host with relevant permissions.

D

Configure the web servers' security group to allow SSH traffic from a bastion host.

E

Deny all SSH traffic from the corporate network in the inbound network ACL.

An application running in a private subnet accesses an Amazon DynamoDB table. The data cannot leave the AWS network to meet security requirements.

How should this requirement be met?

Report Content Errors

A

Configure a network ACL on DynamoDB to limit traffic to the private subnet.

B

Enable DynamoDB encryption at rest using an AWS Key Management Service (AWS KMS) key.

C

Add a NAT gateway and configure the route table on the private subnet.

D

Create a VPC endpoint for DynamoDB and configure the endpoint policy.

A company is using Amazon DynamoDB with provisioned throughput for the inventory database tier of its ecommerce website. During flash sales, customers experience periods of time when the database cannot handle the high number of transactions taking place. This causes the company to lose transactions. During normal periods, the database performs appropriately.

Which solution solves the performance problem the company faces?

Report Content Errors

A

Switch DynamoDB to on-demand mode during flash sales.

B

Implement DynamoDB Accelerator (DAX).

C

Use Amazon Kinesis to queue transactions for processing to DynamoDB.

D

Use Amazon Simple Queue Service (Amazon SQS) to queue transactions to DynamoDB.

A company hosts a popular web application. The web application connects to a database running in a private VPC subnet. The web servers must be accessible only to customers on an SSL connection. The Amazon RDS for MySQL database server must be accessible only from the web servers.

How should a solutions architect design a solution to meet the requirements without impacting running applications?

Report Content Errors

A

Create a network ACL on the web server's subnet, and allow HTTPS inbound and MySQL outbound. Place both database and web servers on the same subnet.

B

Open an HTTPS port on the security group for web servers and set the source to 0.0.0.0/0. Open the MySQL port on the database security group and attach it to the MySQL instance. Set the source to web server security group.

C

Create a network ACL on the web server's subnet; allow HTTPS inbound, and specify the source as 0.0.0.0/0. Create a network ACL on a database subnet, allow MySQL port inbound for web servers, and deny all outbound traffic.

D

Open the MySQL port on the security group for web servers and set the source to 0.0.0.0/0. Open the HTTPS port on the database security group and attach it to the MySQL instance. Set the source to web server security group.

A team has an application that detects when new objects are uploaded into an Amazon S3 bucket. The uploads invoke an AWS Lambda function to write object metadata into an Amazon DynamoDB table and an Amazon RDS for PostgreSQL database.

Which action should the team take to ensure high availability?

Report Content Errors

A

Enable Cross-Region Replication in the S3 bucket.

B

Create a Lambda function for each Availability Zone the application is deployed in.

C

Enable Multi-AZ on the RDS for PostgreSQL database.

D

Create a DynamoDB stream for the DynamoDB table.

A company has decided to use AWS to achieve high availability. The company's architecture consists of an Application Load Balancer in front of an Auto Scaling group that consists of Amazon EC2 instances. The company uses Amazon CloudWatch metrics and alarms to monitor the architecture. A solutions architect notices that the company is not able to launch some instances. The solutions architect finds the following message: EC2 QUOTA EXCEEDED.

How can the solutions architect ensure that the company is able to launch all the EC2 instances correctly?

Report Content Errors

A

Modify the Auto Scaling group to raise the maximum number of instances that the company can launch.

B

Use Service Quotas to request an increase to the number of EC2 instances that the company can launch.

C

Recreate the Auto Scaling group to ensure the Auto Scaling group is connected to the Application Load Balancer.

D

Modify the CloudWatch metric that the company monitors to launch the instances.

A company runs an online media site, hosted on-premises. An employee posted a product review that contained videos and pictures. The review went viral, and the company needs to handle the resulting spike in website traffic.

What action would provide an immediate solution?

Report Content Errors

A

Redesign the website to use Amazon API Gateway, and use AWS Lambda to deliver content.

B

Add server instances using Amazon EC2 and use Amazon Route 53 with a failover routing policy.

C

Serve the images and videos using an Amazon CloudFront distribution created using the media site as the origin.

D

Use Amazon ElastiCache for Redis for caching and reducing the load requests from the origin.

A company is planning to use a third-party service for application analytics. A solutions architect sets up a VPC peering connection between the company's VPC on AWS and the third-party analytics provider's VPC on AWS.

Which additional step should the solutions architect take so that network traffic can flow between the two VPCs?

Report Content Errors

A

Resolve any overlapping CIDR ranges.

B

Configure the route tables for both VPCs.

C

Verify that neither VPC has additional peering connections.

D

Verify that internet gateways are attached to each VPC.

Cost Explorer is showing charges higher than expected for Amazon Elastic Block Store (Amazon EBS) volumes connected to application servers in a production account. A significant portion of the charges from Amazon EBS are from volumes that were created as Provisioned IOPS SSD (io2) volume types. Controlling costs is the highest priority for this application.

Which steps should the user take to analyze and reduce the EBS costs without incurring any application downtime? (Select TWO.)

Report Content Errors

A

Use the Amazon EC2 ModifyInstanceAttribute action to enable EBS optimization on the application server instances.

B

Use the Amazon CloudWatch GetMetricData action to evaluate the read/write operations and read/write bytes of each volume.

C

Use the Amazon EC2 ModifyVolume action to reduce the size of the underutilized io2 volumes.

D

Use the Amazon EC2 ModifyVolume action to change the volume type of the underutilized io2 volumes to General Purpose SSD (gp3).

E

Use an Amazon S3 PutBucketPolicy action to migrate existing volume snapshots to Amazon S3 Glacier Flexible Retrieval.

A company hosts its website on AWS. To address the highly variable demand, the company has implemented Amazon EC2 Auto Scaling. Management is concerned that the company is over-provisioning its infrastructure, especially at the front end of the three-tier application. A solutions architect needs to ensure costs are optimized without impacting performance.

What should the solutions architect do to accomplish this?

Report Content Errors

A

Use Auto Scaling with Reserved Instances.

B

Use Auto Scaling with a scheduled scaling policy.

C

Use Auto Scaling with the suspend-resume feature.

D

Use Auto Scaling with a tarA company designs a mobile app for its customers to upload photos to a website. The app needs a secure login with multi-factor authentication (MFA). The company wants to limit the initial build time and the maintenance of the solution.

Which solution should a solutions architect recommend to meet these requirements?

Report Content Errors

A

Use Amazon Cognito Identity with SMS-based MFA.

B

Edit IAM policies to require MFA for all users.

C

Federate IAM against the corporate Active Directory that requires MFA.

D

Use Amazon API Gateway and require server-side encryption (SSE) for photos.

get tracking scaling policy.

Review & Finalize Section

Question

An application provides a feature that allows users to securely download private and personal files. The web server is currently overwhelmed with serving files for download. A solutions architect must find a more effective solution to reduce the web server load and cost, and must allow users to download only their own files.

Which solution meets all requirements?

Report Content Errors

A

Store the files securely on Amazon S3 and have the application generate an Amazon S3 presigned URL for the user to download.

B

Store the files in an encrypted Amazon Elastic Block Store (Amazon EBS) volume, and use a separate set of servers to serve the downloads.

C

Have the application encrypt the files and store them in the local Amazon EC2 instance store prior to serving them up for download.

D

Create an Amazon CloudFront distribution to distribute and cache the files.

A company has a three-tier architecture solution in which an application writes to a relational database. Because of frequent requests, the company wants to cache data whenever the application writes data to the database. The company's priority is to minimize latency for data retrieval and to ensure that data in the cache is never stale.

Which caching strategy should the company use to meet these requirements?

Report Content Errors

A

Amazon ElastiCache with write-through

B

Amazon DynamoDB Accelerator (DAX)

C

Amazon ElastiCache with lazy loading

D

Amazon Simple Queue Service (Amazon SQS)

A company has a three-tier web application on AWS for document storage and retrieval. The application stores documents on a shared NFS volume and references documents by using a Multi-AZ deployment of an Amazon RDS for MySQL DB instance. The document metadata is consulted regularly. The documents are not accessed more than one time a year, but they must remain immediately available. A solutions architect needs to optimize the workload and implement application modifications.

Which solution will meet these requirements MOST cost-effectively?

Report Content Errors

A

Use an Amazon FSx for Lustre shared volume for document storage. Use a Multi-AZ deployment of an RDS for MySQL DB instance to keep document metadata.

B

Use an Amazon S3 bucket with the S3 Glacier Deep Archive storage class for document storage. Use an Amazon DynamoDB table to keep document metadata.

C

Use an Amazon S3 bucket with the S3 Standard-Infrequent Access (S3 Standard-IA) storage class for document storage. Use an Amazon DynamoDB table to keep document metadata.

D

Use an Amazon Elastic File System (Amazon EFS) file system with the EFS Standard-Infrequent Access (EFS Standard-IA) storage class for document storage. Use a Multi-AZ deployment of an RDS for MySQL DB instance to keep document metadata.

A company needs to implement a relational database with a multi-Region disaster recovery Recovery Point Objective (RPO) of 1 second and a Recovery Time Objective (RTO) of 1 minute.

Which AWS solution can achieve this?

Report Content Errors

A

Amazon Aurora Global Database

B

Amazon DynamoDB global tables

C

Amazon RDS for MySQL with Multi-AZ turned on

D

Amazon RDS for MySQL with a cross-Region snapshot copy

A company is reviewing a recent migration of a three-tier application to a VPC. The security team discovers that the principle of least privilege is not being applied to Amazon EC2 security group ingress and egress rules between the application tiers.

What should a solutions architect do to correct this issue?

Report Content Errors

A

Create security group rules using the instance ID as the source or destination.

B

Create security group rules using the security group ID as the source or destination.

C

Create security group rules using the VPC CIDR blocks as the source or destination.

D

Create security group rules using the subnet CIDR blocks as the source or destination.

A development team is deploying a new product on AWS and is using AWS Lambda as part of the deployment. The team allocates 512 MB of memory for one of the Lambda functions. With this memory allocation, the function is completed in 2 minutes. The function runs millions of times monthly, and the development team is concerned about cost. The team conducts tests to see how different Lambda memory allocations affect the cost of the function.

Which steps will reduce the Lambda costs for the product? (Select TWO.)

Report Content Errors

A

Increase the memory allocation for this Lambda function to 1,024 MB if this change causes the run time of each function to be less than 1 minute.

B

Increase the memory allocation for this Lambda function to 1,024 MB if this change causes the run time of each function to be less than 90 seconds.

C

Reduce the memory allocation for this Lambda function to 256 MB if this change causes the run time of each function to be less than 4 minutes.

D

Increase the memory allocation for this Lambda function to 2,048 MB if this change causes the run time of each function to be less than 1 minute.

E

Reduce the memory allocation for this Lambda function to 256 MB if this change causes the run time of each function to be less than 5 minutes.

A company's cloud operations team wants to standardize resource remediation. The company wants to provide a standard set of governance evaluations and remediations to all member accounts in its organization in AWS Organizations.

Which self-managed AWS service can the company use to meet these requirements with the LEAST amount of operational effort?

Report Content Errors

A

AWS Security Hub compliance standards

B

AWS Config conformance packs

C

AWS CloudTrail

D

AWS Trusted Advisor

Question

A company has a web application that makes requests to a backend API service. The API service runs on Amazon EC2 instances accessed behind an Elastic Load Balancer.

Most backend API service endpoint calls finish very quickly, but one endpoint that makes calls to create objects in an external service takes a long time to complete. These long-running calls are causing client timeouts and increasing overall system latency.

What should be done to minimize the system throughput impact of the slow-running endpoint?

Report Content Errors

A

Change the EC2 instance size to increase memory and compute capacity.

B

Use Amazon Simple Queue Service (Amazon SQS) to offload the long-running requests for asynchronous processing by separate workers.

C

Increase the load balancer idle timeout to allow the long-running requests to complete.

D

Use Amazon ElastiCache for Redis to cache responses from the external service.

Question

A company is creating a three-tier web application consisting of a web server, an application server, and a database server. The application will track GPS coordinates of packages as they are being delivered. The application will update the database every 0.5 seconds.

The tracking will need to be read as fast as possible for users to check the status of their packages. Only a few packages might be tracked on some days, whereas millions of packages might be tracked on other days. Tracking will need to be searchable by tracking ID, customer ID, and order ID. Orders older than 1 month no longer need to be tracked.

What should a solutions architect recommend to accomplish this with minimal total cost of ownership?

Report Content Errors

A

Use Amazon DynamoDB. Activate Auto Scaling for the DynamoDB table. Schedule an automatic deletion script for items older than 1 month.

B

Use Amazon DynamoDB with global secondary indexes. Activate Auto Scaling for the DynamoDB table and the global secondary indexes. Turn on TTL for the DynamoDB table.

C

Use an Amazon RDS On-Demand Instance with Provisioned IOPS (PIOPS). Configure Amazon CloudWatch alarms to send notifications when PIOPS are exceeded. Increase and decrease PIOPS as needed.

D

Use an Amazon RDS Reserved Instance with Provisioned IOPS (PIOPS). Configure Amazon CloudWatch alarms to send notifications when PIOPS are exceeded. Increase and decrease PIOPS as needed.

A company runs an application on three very large Amazon EC2 instances in a single Availability Zone in the us-east-1 Region. Multiple 16 TB Amazon Elastic Block Store (Amazon EBS) volumes are attached to each EC2 instance. The operations team uses an AWS Lambda script triggered by a schedule-based Amazon EventBridge rule to stop the instances on evenings and weekends, and start the instances on weekday mornings.

Before deploying the solution, the company used the public AWS pricing documentation to estimate the overall costs of running this data warehouse solution 5 days a week for 10 hours a day. When looking at monthly Cost Explorer charges for this new account, the overall charges are higher than the estimate.

What is the MOST likely cost factor that the company overlooked?

Report Content Errors

A

EC2 data transfer charges between the instances are much higher than expected.

B

EC2 and EBS rates are higher in us-east-1 than most other AWS Regions.

C

The Lambda charges to stop and start the instances are much higher than expected.

D

The company is being billed for the EBS storage on nights and weekends.

A company has implemented one of its microservices on AWS Lambda that accesses an Amazon DynamoDB table named "Books". A solutions architect is designing an IAM policy to be attached to the Lambda function's IAM role giving it access to put, update, and delete items in the "Books" table. The IAM policy must prevent the function from performing any other actions on the "Books" table and any other table.

Which IAM policy would fulfill these needs and provide the LEAST privileged access?

Report Content Errors

A

{

    "Version": "2012-10-17",

    "Statement": \[

        {

  		  "Sid": "PutUpdateDeleteOnBooks",

  		  "Effect": "Allow",

            "Action": \[

  			  "dynamodb:PutItem",

  			  "dynamodb:UpdateItem",

  			  "dynamodb:DeleteItem"

  		  \],

  		  "Resource": "arn:aws:dynamodb:us-west-2:123456789012:table/Books"

  	  }

    \]

}

B

{

    "Version": "2012-10-17",

    "Statement": \[

  	  {

  		  "Sid": "PutUpdateDeleteOnBooks",

  		  "Effect": "Allow",

            "Action": \[

  			  "dynamodb:PutItem",

  			  "dynamodb:UpdateItem",

  			  "dynamodb:DeleteItem"

  		  \],

  		  "Resource": "arn:aws:dynamodb:us-west-2:123456789012:table/\*"

  	  }

    \]

}

C

{

    "Version": "2012-10-17",

    "Statement": \[

  	  {

  		  "Sid": "PutUpdateDeleteOnBooks",

  		  "Effect": "Allow",

  		  "Action": "dynamodb:\*",

  		  "Resource": "arn:aws:dynamodb:us-west-2:123456789012:table/Books"

  	  }

    \]

}

D

{

    "Version": "2012-10-17",

    "Statement": \[

  	  {

  		  "Sid": "PutUpdateDeleteOnBooks",

  		  "Effect": "Allow",

  		  "Action": "dynamodb:\*",

  		  "Resource": "arn:aws:dynamodb:us-west-2:123456789012:table/Books"

  	  },

  	  {

      	  "Sid": "PutUpdateDeleteOnBooks",

  		  "Effect": "Deny",

  		  "Action": "dynamodb:\*:\*",

  		  "Resource": "arn:aws:dynamodb:us-west-2:123456789012:table/Books"

    \]

}

A company is designing a website that will be hosted on Amazon S3.

How should users be prevented from linking directly to the assets in the S3 bucket?

Report Content Errors

A

Create a static website, then update the bucket policy to require users to access the resources with the static website URL.

B

Create an Amazon CloudFront distribution with an origin access control (OAC) and update the bucket policy to grant permission to the OAC only.

C

Create a static website, then configure an Amazon Route 53 record set with an alias pointing to the static website. Provide this URL to users.

D

Create an Amazon CloudFront distribution with an AWS WAF web ACL that permits access to the origin server through the distribution only.

An administrator wants to apply a resource-based policy to the S3 bucket named "iam-policy-testbucket" to restrict access and to allow accounts to only write objects to the bucket. When the administrator tries to apply the following policy to the "iam-policy-testbucket" bucket, the S3 bucket presents an error.

{ "Version": "2012-10-17", "Id": "Policy1646946718956", "Statement": \[ { "Sid": "Stmt1646946717210", "Effect": "Allow", "Action": "s3:PutObject", "Resource": "arn:aws:s3:::iam-policy-testbucket/\*" } \]}

How can the administrator correct the policy to resolve the error and successfully apply the policy?

Report Content Errors

A

Change the Action element from s3:PutObject to s3:\*.

B

Remove the Resource element because it is unnecessary for resource-based policies.

C

Change the Resource element to NotResource.

D

Add a Principal element to the policy to declare which accounts have access.

A company has a well-architected application that streams audio data by using UDP in the AWS Cloud. The company hosts the application in the eu-central-1 Region. The company plans to offer services to North American users. A solutions architect must improve application network performance for the North American users.

Which of the following is the MOST cost-effective solution?

Report Content Errors

A

Create an AWS Global Accelerator standard accelerator with an endpoint group in eu-central-1.

B

Use AWS CloudFormation to deploy additional application infrastructure in the us-east-1 Region and the us-west-1 Region.

C

Create an Amazon CloudFront distribution and use the North America (United States, Mexico, Canada) and Europe and Israel price classes.

D

Configure the application to use an Amazon Route 53 latency-based routing policy.

An environment has an Auto Scaling group across two Availability Zones referred to as AZ-a and AZ-b. AZ-a has four Amazon EC2 instances, and AZ-b has three EC2 instances. The Auto Scaling group uses a default termination policy. None of the instances are protected from a scale-in event.

How will Auto Scaling proceed if there is a scale-in event?

Report Content Errors

A

Auto Scaling selects an instance to terminate randomly.

B

Auto Scaling terminates the instance with the oldest launch configuration of all instances.

C

Auto Scaling selects the Availability Zone with four EC2 instances, and then continues to evaluate.

D

Auto Scaling terminates the instance with the closest next billing hour of all instances.

A solutions architect is redesigning a monolithic application to be a loosely coupled application composed of two microservices: Microservice A and Microservice B.

Microservice A places messages in a main Amazon Simple Queue Service (Amazon SQS) queue for Microservice B to consume. When Microservice B fails to process a message after four retries, the message needs to be removed from the queue and stored for further investigation.

What should the solutions architect do to meet these requirements?

Report Content Errors

A

Create an SQS dead-letter queue. Microservice B adds failed messages to that queue after it receives and fails to process the message four times.

B

Create an SQS dead-letter queue. Configure the main SQS queue to deliver messages to the dead-letter queue after the message has been received four times.

C

Create an SQS queue for failed messages. Microservice A adds failed messages to that queue after Microservice B receives and fails to process the message four times.

D

Create an SQS queue for failed messages. Configure the SQS queue for failed messages to pull messages from the main SQS queue after the original message has been received four times.

A company is building a document storage application on AWS. The application runs on Amazon EC2 instances in multiple Availability Zones. The company requires the document store to be highly available. The documents need to be available to all EC2 instances hosting the application and returned immediately when requested multiple times per month. The lead engineer has configured the application to use Amazon Elastic Block Store (Amazon EBS) to store the documents, but is willing to consider other options to meet the availability requirement.

What should a solutions architect recommend?

Report Content Errors

A

Snapshot the EBS volumes regularly and build new volumes using those snapshots in additional Availability Zones.

B

Use Amazon EBS for the EC2 instance root volumes. Configure the application to build the document store on Amazon S3 Standard.

C

Use Amazon EBS for the EC2 instance root volumes. Configure the application to build the document store on Amazon S3 Glacier Flexible Retrieval.

D

Use at least three Provisioned IOPS EBS volumes for EC2 instances. Mount the volumes to the EC2 instances in a RAID 5 configuration.

A media company has an application that tracks user clicks on its websites and performs analytics to provide near-real-time recommendations. The application has a fleet of Amazon EC2 instances that receive data from the websites and send the data to an Amazon RDS DB instance for long-term retention. Another fleet of EC2 instances hosts the portion of the application that is continuously checking changes in the database and running SQL queries to provide recommendations.

Management has requested a redesign to decouple the infrastructure. The solution must ensure that data analysts are writing SQL to analyze the new data only. No data can be lost during the deployment.

What should a solutions architect recommend to meet these requirements and to provide the FASTEST access to the user activity?

Report Content Errors

A

Use Amazon Kinesis Data Streams to capture the data from the websites, Kinesis Data Firehose to persist the data on Amazon S3, and Amazon Athena to query the data.

B

Use Amazon Kinesis Data Streams to capture the data from the websites, Kinesis Data Analytics to query the data, and Kinesis Data Firehose to persist the data on Amazon S3.

C

Use Amazon Simple Queue Service (Amazon SQS) to capture the data from the websites, keep the fleet of EC2 instances, and change to a bigger instance type in the Auto Scaling group configuration.

D

Use Amazon Simple Notification Service (Amazon SNS) to receive data from the websites and proxy the messages to AWS Lambda functions that run the queries and persist the data. Change Amazon RDS to Amazon Aurora Serverless to persist the data.

A web application runs on Amazon EC2 instances behind an Application Load Balancer (ALB). The application allows users to create custom reports of historical weather data. Generating a report can take up to 5 minutes. These long-running requests use many of the available incoming connections, making the system unresponsive to other users.

How can a solutions architect make the system more responsive?

Report Content Errors

A

Use Amazon SQS with AWS Lambda to generate reports.

B

Increase the idle timeout on the ALB to 5 minutes.

C

Update the client-side application code to increase its request timeout to 5 minutes.

D

Publish the reports to Amazon S3 and use Amazon CloudFront for downloading to the user.

A company currently operates a web application backed by an Amazon RDS MySQL database. It has automated backups that run daily and are not encrypted. A security audit requires future backups to be encrypted and the unencrypted backups to be destroyed. The company will make at least one encrypted backup before destroying the old backups.

What should be done to set up encryption for future backups?

Report Content Errors

A

Turn on default encryption for the Amazon S3 bucket where backups are stored.

B

Modify the backup section of the database configuration to toggle the Enable encryption check box.

C

Create a snapshot of the database. Copy it to an encrypted snapshot. Restore the database from the encrypted snapshot.

D

Configure an encrypted read replica on RDS for MySQL. Promote the encrypted read replica to primary. Remove the original database instance.

A company stops a cluster of Amazon EC2 instances over a weekend. The costs decrease, but they do not drop to zero.

Which resources could still be generating costs? (Select TWO.)

Report Content Errors

A

Elastic IP addresses

B

Data transfer out

C

Regional data transfers

D

Amazon Elastic Block Store (Amazon EBS) volumes

E

AWS Auto Scaling

A solutions architect at an ecommerce company wants to store application log data using Amazon S3. The solutions architect is unsure how frequently the logs will be accessed or which logs will be accessed the most. The company wants to keep costs as low as possible by using the appropriate S3 storage class.

Which S3 storage class should be implemented to meet these requirements?

Report Content Errors

A

S3 Glacier Flexible Retrieval (formerly S3 Glacier)

B

S3 Intelligent-Tiering

C

S3 Standard-Infrequent Access (S3 Standard-IA)

D

S3 One Zone-Infrequent Access (S3 One Zone-IA)

A company is performing an AWS Well-Architected Framework review of an existing workload deployed on AWS. The review identified a public-facing website running on the same Amazon EC2 instance as a Microsoft Active Directory domain controller that was installed recently to support other AWS services. A solutions architect needs to recommend a new design that would improve the security of the architecture and minimize the administrative demand on IT staff.

What should the solutions architect recommend?

Report Content Errors

A

Use AWS Managed Microsoft AD to create a managed Active Directory. Uninstall Active Directory on the current EC2 instance.

B

Create another EC2 instance in the same subnet and reinstall Active Directory on it. Uninstall Active Directory on the current EC2 instance.

C

Use AWS Directory Service to create an Active Directory connector. Proxy Active Directory requests to the Active Directory domain controller running on the current EC2 instance.

D

Configure AWS IAM Identity Center (AWS Single Sign-On) with Security Assertion Markup Language (SAML) 2.0 federation with the current Active Directory controller. Modify the EC2 instance's security group to deny public access to Active Directory.

A solutions architect is designing a database solution that must support a high rate of random disk reads and writes. It must provide consistent performance, and requires long-term persistence.

Which storage solution meets these requirements?

Report Content Errors

A

An Amazon Elastic Block Store (Amazon EBS) Provisioned IOPS volume

B

An Amazon Elastic Block Store (Amazon EBS) General Purpose volume

C

An Amazon Elastic Block Store (Amazon EBS) magnetic volume

D

An Amazon EC2 instance store

A company wants to create an application that will transmit protected health information (PHI) to thousands of service consumers in different AWS accounts. The application servers will sit in private VPC subnets. The routing for the application must be fault tolerant.

What should be done to meet these requirements?

Report Content Errors

A

Create a VPC endpoint service and grant permissions to specific service consumers to create a connection.

B

Create a virtual private gateway connection between each pair of service provider VPCs and service consumer VPCs.

C

Create an internal Application Load Balancer in the service provider VPC and put application servers behind it.

D

Create a proxy server in the service provider VPC to route requests from service consumers to the application servers.

A solutions architect finds that an Amazon Aurora cluster with On-Demand Instance pricing is being underutilized for a blog application. The application is used only for a few minutes several times each day for reads.

What should a solutions architect do to optimize utilization MOST cost-effectively?

Report Content Errors

A

Turn on Auto Scaling on the original Aurora database.

B

Refactor the blog application to use Aurora parallel query.

C

Convert the original Aurora database to an Aurora global database.

D

Convert the original Aurora database to Amazon Aurora Serverless.

An application running on AWS Lambda requires an API key to access a third-party service. The key must be stored securely with audited access to the Lambda function only.

What is the MOST secure way to store the key?

Report Content Errors

A

As an object in Amazon S3

B

As a secure string in AWS Systems Manager Parameter Store

C

Inside a file on an Amazon EBS volume attached to the Lambda function

D

Inside a secrets file stored on Amazon EFS

A company wants to build an immutable infrastructure for its software applications. The company wants to test the software applications before sending traffic to them. The company seeks an efficient solution that limits the effects of application bugs.

Which combination of steps should a solutions architect recommend? (Select TWO.)

Report Content Errors

A

Use AWS CloudFormation to update the production infrastructure and roll back the stack if the update fails.

B

Apply Amazon Route 53 weighted routing to test the staging environment and gradually increase the traffic as the tests pass.

C

Apply Amazon Route 53 failover routing to test the staging environment and fail over to the production environment if the tests pass.

D

Use AWS CloudFormation with a parameter set to the staging value in a separate environment other than the production environment.

E

Use AWS CloudFormation to deploy the staging environment with a snapshot deletion policy and reuse the resources in the production environment if the tests pass.

A solutions architect is designing an elastic application that will have between 10 and 50 Amazon EC2 concurrent instances running, depending on the load. Each instance must mount storage that will read and write to the same 50 GB folder.

Which storage type meets the requirements?

Report Content Errors

A

Amazon S3

B

Amazon Elastic File System (Amazon EFS)

C

Amazon Elastic Block Store (Amazon EBS) volumes

D

Amazon EC2 instance store

