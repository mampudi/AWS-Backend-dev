# AWS-Backend-dev
## What is Amazon S3
* Simple Storage Service - Launched in 2006 as AWS first service
* Focused on General Object Storage on the Cloud
* Big files, small files, media content, source code, spreadsheets etc
* Scalable, Highly Available, Durable, Supports integration with AWS
* Useful in a variety of contexts
  * Website Hosting
  * Database Backups
  * Data Processing Pipelines

## Core Concepts

* Buckets: container of objects you want to store within a particular namespace
  * It needs to have a globally unique name 
  * Think of it as a file system, the bucket itself is a top folder
* Objects: the contents you are storing inside your buckets
  * e.g media content, json files, sdk's, jar, zip files etc
  * The maximum size is 5 TB

## Access
* Access content via URL
  * http://s3.amazaonaws.com/<BUCKET_NAME>/<OBJECT_NAME>
  * This will only work if your S3 bucket is publicly exposed
* Programmatically
```
s3Client = boto3.client('s3');
myObject = s3Client.get_object(Bucket='BUCKET_NAME', key='OBJECT_NAME')
```

* AWS CONSOLE

## S3 Storage Classes
* Storage classes allow you to reduce costs, but with certain sacrifices
* Examples
  * Standard - excellent availability, latency and high throughput to buckets and objects
  * Intelligent - can shuffle around your data based on how you are accessing it
  * Infrequent Access - For older objects that you access infrequently 
  * Glacier - Suited to an archiving use case (reduced cost but delay in accessing the data)
  * Deep Glacier - Objects that you keep around long term due to compliance
* Each tier has different pricing, latency and availability guarantees 
* Standard Tier (Hot Data) -> Infrequent Access -> Glacier (Cold Data)
* Lifecycle Rule automate the data movement process
  * You can specify after and object get uploaded how long it can stay in a specific tier
  * You can configure these on an bucket or object level

## S3 Security
* Public access is blocked by default
* Data Protection - Highly durable and availability guarantees, encryption in transit and at rest
* Access - Access and resourced based controls with AWS IAM
* Auditing - Access logs, action based logs and alarms
* Infrastructure security - Built on top of AWS Cloud Infrastructure

## More than just storage
* Data Ingestion Pipeline (stock market data) -> Amazon Kinesis Data Firehose -> S3 -> Lambda
  * S3 Events
    * Created 
    * Modified
    * Deleted
    * Replicated
* Analytics and Dashboarding
  * Use Amazon Athena (ananlytics service) - Do sql style queries on the data within your bucket
  * Use Amazon QuickSite for dashboards
* Event Driven Architectures
  * Customer -> S3 -> Lambda -> AWS AppSync -> Customer

## Pricing
* Dependent on Storage Class
* 3 main factors
  * Storage
  * Access (GET, POST etc)
  * Transfer
* 100GB of Storage, 10k PUT Request, 10k Read Requests
  * Standard Tier - $6.76 / month
  * Infrequent Access Tier - $6.26 / month
  * Glacier Tier - $5.64 / Month
  * Free Tier - 5 GB (Standard Tier), 20k Get, 2k Put