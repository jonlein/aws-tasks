# Amazon Relational Database Service (Amazon RDS)

> Amazon RDS (Relational Database Service) is an AWS-managed database service. It simplifies database administration tasks like provisioning, backups, and scaling for popular relational database engines (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server). RDS offers high availability, security features, automated updates, and monitoring. It's ideal for applications of all sizes, providing a hassle-free database solution in the cloud.

## Practical Task: A (Amazon RDS) Database instance that is connected to Amazon EC2 instance

### Step 1: Create an EC2 Instance 

For your EC2 instance, please allow SSH traffic from anywhere and create a ssh key pair so that you can log in to the EC2 instance. 

***Run the following command to update the software on your EC2 instance and install the Apache web server, PHP, and MariaDB software.***
```
sudo dnf update -y
sudo dnf install -y httpd php php-mysqli
sudo systemctl start httpd
sudo systemctl enable httpd
```

***To enable content management on the Apache Web Server, grant appropriate file permissions to the ec2-user and future apache group members for the Apache document root. This allows them to add, delete, and edit files, facilitating the addition of static websites or PHP applications.***
```
sudo usermod -a -G apache ec2-user
sudo chown -R ec2-user:apache /var/www
sudo chmod 2775 /var/www
find /var/www -type d -exec sudo chmod 2775 {} \;
find /var/www -type f -exec sudo chmod 0664 {} \;
```
### Step 2: Create a MySQL DB Instance

- Select the Engine Type as MySQL 
- Select the engine version MYSQL 8.0.33
- Choose a sample Template as Free Tier
- Give an appropriate name for DB instance identifier. 
- Create a login ID for your DB instance
    - Note Master Username and create your own Master password. 
- Under Connectivity select: Connect to an EC2 compute resource.
    - Select your EC2 instance to which you want to connect. 
- Use the Default VPC
- Select Automatic Setup for DB subnet group. 
- Make sure the public access is No.
- Additional VPC security group : Choose Default
- Create Database. 
- You can ignore the suggested Database addons. 

### Connect your Apache web server to your DB instance

- Connect to your EC2 instance and create a directory named ```inc```. Inside the inc directory, create a file and name it as dbinfo.inc. 

```
cd /var/www
mkdir inc
cd inc
nano conn.inc
```
- The content of the conn.inc is as below. You need to update information in the file to your own DB instance information 
```
<?php

define('DB_SERVER', 'db_instance_endpoint');
define('DB_USERNAME', 'tutorial_user');
define('DB_PASSWORD', 'master password');
define('DB_DATABASE', 'sample');

?>
```               
### Read More
- [Amazon Relational Database Service](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- [MySQL on Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MySQL.html)
- [Install a web server on your EC2 instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Tutorials.WebServerDB.CreateWebServer.html)