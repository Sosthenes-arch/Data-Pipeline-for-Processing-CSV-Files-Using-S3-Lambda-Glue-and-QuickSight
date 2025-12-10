# Data-Pipeline-for-Processing-CSV-Files-Using-S3-Lambda-Glue-and-QuickSight

This project demonstrates a complete **serverless data pipeline** on AWS for ingesting, preprocessing, transforming, and visualizing CSV data using **Amazon S3, AWS Lambda, AWS Glue, and Amazon QuickSight**.

The pipeline automates data flow from raw ingestion to final insights, ensuring a scalable and cost-efficient workflow suitable for analytics and reporting.

---

## 🚀 Architecture Overview

![Architecture Overview](Data%20Pipeline%20for%20Processing%20CSV%20Files%20Using%20S3,%20Lambda,%20Glue,%20and%20QuickSight.drawio.svg)



The pipeline is built using the following AWS services:

- **Amazon S3** – Storage for raw, processed, and final datasets  
- **IAM** – Secure roles and permissions for all services  
- **AWS Lambda** – Automated preprocessing for uploaded CSV files  
- **AWS Glue** – ETL transformations & schema discovery  
- **Amazon QuickSight** – Dashboarding and data visualization  

---

## 🗂️ 1. S3 Bucket Setup

Three S3 buckets are created to structure the pipeline:

- **Raw Data Bucket** – Stores all incoming CSV files  
- **Processed Data Bucket** – Stores preprocessed output from Lambda  
- **Final Data Bucket** – Stores transformed data from AWS Glue  

All buckets should be created in the **same AWS region** for consistency.

---

## 🔐 2. IAM Configuration

Two IAM roles were created:

### **Lambda Execution Role**
Provides access for Lambda to read/write S3 and interact with AWS Glue.  
Attached permissions include:
- AmazonS3FullAccess  
- AWSGlueServiceRole  

### **Glue Service Role**
Allows AWS Glue to crawl and transform data.  
Attached permissions include:
- AWSGlueServiceRole  
- AmazonS3FullAccess  

A least-privilege model is recommended for production environments.

---

## ⚙️ 3. Amazon QuickSight Setup

QuickSight is configured to visualize processed CSV data:

- A new QuickSight account was created in the same region as S3  
- Required S3 buckets were granted access  
- Default QuickSight-managed role was used  
- Pixel Perfect Reports were disabled  

QuickSight should now be ready to connect to final datasets.

---

## 📥 4. Data Ingestion & Preprocessing

Data ingestion is handled by:

- A **Lambda function** triggered automatically when a CSV file is uploaded to the `raw` S3 bucket  
- An **S3 event notification** (PUT event) forwarding uploads to Lambda  
- Lambda processes the file and stores cleaned output into the processed bucket  

Uploading any new CSV into the raw bucket triggers full preprocessing.

---

## 🔄 5. Data Transformation with AWS Glue

AWS Glue is used for schema discovery and ETL processing.

### **Glue Data Catalog**
- A Glue database named `csv_data_pipeline_catalog` organizes metadata

### **Crawler**
- A crawler scans the processed bucket  
- Discovers schema  
- Creates catalog tables for transformation

### **Visual ETL Job**
- Source: Processed CSV table from the Data Catalog  
- Transformations: Schema changes and column cleanup  
- Target: Final S3 bucket (output stored as compressed CSV)

Final transformed files are extracted, renamed `.csv`, and reuploaded for QuickSight consumption.

---

## 📊 6. Data Visualization with Amazon QuickSight

QuickSight connects to final processed data using:

- A new dataset sourced from S3  
- A manifest configuration referencing the final CSV  
- Visualizations such as bar charts and line charts to analyze trends

Dashboards can be published and shared with stakeholders.

---

## ✅ Final Pipeline Status

Your complete pipeline includes:

- ✔️ Three S3 buckets for clean data flow  
- ✔️ IAM roles enabling secure access  
- ✔️ Automated ingestion and preprocessing through Lambda  
- ✔️ Schema discovery and ETL via Glue  
- ✔️ Data visualization inside QuickSight  
- ✔️ Fully working end-to-end data workflow  

This project successfully demonstrates a production-ready serverless data pipeline for CSV analytics.

---

## 📌 Summary

This hands-on project covered:

- Bucket creation and secure IAM configuration  
- Event-driven preprocessing with Lambda  
- ETL orchestration using AWS Glue Studio  
- Metadata management via Glue Data Catalog  
- Visualization and insights using Amazon QuickSight  

This is how i built a  fully functional cloud-based analytics pipeline leveraging AWS managed services.
