# Hosting an HTML Website

The first task,challenge your learning in hosting an HTML website on a single EC2 instance in the default VPC.This repository contains a script for setting up an Apache HTTP server with the Project techmax web application from Amazon S3

## Prerequisites

Before running the script, ensure that you have the following:

- AWS and GitHub accounts
- Root access or sudo privileges on the target system

## Objectives

1. Choose your region
2. Create security groups
3. Create IAM role
4. Create an Amazon S3 bucket
5. Upload the web files to the S3 bucket
6. Write your script
7. Add your script and launch your Amazon EC2 instance
8. Launch your HTML website using your instance's public IPv4 address.
9. Conclusion and clean up

## Task 1

1. Create security groups with ports 80 and 22 opened.
2. Create IAM role with S3FullAccess
3. Create an amazon S3 bucket and attach the role you just created
4. Download the techmax.zip file and upload it on your S3 bucket
5. Create a script that downloads the web files from the S3 bucket and hosts the HTML website on an EC2 instance. Refer to the sample script provided below.

   ```shell
   #!/bin/bash
   sudo su
   yum update -y
   yum install -y httpd
   cd /var/www/html
   aws s3 sync s3://techmax-project /var/www/html
   unzip techmax.zip
   cp -r /var/www/html/techmax/* /var/www/html
   rm -rf techmax.zip techmax
   systemctl enable httpd
   systemctl start httpd
   ```

6. Launch your EC2 instance and add the script to the user data.
   - Use Amazon Linux 2 AMI
   - Use the default VPC
   - Use the security groups you created

7. After the script completes successfully,launch the HTML website using the public IPv4 address of your EC2 instance.
8. You should get the website below.

![Alt text](/ec2-s3-host.png)