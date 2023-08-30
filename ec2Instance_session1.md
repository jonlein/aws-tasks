# Amazon Elastic Compute Cloud (Amazon EC2) Linux

In this task, you will practically create an Amazon EC2 instance,set up a simple web server and create your own AMI image from an Amazon EC2 instance. This practical task is based on Lab 3 from the Amazon Cloud Academy with a bit of modification to align with the academic context. 

You are required to follow the following steps to complete the lab. 

## Launch the Instance

1. Launch ***Lab 3 – Introduction to Amazon EC2*** from **AWS Academy Portal.** 
2. Launch Your Amazon EC2 Instance. (Follow the guidelines as mentioned in the Lab document till Step 13.)
3. In **Step 14**, it asks you to remove the  Inbound security group rules. ```Please do not remove it.``` Let the rule exist as you will make SSH connection to this newly created instance. 
4. Continue to Step 15 as it is and then **launch the instance.** 


## Establish a Connection to Your Instance

1. Use SSH client to connect to your newly created instance. 

> Note, you can connect to each others instances and do the following tasks: 

### Install & start a simple Web Server by running the following commands

```
dnf install -y httpd
systemctl enable httpd
systemctl start httpd

```

### Create a simple html page

You can user nano to create a simple html file and name it as index.html in /var/www/html directory. In the index.html file, you can write your own Name. 

### Update Your Security Group 

You will be proving an access to the Web Server, therefore you are required to add inbound rule as below 

•Type: HTTP
•Source: Anywhere-IPv4

> Check by typing your ipv4 address in the browser, if you can see a simple page. 

### Create an AMI from an Amazon EC2 Instance

You can create a tailored image of a virtual server  that you've created and configured according to your specific requirements like in this task. This custom AMI can include your desired operating system, software packages, configurations, and even your application code.

Creating a custom AMI allows you to capture a snapshot of a particular configuration that you've set up, making it easier to replicate and deploy identical instances with the same setup in the future.

***Follow the guidelines at this link to create your own AMI***

[Link](https://docs.aws.amazon.com/toolkit-for-visual-studio/latest/user-guide/tkv-create-ami-from-instance.html) 

Locate the image that you have created. **Try to launch a new instance** with your own AMI however you won't be able to do it due to the restrictions in the lab environment.


