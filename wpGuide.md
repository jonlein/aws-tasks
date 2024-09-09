## Installing WordPress 

### Step 1: Connect to your EC2 instance and get to the command line

### Step 2: Download WordPress Files

1. Download the Wordpress installation file to your root directory of your website that is (/var/www/html). Use the following command 

```
sudo wget /var/www/html/https://wordpress.org/latest.zip

```

2. Unzip the wordpress file 

```
# install the unzip tool (if you have Amazon Linux)
sudo dnf install -u unzip 

#use the following command to unzip your wordpress file
sudo unzip /var/www/html/latest.zip

```
3. Update the wp-config-sample.php and rename it as wp-config.php (Do this after you have created the database service and a database)

In this file you need to update the hostname (Database endpoint) , database name, username, and password.


### Step 3: Create a Database

1. Create a Database for the wordpress website by utilizing RDS service.  Note down the database name, username, and password you set during this process. You'll need these for the WordPress installation. 

### Step 4: Install WordPress

1. Open a web browser and go to your website's domain (e.g., http://example.com/wordpress.
2. You will see the WordPress installation wizard: (Go through these steps only if you have not configure the wp-config.php above)
   - Select your preferred language and click "Continue."
   - On the next page, you'll be prompted to enter your database information:
     - **Database Name:** Enter the name of the database you created in Step 3.
     - **Username:** Enter the database username.
     - **Password:** Enter the database password.
     - **Database Host:** Usually, you can leave this as "localhost."
   - Click the "Submit" button.
3. WordPress will connect to your database. If the information you provided is correct, you will see a confirmation message.
4. Click the "Run the installation" button.
5. You'll be asked to enter some basic site information:
   - **Site Title:** Enter the name of your website.
   - **Username:** Choose a username for your WordPress admin account.
   - **Password:** Set a secure password for your admin account.
   - **Your Email:** Enter your email address.
   - **Privacy:** Decide whether you want search engines to index your site (you can change this later).
6. Click the "Install WordPress" button.
7. If the installation is successful, you will see a success message. Click the "Log In" button to access your WordPress dashboard.

### Step 5: Log in to Your WordPress Dashboard

1. Enter the username and password you set in Step 4.
2. Log in to your WordPress site and make a simple post. In the same post, you will need to include an image from your s3 bucket. 

