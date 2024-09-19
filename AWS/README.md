# About Cloud Computing

Cloud computing is a model for delivering computing services such as storage, processing power, and applications over the internet, instead of hosting and maintaining physical servers and hardware. Users access these resources through the internet ("the cloud") on a pay-as-you-go basis, which provides flexibility, scalability, and cost-efficiency.

### Key Characteristics of Cloud Computing:

1. **On-Demand Self-Service**: Users can access computing resources as needed, without requiring human intervention.
2. **Broad Network Access**: Services are available over the internet from any location and device.
3. **Resource Pooling**: Multiple users share the same physical resources (servers, storage) through virtualization.
4. **Rapid Elasticity**: Cloud resources can be scaled up or down dynamically according to demand.
5. **Measured Service**: Usage is monitored, controlled, and reported, ensuring that customers pay only for what they use.

### Types of Cloud Computing Services:

1. **Infrastructure as a Service (IaaS)**: Offers virtualized computing resources like virtual machines (VMs), storage, and networks. Example: Amazon Web Services (AWS) EC2.
2. **Platform as a Service (PaaS)**: Provides a platform that allows developers to build, run, and manage applications without worrying about the underlying infrastructure. Example: Google App Engine, Microsoft Azure.
3. **Software as a Service (SaaS)**: Delivers software applications over the internet on a subscription basis. Example: Google Workspace, Microsoft 365.

### Deployment Models:

1. **Public Cloud**: Services provided by third-party vendors over the internet to the general public. Example: AWS, Microsoft Azure, Google Cloud.
2. **Private Cloud**: Services are maintained on a private network, typically by a single organization for its own use, offering more control and security.
3. **Hybrid Cloud**: A combination of both public and private clouds, allowing data and applications to be shared between them.

### Benefits of Cloud Computing:

- **Cost Efficiency**: Reduces capital expenditure (CapEx) by eliminating the need to buy hardware and manage data centers.
- **Scalability**: Easily scale resources to handle increased workloads.
- **Flexibility and Mobility**: Access resources from anywhere with an internet connection.
- **Disaster Recovery and Backup**: Offers data backup, disaster recovery, and business continuity with minimal investment.

Cloud computing is widely adopted across industries for tasks like hosting websites, storing large datasets, running applications, and enabling artificial intelligence and machine learning operations.

![alt text](../Images/image28.png)

# Amazon EC2

Amazon EC2 (Elastic Compute Cloud) is a web service provided by AWS (Amazon Web Services) that offers scalable virtual servers in the cloud. It allows you to run applications and services on virtual machines (called instances) with flexible configuration options. Here’s a breakdown of key details about Amazon EC2:

### 1. **Instance Types**

- EC2 offers a variety of instance types optimized for different use cases, including:
  - **General Purpose**: Balanced resources (e.g., t2, t3, m5 instances).
  - **Compute Optimized**: For compute-intensive tasks (e.g., c5 instances).
  - **Memory Optimized**: For memory-intensive applications (e.g., r5 instances).
  - **Storage Optimized**: For applications requiring high I/O operations (e.g., i3 instances).
  - **GPU Instances**: For tasks requiring GPU acceleration like machine learning (e.g., p3 instances).

### 2. **Elasticity and Scalability**

- **Elasticity**: You can dynamically scale up or down your EC2 instances to handle changes in traffic or workload.
- **Auto Scaling**: Automatically adjusts the number of instances based on defined policies, keeping performance and costs optimized.

### 3. **Pricing Models**

- **On-Demand**: Pay for compute capacity by the second without any long-term commitment.
- **Reserved Instances**: Offers significant discounts (up to 75%) if you reserve an instance for 1 or 3 years.
- **Spot Instances**: Purchase unused capacity at a discounted rate, suitable for fault-tolerant and flexible workloads.
- **Savings Plans**: A flexible pricing model that offers lower prices in exchange for a commitment to use a specific amount of compute power.

### 4. **Storage Options**

- **Elastic Block Store (EBS)**: Persistent block storage volumes that you can attach to EC2 instances. EBS volumes can be used for databases, file systems, or any other block storage needs.
- **Instance Store**: Temporary block storage that is physically attached to the instance. Data is lost when the instance is stopped or terminated.
- **Elastic File System (EFS)**: A managed file system that can be shared among multiple instances.

### 5. **Security**

- **Security Groups**: Acts as a virtual firewall to control inbound and outbound traffic for instances.
- **Key Pairs**: EC2 instances use public-private key pairs for SSH access.
- **IAM Roles**: You can assign IAM (Identity and Access Management) roles to EC2 instances to securely access other AWS services (e.g., S3, DynamoDB).

### 6. **Networking**

- **Elastic IP**: Static IP addresses that you can allocate to instances.
- **VPC**: Virtual Private Cloud lets you launch instances in an isolated network.
- **Elastic Load Balancing (ELB)**: Automatically distributes incoming traffic across multiple EC2 instances.

### 7. **Regions and Availability Zones**

- EC2 instances are available in various **AWS Regions** globally. Each region has multiple **Availability Zones** (AZs), which are distinct data centers. This allows for high availability and disaster recovery.

### 8. **Monitoring and Management**

- **Amazon CloudWatch**: Provides monitoring for EC2 instances, including metrics like CPU, memory, and disk I/O.
- **EC2 Auto Recovery**: Automatically recovers an instance if it becomes impaired.
- **Elastic IPs and Load Balancers**: Manage traffic to multiple instances across different AZs or Regions.

### 9. **Use Cases**

- **Web Hosting**: EC2 is often used for scalable web hosting solutions.
- **Data Processing**: High-compute instances can be used for real-time or batch data processing.
- **Machine Learning**: GPU instances are well-suited for training machine learning models.
- **Gaming**: EC2 is used for hosting game servers with scalable capacity.

Would you like more details on any specific aspect of EC2?

![alt text](../Images/image30.png)

# AWS EBS (Elastic Block Store)

Amazon **EBS (Elastic Block Store)** is a block storage service designed for use with Amazon EC2 instances. EBS provides persistent storage volumes that can be attached to EC2 instances and are well-suited for databases, file systems, and other applications requiring reliable, high-performance storage.

Here are the key details about EBS volumes:

### 1. **Types of EBS Volumes**

EBS offers several types of volumes optimized for different use cases:

- **General Purpose SSD (gp2/gp3)**:
  - **gp2**: Provides baseline performance with burst capability.
  - **gp3**: Offers consistent performance with customizable IOPS and throughput, decoupling performance from capacity.
  - Use case: Most workloads, including boot volumes, small to medium databases, and development environments.
- **Provisioned IOPS SSD (io1/io2)**:

  - Designed for high-performance applications that require high IOPS (Input/Output Operations Per Second).
  - **io2** offers better durability (99.999%) and is often used for critical databases like Oracle, MySQL, and MongoDB.
  - Use case: Mission-critical applications, large databases, and workloads requiring consistent IOPS.

- **Throughput Optimized HDD (st1)**:

  - Provides low-cost, high-throughput storage for data that is accessed sequentially.
  - Use case: Large-scale data warehouses, big data processing, and log storage.

- **Cold HDD (sc1)**:
  - Lowest cost storage, designed for infrequently accessed data.
  - Use case: Archival storage and infrequently accessed data.

### 2. **EBS Volume Characteristics**

- **Persistence**: EBS volumes are persistent, meaning data is retained even if the EC2 instance is stopped, restarted, or terminated (except for the root volume if specified to delete on termination).
- **Scalability**: You can increase the size of an EBS volume, adjust performance characteristics (IOPS and throughput), and change volume types without stopping the instance.

- **Resilience**: EBS volumes are automatically replicated within the same availability zone (AZ) to prevent data loss due to hardware failure.

- **Snapshots**: EBS allows you to take point-in-time snapshots of volumes. Snapshots are stored in Amazon S3 and can be used to restore volumes or create new ones in different availability zones or regions.

### 3. **EBS Volume Attachment**

- **Attach to EC2 Instances**: An EBS volume can be attached to any running EC2 instance in the same availability zone. Once attached, it appears as a block device that can be formatted with a file system and mounted.
- **Multiple Attachments**: Only io1/io2 volumes can be attached to multiple instances simultaneously, using the **multi-attach** feature. However, this is typically used for clustered or shared file systems.
- **Detach**: EBS volumes can be detached from an EC2 instance and reattached to another instance. This makes it easy to migrate storage between instances.

### 4. **Performance Factors**

- **IOPS (Input/Output Operations per Second)**:
  - gp3, io1, and io2 volumes allow you to provision specific IOPS levels.
  - gp2 and gp3 volumes provide baseline IOPS with the ability to burst for short periods.
- **Throughput**: The speed at which data is read from or written to the volume. Some volume types like st1 and sc1 are optimized for high throughput.

### 5. **Data Encryption**

- EBS volumes can be encrypted to ensure data-at-rest security. EBS encryption uses AWS Key Management Service (KMS) to handle encryption keys.
  - Encryption applies to data in transit between the EC2 instance and EBS.
  - Snapshots created from encrypted volumes and volumes created from encrypted snapshots are also encrypted.

### 6. **Snapshots and Backup**

- **Snapshots**: You can take incremental snapshots of EBS volumes, which are stored in S3. Snapshots can be used to restore a volume or create new ones.
- **Automated Backups**: AWS provides automated backup policies to schedule periodic snapshots, making it easier to manage backups and disaster recovery.

### 7. **Resizing EBS Volumes**

- You can resize an EBS volume without downtime. This includes increasing the volume size, adjusting the IOPS (for io1/io2/gp3), and switching between different volume types.

### 8. **Pricing**

- **Pay-per-Use**: EBS pricing is based on the type and size of the volume, provisioned IOPS, and any additional snapshots you store.
- **Snapshot Costs**: You are charged for the amount of data stored in S3, which includes the data in the snapshot and incremental changes since the last snapshot.

### 9. **Use Cases**

- **Boot Volumes**: EBS volumes are often used to store operating systems and boot files for EC2 instances.
- **Database Storage**: High-performance EBS volumes (like io2) are used for running databases that require low-latency, high-reliability storage.
- **Big Data**: Throughput-optimized volumes (st1) are suitable for data-intensive applications like Hadoop clusters.
- **Backup and Disaster Recovery**: Snapshots provide an easy way to create backups of volumes and restore them when needed.

### 10. **Limitations**

- **Availability Zone Bound**: EBS volumes are tied to a single AZ and must be detached and reattached to migrate between AZs.
- **Maximum Size**: The maximum size for an EBS volume is 64 TiB.

Would you like to dive deeper into any specific feature of EBS?
