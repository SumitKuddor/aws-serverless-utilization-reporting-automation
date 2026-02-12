# 🚀 AWS Utilization Reporting Automation

**Fully Serverless AWS Automation for EC2 & RDS Utilization Reporting**

This project automates AWS infrastructure monitoring and reporting using **AWS Lambda, Step Functions, CloudWatch, and Amazon S3**.
It generates **daily, weekly, and monthly utilization reports** in **Word & Excel formats**, including **CPU, Memory, Disk, and RDS performance metrics**.

---

## 📌 Features

* 🔍 Automatic **EC2 & RDS Inventory Collection**
* 📊 CloudWatch Metrics Collection

  * **EC2 →** CPU, Memory, Disk
  * **RDS →** CPU, FreeableMemory, DBConnections, ReadIOPS, WriteIOPS
* 📈 Graph Generation using **CloudWatch widgets**
* 📄 Automated **Word (.docx) & Excel (.xlsx) Report Generation**
* ☁️ Report Storage in **Amazon S3**
* 🔁 Orchestration using **AWS Step Functions**
* ⚡ Fully **Serverless Architecture**
* 💰 Low-cost implementation (**~$0.22/month**)

---

## 🏗️ Architecture Overview

### AWS Services Used

* AWS Lambda
* AWS Step Functions
* Amazon CloudWatch
* Amazon S3
* AWS IAM
* Amazon EC2
* Amazon RDS

---

### Workflow Architecture

```
Step Functions
   |
   ├── EC2 Inventory Lambda
   ├── RDS Inventory Lambda
   ├── Inventory Merger Lambda
   ├── Parallel Metrics Collection Lambda
   ├── Metrics Aggregation Lambda
   └── Word & Excel Report Generator Lambda
```

---

## 🔄 Workflow Steps (Step Functions)

| Step | Lambda Function            | Description                        |
| ---- | -------------------------- | ---------------------------------- |
| 1    | ec2-fetch-inventory        | Fetch EC2 inventory                |
| 2    | rds-fetch-inventory        | Fetch RDS inventory                |
| 3    | rds-ec2-spliter            | Combine EC2 & RDS data             |
| 4    | parallel-metrics-functions | Collect CloudWatch metrics         |
| 5    | aggregate-metrics-lambda   | Merge metrics & calculate averages |
| 6    | generate-word-excel-report | Generate Word & Excel reports      |
| 7    | FailState                  | Error handling                     |

---

## 📂 S3 Folder Structure

```
s3://aws-utilization-reports-prod1/
│
├── output/YYYY-MM-DD/
│   ├── ec2_inventory.json
│   └── rds_inventory.json
│
├── images/YYYY-MM-DD/
│   ├── i-xxxx_CPU.png
│   └── db-xxxx_CPU.png
│
└── reports/YYYY-MM-DD/
    ├── aws_report_YYYY-MM-DD.docx
    └── aws_metrics_YYYY-MM-DD.xlsx
```

---

## ⚙️ Prerequisites

* AWS Account
* IAM Admin Access (for initial setup)
* AWS Region: **ap-south-1 (Mumbai)**
* Python **3.12 Runtime**

---

## 🛠️ Tech Stack

**Language:** Python 3.12

**Libraries:**

* boto3
* python-docx
* openpyxl
* matplotlib
* pandas
* pillow

---

## 📦 Lambda Functions Summary

| Lambda                     | Purpose                                    |
| -------------------------- | ------------------------------------------ |
| ec2-fetch-inventory        | Fetch EC2 instance details                 |
| rds-fetch-inventory        | Fetch RDS database details                 |
| rds-ec2-spliter            | Merge EC2 + RDS inventories                |
| parallel-metrics-functions | Fetch CloudWatch metrics & generate graphs |
| aggregate-metrics-lambda   | Combine all metrics                        |
| generate-word-excel-report | Generate Word & Excel reports              |

---

## 🚀 Deployment Steps

### Phase 1 – Preparation

* Create S3 Bucket
* Create IAM Roles
* Enable CloudWatch Agent (EC2)
* Enable RDS Enhanced Monitoring

---

### Phase 2 – Python Lambda Layer

```bash
mkdir lambda-layer && cd lambda-layer
mkdir python && cd python
pip install boto3 python-docx openpyxl matplotlib pandas pillow -t .
cd ..
zip -r aws-utilization-layer.zip python
```

Upload this zip as **Lambda Layer**.

---

### Phase 3 – Lambda Setup

Create **6 Lambda Functions** with:

* Runtime: Python 3.12
* Add Layer
* Set Memory & Timeout accordingly

---

### Phase 4 – Step Functions

* Create State Machine
* Paste workflow JSON
* Assign IAM Role
* Deploy

---

### Phase 5 – Testing

* Trigger Step Function execution
* Verify outputs in S3
* Download Word & Excel reports

---

## 📊 Sample Output

* 📄 **Word Report** → Executive Summary + Graphs
* 📊 **Excel Report** → Average metrics & raw data

---

## 💰 Cost Estimation

| Service        | Monthly Cost      |
| -------------- | ----------------- |
| AWS Lambda     | $0.13             |
| Amazon S3      | $0.05             |
| CloudWatch     | $0.04             |
| Step Functions | $0.00             |
| **Total**      | **$0.22 / month** |

**12-Month Cost:** **$2.64**

---

## 🎯 Use Cases

* AWS Cost Optimization
* Infrastructure Monitoring
* Operations Reporting
* Cloud Governance
* Client Reporting Automation

---

## 👨‍💻 Author

**Sumit Kuddor**
Cloud | AWS | Linux | Automation | DevOps
📍 Mumbai, India

---

⭐ **If you like this project, give it a star!**



