## Project Work: Deploying and managing a WordPress website using AWS.

### Purpose
> In this project work, you will deploy and manage a WordPress website using Amazon Web Services (AWS). You will utilize AWS services to create a reliable and efficient infrastructure for hosting and managing the WordPress site. 

***Note: if you wish, you may do the following tasks using Amazon Beanstalk.*** 

### Materials
***Step-by-step guide for student***
You will need to set up the following software stack for hosting a WordPress website. 
 - **Web Server (Apache)**: A web server is essential for serving the WordPress files and handling incoming HTTP requests from users' browsers. You are required to install Apache Web Server. 
 - **Database Server (MySQL or MariaDB)**: WordPress requires a database to store content, settings, user data, and more. MySQL or MariaDB is commonly used as the database server to manage this data.
- **PHP**: PHP is a scripting language used by WordPress to generate dynamic content and interact with the database. It's essential for running the WordPress application.

***These components together form the LAMP (Linux, Apache, MySQL, PHP) which provides the foundation for hosting WordPress.***

**You are required to implement the following services:**

### Amazon EC2 Instance for hosting 
Create an Amazon EC2 instance to host the WordPress application. You can choose Amazon Linux, Ubuntu, or other compatible AMIs. You need to install a web server that has support for php on the Amazon EC2 instance to host your WordPress application. You are required to open relevant ports and allow connections to your server so that the WordPress website is available to the public.

### Amazon S3 for Media Storage
You will use Amazon S3 to store and serve media files like images and videos, to reduce the storage load on your EC2 instance and enhance the overall performance. That is, you are required to create an S3 bucket, configure bucker permissions and upload your media files to the S3 bucker. You can upload some random light weight media files (a couple of images). In addition to this, you will need to configure the following for your bucket: 
1. Backup and Data Lifecycle Policies: Implement lifecycle policies to automatically transition media files to cheaper storage classes or delete them when no longer needed. 
2. Implement best practices for optimizing S3 performance and cost efficiency.

### Amazon RDS for WordPress Database
You will set up an Amazon RDS (Relational Database Service) instance to host the WordPress database, ensuring data durability and automatic backups. 

1. Create Amazon RDS service and select your MySQL as your database engine. 

2. Specify DB instance size, storage, and allocated storage type based on your needs.

3. Set a meaningful DB instance identifier and master username/password for database access.
4. Configure VPC, subnet group, and security group settings to control network access.
5. Enable "Automatic backups" to schedule regular automated backups.
6. Connect your WordPress to RDS database by updating your WordPress configuration to use the RDS endpoint, master username, and password.
7. Test and ensure your WordPress can connect to the RDS instance and interact with the database properly. 
8. Check how you can implement automated database snapshots for additional data protection. You are not required to practically implement it.

### Cost Management
Utilize AWS Cost Explorer and Budgets to monitor and manage costs associated with the AWS services you have created above. Please conduct the following tasks: 
1. Estimate the cost of running the above services based on minimal use of your services. 
 2. Define a budget specifying spending limits, time periods, and other criteria.
 3. Configure email or SNS (Simple Notification Service) notifications to receive alerts when budget thresholds are exceeded.
4. Implement cost effective measures based on insights you gain from AWS Cost Explorer to optimize costs, such as resizing instances, terminating unused resources etc. 

### Guidance and feedback
Guidance is available in class during the project consultation session.

### Evaluation
The evaluation is done based on the number of successfully completed tasks. 

### Schedule and timing
Check the deadline in Moodle page.  

### Submission
You will submit a video that includes the result after conducting the whole tasks. In the demonstration, you should include all tasks that you were able to implement that is your simple wordpress site is running that utilizes Amazon services as mentioned above. 

