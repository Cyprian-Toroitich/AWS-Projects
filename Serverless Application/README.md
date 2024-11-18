# Project: Daily Sales Reporting System with AWS Lambda and Amazon SNS

This project involves setting up a daily sales reporting system for a café using AWS services. The system extracts sales data from an RDS database, generates a sales report, and sends it via email to subscribers using SNS. It employs Lambda functions, VPC configuration, and EventBridge for automation.

## Table of Contents
- [Overview](#overview)
- [Technologies Used](#technologies-used)
- [Setup and Configuration](#setup-and-configuration)
  - [Creating the DataExtractor Lambda Function](#creating-the-dataextractor-lambda-function)
  - [Creating the salesAnalysisReport Lambda Function](#creating-the-salesanalysisreport-lambda-function)
  - [Creating an SNS Topic](#creating-an-sns-topic)
  - [Creating an Email Subscription to the SNS Topic](#creating-an-email-subscription-to-the-sns-topic)
  - [Testing the salesAnalysisReport Lambda Function](#testing-the-salesanalysisreport-lambda-function)
  - [Setting Up an Amazon EventBridge Event](#setting-up-an-amazon-eventbridge-event)
- [Summary](#summary)

---

## Overview
This project automates the generation and distribution of sales reports. It integrates AWS Lambda for data extraction and reporting, Amazon SNS for email notifications, and EventBridge for scheduling daily triggers.

---

## Technologies Used
- **AWS Lambda**: For data extraction and report generation.
- **Amazon RDS**: Database for storing café sales data.
- **Amazon SNS**: For distributing the sales report via email.
- **Amazon EventBridge**: For scheduling the daily sales report.
- **Amazon VPC**: Ensures secure communication between services.

---

## Setup and Configuration

### Creating the DataExtractor Lambda Function
1. **Create a Security Group for Lambda**:
   - Name: `LambdaSG`
   - VPC: `Lab VPC`
   - Outbound Rules: Allow all traffic.

2. **Update the Database Security Group**:
   - Add an inbound rule:
     - **Type**: MYSQL/Aurora
     - **Source**: The `LambdaSG` security group.

3. **Create the DataExtractor Lambda Function**:
   - **Function Name**: `salesAnalysisReportDataExtractor`
   - **Runtime**: Python 3.8
   - **Role**: `salesAnalysisReportDERole`
   - **VPC Settings**:
     - VPC: `Lab VPC`
     - Subnets: Private subnet 1 and Private subnet 2
     - Security Group: `LambdaSG`

4. **Configure the Function**:
   - Upload `salesAnalysisReportDataExtractor.zip` as the code.
   - Description: *Lambda function to extract data from database*.
   - Handler: `salesAnalysisReportDataExtractor.lambda_handler`
   - Memory Size: 128 MB
   - Timeout: 30 seconds.

---

### Creating the salesAnalysisReport Lambda Function
1. **Create the salesAnalysisReport Lambda Function**:
   - **Function Name**: `salesAnalysisReport`
   - **Runtime**: Python 3.8
   - **Role**: `salesAnalysisReportRole`

2. **Configure the Function**:
   - Upload `salesAnalysisReport.zip` as the code.
   - Description: *Lambda function to generate and send the daily sales report*.
   - Handler: `salesAnalysisReport.lambda_handler`
   - Memory Size: 128 MB
   - Timeout: 30 seconds.

---

### Creating an SNS Topic
1. **Create a Standard SNS Topic**:
   - Name: `SalesReportTopic`
   - Display Name: *Sales Report Topic*.

2. **Update the salesAnalysisReport Lambda Function**:
   - Add the following environment variable:
     - **Variable Name**: `topicARN`
     - **Variable Value**: The ARN of the SNS topic.

---

### Creating an Email Subscription to the SNS Topic
1. **Create a New Email Subscription**:
   - Topic: `SalesReportTopic`
   - Email Address: Use an accessible email address.

2. **Confirm the Subscription**:
   - Check your email inbox and confirm the subscription.

---

### Testing the salesAnalysisReport Lambda Function
1. **Create a Test Event**:
   - Use the default `hello-world` test event.

2. **Run the Test**:
   - Check your email inbox for the sales report.
   - Troubleshoot using CloudWatch Logs if necessary.

---

### Setting Up an Amazon EventBridge Event
1. **Create a New EventBridge Rule**:
   - Trigger the `salesAnalysisReport` Lambda function daily.
   - Specify a time using a cron expression in UTC.

---

## Summary
This project demonstrates how to automate the generation and distribution of sales reports using AWS Lambda, Amazon RDS, Amazon SNS, and EventBridge. By integrating these services securely within a VPC, the system ensures reliable and scalable daily reporting.
