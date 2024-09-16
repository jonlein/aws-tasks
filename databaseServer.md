# Module 8: Databases
# Amazon Relational Database Service (Amazon RDS)

> Amazon RDS (Relational Database Service) is an AWS-managed database service. It simplifies database administration tasks like provisioning, backups, and scaling for popular relational database engines (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server). RDS offers high availability, security features, automated updates, and monitoring. It's ideal for applications of all sizes, providing a hassle-free database solution in the cloud.


## Amazon Database Services Overview

Amazon provides a range of managed database services tailored to different needs, from relational databases to NoSQL and in-memory databases. These services help manage and scale database infrastructure without the overhead of manual maintenance.

### Amazon RDS (Relational Database Service)

- **Amazon RDS** provides a managed **relational database service** with support for multiple database engines including MySQL, PostgreSQL, MariaDB, Oracle, and SQL Server.
- **Features**:
  - **Automated Backups**: Daily backups and transaction logs.
  - **Scaling**: Easily scale compute and storage resources.
  - **High Availability**: Multi-AZ deployments for failover support.
  - **Monitoring**: Integrated monitoring and alerting with Amazon CloudWatch.
- **Use Cases**:
  - Web applications
  - E-commerce
  - Enterprise applications
  - Business intelligence

### Amazon Aurora

-  **Amazon Aurora** is a high-performance, highly available, and scalable **relational database** engine that is compatible with MySQL and PostgreSQL.
- **Features**:
  - **Performance**: Up to 5 times faster than standard MySQL and 2 times faster than standard PostgreSQL.
  - **Scalability**: Automatically scales up to 64 TB of storage.
  - **High Availability**: Replication across multiple Availability Zones.
  - **Backup and Restore**: Continuous backups to Amazon S3 with point-in-time recovery.
- **Use Cases**:
  - High-traffic web applications
  - Online transaction processing (OLTP)
  - Enterprise applications

### Amazon DynamoDB

- Amazon DynamoDB is a fully managed **NoSQL database** service that provides fast and predictable performance with seamless scalability.
- **Features**:
  - **Performance**: Single-digit millisecond response times.
  - **Scaling**: Automatically scales throughput capacity and storage.
  - **High Availability**: Multi-AZ replication with automatic failover.
  - **Integrated with AWS Lambda**: Supports triggers and event-driven architectures.
- **Use Cases**:
  - Gaming
  - IoT
  - Mobile applications
  - Real-time analytics
> A NoSQL database service is a type of database that provides a flexible schema and is designed to handle large volumes of unstructured or semi-structured data. NoSQL databases offer various data models, including key-value, document, column-family, and graph formats.
### Amazon Redshift
- **Amazon Redshift** is a fully managed **data warehouse service** that enables you to run complex queries and perform large-scale data analysis.
- **Features**:
  - **Performance**: Columnar storage and parallel query execution.
  - **Scaling**: Easily scale compute and storage resources.
  - **Integration**: Supports integration with various BI tools and data lakes.
  - **Cost-Effective**: Pay only for the resources you use.
- **Use Cases**:
  - Big data analytics
  - Business intelligence
  - Data warehousing
  - Complex queries and reporting

### Amazon ElastiCache

- **Amazon ElastiCache** provides in-memory caching services for Redis and Memcached, enhancing the performance of web applications by reducing database load.
- **Features**:
  - **Performance**: Sub-millisecond response times.
  - **Scalability**: Easily scale up or out with a few clicks.
  - **High Availability**: Replication and automatic failover for Redis.
  - **Integration**: Works seamlessly with Amazon RDS and EC2.
- **Use Cases**:
  - Caching frequently accessed data
  - Session storage
  - Real-time analytics
  - Message brokering

### Amazon DocumentDB

- **Amazon DocumentDB** is a managed document database service that is compatible with MongoDB, providing scalable, highly available, and secure document storage.
- **Features**:
  - **Compatibility**: Supports MongoDB APIs and tools.
  - **Scaling**: Scales up to 64 TiB of storage and up to 15 replicas.
  - **High Availability**: Multi-AZ deployments with automatic failover.
  - **Backup and Restore**: Automated backups to Amazon S3 with point-in-time recovery.
- **Use Cases**:
  - Content management
  - Catalogs
  - User profiles
  - Metadata storage

## Practical Task: Lab - 5 Build a Database Server (Amazon Academy Portal)
## Practical Task: (Amazon RDS) Database,  Amazon EC2 & Amazon Beanstalk

In this task, you will run a simple php page that is running on a web server (EC2 Instance)and utilizes a database from Amazon RDS. 

After completing the first part of the lab, you will run the same app by using Amazon Beanstalk & Amazon RDS. 

### Step 1: Create an EC2 Instance 

For your EC2 instance, please allow SSH traffic from anywhere and create a ssh key pair (if needed) so that you can log in to the EC2 instance. (At this point, you already have key pairs so it is better to use the existing one)

***Run the following command to update the software on your EC2 instance and install the Apache web server, PHP, and MariaDB software.***
```
sudo dnf update -y
sudo dnf install -y httpd php php-mysqli mariadb105
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

# Note: 2 (setgid) ensures that files created in this directory inherit the group ownership of the directory
```
### Step 2: Create a MySQL DB Instance (Amazon RDS)

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

### Connect to your DB instance and create a database that will be used by your app
- You can connect with the following command 
    ```
    mysql -u username -p -h yourDatabaseEndpoint 
    ```
    ***Type your password and press enter.***
- Create a database with the following command 
    ```
    create database dbname; 
    use databasename;
    ```
- Create a simle table that will be used later on

    ```
    CREATE TABLE EMPLOYEES (
         ID int(11) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
         NAME VARCHAR(45),
         ADDRESS VARCHAR(90)
       );
    ```
### Connect your Apache web server to your DB instance

- Connect to your EC2 instance and create a directory named ```inc```. Inside the inc directory, create a file and name it as dbcon.php 

```
cd /var/www
mkdir inc
cd inc
nano dbcon.php
```
- The content of the dbcon.php is as below. You need to update information in the file to your own DB instance information 
```
<?php

define('DB_SERVER', 'db_instance_endpoint');
define('DB_USERNAME', 'db_username');
define('DB_PASSWORD', 'master password');
define('DB_DATABASE', 'databaseName');

?>
```   

### Create a simple php page

> Lets create a simple php page that will the use the above database and save it as **index.php** in **/var/www/html** directory.

```

<?php include "../inc/dbcon.php"; ?>
<html>
<body>
<h1>Sample page</h1>
<?php

  /* Connect to MySQL and select the database. */
  $connection = mysqli_connect(DB_SERVER, DB_USERNAME, DB_PASSWORD);

  if (mysqli_connect_errno()) echo "Failed to connect to MySQL: " . mysqli_connect_error();

  $database = mysqli_select_db($connection, DB_DATABASE);

  /* Ensure that the EMPLOYEES table exists. */
  VerifyEmployeesTable($connection, DB_DATABASE);

  /* If input fields are populated, add a row to the EMPLOYEES table. */
  $employee_name = htmlentities($_POST['NAME']);
  $employee_address = htmlentities($_POST['ADDRESS']);

  if (strlen($employee_name) || strlen($employee_address)) {
    AddEmployee($connection, $employee_name, $employee_address);
  }
?>

<!-- Input form -->
<form action="<?PHP echo $_SERVER['SCRIPT_NAME'] ?>" method="POST">
  <table border="0">
    <tr>
      <td>NAME</td>
      <td>ADDRESS</td>
    </tr>
    <tr>
      <td>
        <input type="text" name="NAME" maxlength="45" size="30" />
      </td>
      <td>
        <input type="text" name="ADDRESS" maxlength="90" size="60" />
      </td>
      <td>
        <input type="submit" value="Add Data" />
      </td>
    </tr>
  </table>
</form>

<!-- Display table data. -->
<table border="1" cellpadding="2" cellspacing="2">
  <tr>
    <td>ID</td>
    <td>NAME</td>
    <td>ADDRESS</td>
  </tr>

<?php

$result = mysqli_query($connection, "SELECT * FROM EMPLOYEES");

while($query_data = mysqli_fetch_row($result)) {
  echo "<tr>";
  echo "<td>",$query_data[0], "</td>",
       "<td>",$query_data[1], "</td>",
       "<td>",$query_data[2], "</td>";
  echo "</tr>";
}
?>

</table>

<!-- Clean up. -->
<?php

  mysqli_free_result($result);
  mysqli_close($connection);

?>

</body>
</html>


<?php

/* Add an employee to the table. */
function AddEmployee($connection, $name, $address) {
   $n = mysqli_real_escape_string($connection, $name);
   $a = mysqli_real_escape_string($connection, $address);

   $query = "INSERT INTO EMPLOYEES (NAME, ADDRESS) VALUES ('$n', '$a');";

   if(!mysqli_query($connection, $query)) echo("<p>Error adding employee data.</p>");
}

/* Check whether the table exists and, if not, create it. */
function VerifyEmployeesTable($connection, $dbName) {
  if(!TableExists("EMPLOYEES", $connection, $dbName))
  {
     $query = "CREATE TABLE EMPLOYEES (
         ID int(11) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
         NAME VARCHAR(45),
         ADDRESS VARCHAR(90)
       )";

     if(!mysqli_query($connection, $query)) echo("<p>Error creating table.</p>");
  }
}

/* Check for the existence of a table. */
function TableExists($tableName, $connection, $dbName) {
  $t = mysqli_real_escape_string($connection, $tableName);
  $d = mysqli_real_escape_string($connection, $dbName);

  $checktable = mysqli_query($connection,
      "SELECT TABLE_NAME FROM information_schema.TABLES WHERE TABLE_NAME = '$t' AND TABLE_SCHEMA = '$d'");

  if(mysqli_num_rows($checktable) > 0) return true;

  return false;
}
?>                        
                
                                      
```
### Check if your page is working 
- Add some data from the form and ensure that it is added to your database table.

### Challenge Task: Run the above php page by utilizing AWS Elastic Beanstalk service. 
 
### Read More
- [Amazon Relational Database Service](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- [MySQL on Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MySQL.html)
- [Install a web server on your EC2 instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Tutorials.WebServerDB.CreateWebServer.html)
