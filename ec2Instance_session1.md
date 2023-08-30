# Amazon Elastic Compute Cloud (Amazon EC2) Linux

In this task, you will practically create an Amazon EC2 instance,set up a simple web server,create your own AMI image from an Amazon EC2 instance, create a volume and attach the volume to your EC2 instance. This practical task is based on Lab 3 from the Amazon Cloud Academy with a bit of modification to align with the academic context. 

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

- Type: HTTP
- Source: Anywhere-IPv4

> Check by typing your ipv4 address in the browser, if you can see a simple page. 

### Create an AMI from an Amazon EC2 Instance

You can create a tailored image of a virtual server  that you've created and configured according to your specific requirements like in this task. This custom AMI can include your desired operating system, software packages, configurations, and even your application code.

Creating a custom AMI allows you to capture a snapshot of a particular configuration that you've set up, making it easier to replicate and deploy identical instances with the same setup in the future.

***Follow the guidelines at this link to create your own AMI***

[Link](https://docs.aws.amazon.com/toolkit-for-visual-studio/latest/user-guide/tkv-create-ami-from-instance.html) 

Locate the image that you have created. **Try to launch a new instance** with your own AMI however you won't be able to do it due to the restrictions in the lab environment.

## Create an Amazon EBS (Elastic Block Store) volume 

**Steps:** 
- From the AWS Management Console, get to the EC2 dashboard.
- Under the "Elastic Block Store" section, click on "Volumes" in the left sidebar.
- Click the "Create Volume" button.

- Configure the volume settings, including the volume type, size, availability zone, etc. **Allocate only 1 GB for the volume.** 

> Please note that to attach an Amazon EBS (Elastic Block Store) volume to an Amazon EC2 instance, both the volume and the instance must be in the same availability zone within the same Amazon Web Services (AWS) region. 

- Click the "Create Volume" button.

## Attach the volume to an EC2 instance

Once the volume is created, you need to attach the volume to an EC2 instance. 
**Steps:**
- In the the "Volumes" dashboard, Select the volume you just created.
- Click the "Actions" button and choose "Attach Volume."
- In the "Attach Volume" dialog box, select the EC2 instance you want to attach the volume to. 
- Choose the device name (e.g., /dev/sdf) for the volume on the instance.
- Click the "Attach" button.


## Format and Mount the New Volume

In order to use the volume, you need to format and mount it.
**Steps:**

- Check your newly attached volume by running the following command 

```
lsblk
```
- Run the following command to format the volume with the ext4 file system. Replace /dev/volumename with the actual device name of your volume.

```
sudo mkfs -t ext4 /dev/volumename
```

- Create a directory where you want to mount the volume, for example: 

```
sudo mkdir /mnt/webserver
```

- Mount the volume to the directory
```
sudo mount /dev/volumename /mnt/webserver
```
- Check if the volume is mounted properly 
```
df -h
```
> You are also required to adjust file permissions as per your need once the volume is mounted. 
```
sudo chmod -R permissions /mnt/webserver
sudo chown -R user:group /mnt/webserver
```
## Configure your web server 

Now lets assume that you want to make this new volume as a directory to store web pages. You need to configure your web server. The configuration files for the Apache HTTP Server are typically located in the ```/etc/httpd/``` directory. 

***The main configuration file is /etc/httpd/conf/httpd.conf***

- Edit the file /etc/httpd/conf/httpd.conf You need to open this file as a root user 

```
sudo nano /etc/httpd/conf/httpd.conf
```
Find the **DocumentRoot** directive in the file and replace the document web directory to the newly created volume

DocumentRoot "/mnt/webserver"

- You are also required to update the  the Directory Block. In the same file, you need to update <Directory> to match the new directory that you have set as the DocumentRoot.

- Restart your Web Server
```
sudo systemctl restart httpd
```