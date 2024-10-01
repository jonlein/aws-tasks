# Module 7: Storage

## Cloud Storage 
- A **computer data storage model** where digital data is stored in virtualized pools (known as the cloud)
- It provides greater reliability, scalability, and enhanced security compared to traditional on-premises storage solutions.
- Key benefits include remote access, data redundancy, and cost-efficient scalability for growing storage needs.
---

## AWS Storage Services
- **Amazon Simple Storage Service (S3)**
- **Amazon Elastic Block Store (EBS)**
- **Amazon Elastic File System (EFS)**
- **Instance Store (Ephemeral Storage)**
- **Amazon S3 Glacier**

---
## AWS Storage Types

### Instance Store (Ephemeral Storage)
- **Temporary storage** attached to Amazon EC2 instances.
- Data is **lost** when the instance is stopped or terminated.
- **Use Cases**: Ideal for **temporary data**, such as cache or scratch data that can be recreated if lost. Useful for high-performance computing (HPC) applications where data persistence isn't required.
---
### Amazon Elastic Block Store (EBS)
- **Persistent block storage** designed for use with Amazon EC2 instances.
- Can be **mounted** as a block device within the same **Availability Zone**.
- Only **one EC2 instance** can mount an EBS volume at a time.
- **High availability**: Automatically replicated within the same Availability Zone to ensure durability.
- **Low-latency and scalable** storage, ideal for applications requiring rapid data access.
- **Use Cases**: Suitable for **databases, application storage**, file systems, and workloads that require **consistent, low-latency performance**.
---
### Amazon Simple Storage Service (S3)
- **Object storage** where files (objects) are stored and accessed via **URLs**.
- **Globally accessible** from any location with internet access, providing **persistent, scalable storage**.
- **Use Cases**: Best for **media hosting**, static websites, **backups**, **data lakes**, and **big data analytics** due to its scalability and global accessibility.
---
### Amazon Elastic File System (EFS)
- **Shared file system** that can be mounted by multiple EC2 instances at the same time.
- Provides **elastic scalability** as storage grows or shrinks based on usage.
- **Use Cases**: Ideal for distributed applications, **content management systems**, **web serving**, **home directories**, and environments where multiple EC2 instances require **concurrent file access**.
---
### Amazon S3 Glacier
- **Cold storage** designed for long-term, infrequent access.
- Suitable for **archival** and **compliance** purposes, with flexible retrieval times (ranging from minutes to hours).
- **Use Cases**: Cost-effective solution for **long-term data archiving**, regulatory compliance, and backups that do not require frequent access.

---

### Differences Between AWS Storage Types

| **Storage Type**        | **Type**           | **Persistence**         | **Access**        | **Use Cases**                                 | **Data Durability**    |
|-------------------------|--------------------|-------------------------|-------------------|------------------------------------------------|------------------------|
| **Instance Store**       | Ephemeral Storage  | Temporary (data lost when instance stops) | Attached directly to an EC2 instance | High-performance computing, cache, scratch data | No persistence, no replication |
| **Amazon EBS**           | Block Storage      | Persistent (replicated in AZ) | Mounted as a block device by one EC2 instance | Databases, application storage, low-latency workloads | High availability within AZ (replicated) |
| **Amazon S3**            | Object Storage     | Persistent (global accessibility) | Accessible via unique URLs (HTTP/S) | Media hosting, backups, big data analytics, data lakes | Extremely durable (replicated across multiple facilities) |
| **Amazon EFS**           | File Storage       | Persistent (scalable)    | Shared file system mounted by multiple instances | Web serving, content management, shared directories | High availability and durability across multiple AZs |
| **Amazon S3 Glacier**    | Cold Storage       | Persistent (archival storage) | Accessible on-demand with retrieval delays | Long-term archival, compliance data, infrequent backups | Extremely durable (11 9s of durability) |

---
## Differences Between Object Storage, File Storage, and Block Storage

| **Feature**         | **Object Storage (e.g., Amazon S3)**            | **File Storage (e.g., Amazon EFS)**        | **Block Storage (e.g., Amazon EBS)**       |
|---------------------|-------------------------------------------------|--------------------------------------------|--------------------------------------------|
| **Structure**        | Flat structure: data stored as objects in a pool | Hierarchical structure: directories and subdirectories | Data is split into blocks and stored as volumes |
| **Access**           | Objects accessed via unique identifiers (keys) | Files accessed via paths, similar to traditional systems | Blocks are accessed as raw storage via a mounted device |
| **Metadata**         | Extensive metadata associated with each object | Limited metadata (file name, permissions)  | No metadata; data is treated as blocks of raw storage |
| **Scalability**      | Highly scalable: handles large volumes of data | Scalable, but typically for file-based applications | Limited by the size of the volume and availability zone |
| **Use Cases**        | Large-scale unstructured data (media, backups, analytics) | Collaboration, web serving, file sharing   | Databases, low-latency apps, boot volumes for EC2 |
| **Persistence**      | Persistent, highly durable across regions       | Persistent, automatically scaling across instances | Persistent, but tied to a single instance in one AZ |
| **Performance**      | Optimized for throughput and large files        | Good for concurrent access across multiple systems | Low-latency, high-performance storage for I/O-intensive apps |

---

## Practical Task : 

### Lab - 4 Working with EBS (Amazon Academy Portal: Module 7 Storage)
---
### In-class Tasks

1. Create an S3 bucket. You are required to enable versioning for the bucket and upload few files to it so that you can set  permissions to allow public access to certain objects and restrict others. 

2. Configure a lifecycle policy for an S3 bucket to transition objects to different storage classes (e.g., Glaciers)
    - Create a rule to move objects to S3 Glacier after 30 days.
    - Create a rule to delete versions older than 90 days.

3. Create another S3 bucket to store the logs.You will enable logging for the earlier created bucket and store the logs in this newly created bucket. 

4. Create a simple static website (html file ), upload it to S3 bucket. Configure the bucket for static website hosting. Access the website using the S3 bucket URL. 

5. For this tak, you will utilize Amazon Elastic File System (EFS) and make it accessible by at-least 2 EC2 instances. 
    -  Create an Amazon EFS File System 
        - VPC: Select the VPC where your EC2 instances are located.
        - Network: Configure the network settings. Ensure that the security groups allow NFS traffic (port 2049).
    - Configure Security Groups and Network
        - Ensure that the security group attached to your EFS mount targets allows inbound traffic on port 2049 (NFS).
        - Update the security groups for your EC2 instances to allow outbound traffic to port 2049.
        - Mount EFS on EC2 Instances
    - Check from both instances that the newly created Amazon EFS is allowing shared access to files and directories.


