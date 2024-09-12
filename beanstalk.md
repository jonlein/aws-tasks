# AWS Elastic Beanstalk

## What is AWS Elastic Beanstalk?
- **PAAS**: Elastic Beanstalk is a Platform as a Service (PaaS) that simplifies the process of deploying, managing, and scaling web applications and services
- **Fully managed service**: Elastic Beanstalk manages deployment, monitoring, and scaling of applications automatically.
-  **Pay-as-You-Go Model**: Elastic Beanstalk does not require any upfront commitments or long-term contracts. Pay for what you use and when you use it. **You only pay for the AWS resources consumed**, such as EC2 instances, S3 storage, and load balancers.
---
## Key Features

- **Fast and Simple Application Deployment**: Elastic Beanstalk is designed for rapid deployment of applications, whether you're scaling a small app or a complex service.Upload your code and Beanstalk automatically handles the rest.
- **Load balancing and scaling**: Automatically distributes traffic and scales your application based on demand.
- **Monitoring and health checks**: Built-in integration with CloudWatch for real-time monitoring.
- **Seamless integration**: Works with AWS services like S3, RDS, and CloudFormation.

- **Flexible Upload Options**:
  - **AWS Management Console**: Drag-and-drop functionality to quickly deploy code.
  - **Git Integration**: Directly push code changes from a Git repository.
  - **IDEs (Eclipse, Visual Studio)**: Integrated deployment for streamlined workflows directly from the development environment.
---
## Supported Platforms
- **Web frameworks**: Apache, Nginx, IIS
- **Languages**: Java, Node.js, PHP, Ruby, Python, Go, and .NET.
- **Docker**: Supports containerized applications using Docker images.
---
## Automated Management
- **Automatic Infrastructure Handling**: Elastic Beanstalk automatically manages infrastructure tasks for you, including:
  - **Capacity provisioning**: Allocating resources based on application demand.
  - **Load balancing**: Distributing traffic across multiple servers for optimal performance.
  - **Auto-scaling**: Dynamically adjusting capacity to handle traffic spikes.
  - **Application health monitoring**: Built-in monitoring to track app performance and resource usage, ensuring high availability.
---
## Cost Efficiency
- **No Additional Charge for Elastic Beanstalk Itself**: You don’t pay for Elastic Beanstalk as a service, only for the underlying AWS resources you use (such as EC2 instances, RDS databases, and S3 storage).
- **Optimized for Cost Efficiency**: By leveraging features like auto-scaling and monitoring, Elastic Beanstalk ensures that you only pay for the resources you need, reducing unnecessary costs.
---
## Use Cases
- Web applications and websites.
- API backends.
- Microservices with container support (Docker).
- Rapid development and testing environments.

---

# AWS Elastic Beanstalk vs. AWS Lambda

| Feature                   | AWS Elastic Beanstalk                                  | AWS Lambda                                              |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------|
| **Type of Service**        | PaaS (Platform as a Service)                          | FaaS (Function as a Service)                            |
| **Application Type**       | Long-running web applications                         | Event-driven, short-duration functions                  |
| **Infrastructure**         | Manages EC2 instances, load balancers, and scaling    | Serverless; no need to manage infrastructure            |
| **Scaling**                | Automatic scaling of EC2 instances                    | Automatic scaling of functions based on invocations     |
| **Pricing Model**          | Pay for underlying resources (EC2, RDS, etc.)         | Pay only for the execution time of functions            |
| **Startup Time**           | Slower due to EC2 instance initialization             | Near-instant, on-demand execution                      |
| **Use Case**               | Ideal for traditional web apps, APIs, and microservices | Suitable for microservices, event-driven architectures  |
| **Control**                | More control over infrastructure (EC2, RDS, etc.)     | Less control; focus on code, not infrastructure         |
| **Persistence**            | Supports persistent applications with database access | Stateless, no persistent connections between executions |
| **Integration**            | Works well with other AWS services like S3, RDS, CloudWatch | Deep integration with AWS services like API Gateway, S3, DynamoDB |
---
## Major Differences between AWS Elastic Beanstalk & AWS Lambda
- **AWS Elastic Beanstalk** is ideal for managing traditional web apps and services where you need control over the infrastructure.
- **AWS Lambda** is perfect for event-driven applications and microservices that need to scale instantly without managing infrastructure.

--- 

# Similar services from other providers

- Azure App Service
- Google App Engine
- Heroku
- IBM Cloud Foundry

# Practical Tasks: 

## 1. Activity: AWS Elastic Beanstalk for Amazon Academy Portal. 

## 2. Create a development environment to host a simple php web page (without a database ) on AWS Elastic Beanstalk. (Learner Lab )

### Lab Environment Setup Instructions

Go the Amazon Console and Search **Elastic Beanstalk** then click **Create Environment**. 

#### 1. Service Access 
Make sure to use the correct service roles and specify the EC2 key pair.

- **Service Role**:  
  `LabRole`
- **EC2 Key Pair**:  
  `deepakLab`
- **EC2 Instance Profile**:  
  `LabInstanceProfile`

#### 2. Networking and Database Settings
- Use the **recommended VPC**.
- Activate **Public IP** for Amazon EC2 instances.
- Select one of the available **instance subnets**.

#### 3. Updates, Monitoring, and Logging
- Set **Health Reporting** to **Basic**.
- Under **Managed Platform Updates**, uncheck **Activate**.

#### 3. Platform software 
- Leave the Document root empty

#### 4. Other Settings
You can leave the rest of the settings as default.

#### 5. Uploading Your PHP Code
- Zip your PHP files (without a folder, only the necessary files for your app) & upload.
  - **Even if it is just a single file, you are required to zip it or otherwise the deployment won't succeed.**
- Deploy the zipped files using Elastic Beanstalk.
- Once deployed, you should see your PHP app live.


## Read More
- [QuickStart: Deploy a PHP application to Elastic Beanstalk](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/php-quickstart.html)

- [QuickStart: Deploy a Docker application to Elastic Beanstalk](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/docker-quickstart.html)

## 3. AWS CLI in Terminal/PowerShell (Optional)
[Get started with the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)


