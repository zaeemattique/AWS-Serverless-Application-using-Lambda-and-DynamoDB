# AWS-Serverless-Application-using-Lambda-and-DynamoDB

#Serverless Inventory Monitoring System on AWS

This project implements a serverless architecture for managing and monitoring product inventory using AWS services. It automates CSV uploads to an S3 bucket, stores inventory data in DynamoDB, and sends low-inventory alerts via SNS.

#Architecture Overview

**Services Used:**
- **Amazon S3** – Triggers data processing when CSV files are uploaded.
- **AWS Lambda** – 
  - Parses and uploads inventory from S3 to DynamoDB.
  - Monitors low stock and publishes alerts via SNS.
- **Amazon DynamoDB** – Stores inventory data (StoreRegion, Product, ProductCount).
- **Amazon SNS** – Sends notifications for low inventory items.
- **IAM Roles and Policies** – Ensure secure access between services.

#Workflow

1. **CSV File Upload:** User uploads a file (e.g., `inventory.csv`) to the S3 bucket.
2. **Lambda Trigger 1 (`dynamo_db_upload.py`):** 
   - Triggered by the S3 upload.
   - Reads the CSV file.
   - Inserts records into a DynamoDB table.
3. **DynamoDB Stream + Lambda Trigger 2 (`sns_notify.py`):**
   - Monitors changes in the inventory table.
   - Scans for items with stock `≤ 5`.
   - Sends alerts via SNS to subscribed email addresses.

#Sample CSV Format

```csv
StoreRegion,Product,ProductCount
North,Apple,10
South,Orange,3
East,Banana,2

# Deployment Steps (via AWS CLI)
Scripts provided in aws-cli-script.txt will help you:
Create and configure the S3 bucket, DynamoDB table, SNS topic, and IAM roles.
Deploy and connect Lambda functions with event triggers and permissions.

#Notifications
Subscribe an email to the SNS topic. You’ll receive alerts when product stock falls below the threshold.

#Cleanup
Remember to delete:
Lambda functions
S3 bucket
DynamoDB table
SNS topic
IAM roles and policies

Author: Zaeem Attique Ashar
Feel free to connect on LinkedIn 💼
