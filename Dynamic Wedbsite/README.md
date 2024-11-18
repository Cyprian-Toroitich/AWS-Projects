# Project: Café Website Hosting with AWS EC2 and Cloud9

This project involves hosting a dynamic café website using an EC2 instance with a LAMP stack. The process includes configuring an IDE using AWS Cloud9, deploying the application, and duplicating the environment with an Amazon Machine Image (AMI).

## Table of Contents
- [Overview](#overview)
- [Technologies Used](#technologies-used)
- [Setup and Configuration](#setup-and-configuration)
  - [Task 2: Connecting to the IDE on the EC2 Instance](#task-2-connecting-to-the-ide-on-the-ec2-instance)
  - [Task 3: Analyzing the LAMP Stack Environment and Web Server Accessibility](#task-3-analyzing-the-lamp-stack-environment-and-web-server-accessibility)
  - [Task 4: Installing the Café Application](#task-4-installing-the-café-application)
  - [Task 5: Testing the Web Application](#task-5-testing-the-web-application)
  - [Task 6: Creating an AMI and Launching a New EC2 Instance](#task-6-creating-an-ami-and-launching-a-new-ec2-instance)
  - [Task 7: Verifying the New Café Instance](#task-7-verifying-the-new-café-instance)
- [Summary](#summary)

---

## Overview
This project demonstrates the deployment of a dynamic café website on AWS using a LAMP stack. It covers setting up the environment, testing application functionality, and scaling the setup by creating an AMI.

---

## Technologies Used
- **Amazon EC2**: Hosts the web application.
- **AWS Cloud9**: Integrated Development Environment (IDE).
- **Amazon Linux**: Operating system for the EC2 instance.
- **LAMP Stack**: Linux, Apache, MariaDB, PHP.
- **AWS Systems Manager Parameter Store**: Securely stores application parameters.

---

## Setup and Configuration

### Task 2: Connecting to the IDE on the EC2 Instance
1. Navigate to **AWS Cloud9** in the AWS Management Console.
2. Open the **CafeWebServer** environment.
3. The IDE includes:
   - **Bash terminal**: Available in the bottom-right panel.
   - **File browser**: Displays files in `/home/ec2-user/environment`.
   - **File editor**: Located in the top-right panel.

---

### Task 3: Analyzing the LAMP Stack Environment and Web Server Accessibility
1. Check the operating system version:
   ```bash
   cat /proc/version
