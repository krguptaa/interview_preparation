# AWS Interview Questions

Amazon Web Services (AWS) interview questions and answers, including practical examples and real-world scenarios.

---

## 1. What is AWS and what are its primary services?

### Answer

**Amazon Web Services (AWS)** is a cloud computing platform provided by Amazon. It offers a wide range of cloud services that allow organizations to build, deploy, run, and manage applications without maintaining physical infrastructure.

AWS follows a **pay-as-you-go pricing model**, where customers generally pay for the resources they consume.

AWS provides services across different cloud models, including:

- **Infrastructure as a Service (IaaS)** – Provides infrastructure such as virtual servers, storage, and networking.
- **Platform as a Service (PaaS)** – Provides managed platforms for deploying applications without managing the underlying infrastructure.
- **Software as a Service (SaaS)** – Provides complete software applications through the internet.

### Common AWS Services

| Service | Purpose |
|---|---|
| **EC2** | Virtual servers / compute |
| **S3** | Object storage |
| **RDS** | Managed relational databases |
| **DynamoDB** | Managed NoSQL database |
| **Lambda** | Serverless compute |
| **Elastic Beanstalk** | Application deployment platform |
| **IAM** | Identity and access management |
| **VPC** | Virtual networking |
| **CloudFront** | Content delivery / CDN |
| **Route 53** | DNS and domain management |
| **CloudWatch** | Monitoring and logging |
| **SQS** | Message queuing |
| **SNS** | Notifications and pub/sub messaging |

### Practical Example

Suppose we have an e-commerce application:

```text
Users
  |
  v
Route 53
  |
  v
CloudFront
  |
  v
Application Load Balancer
  |
  v
EC2 / ECS
  |
  +------> RDS MySQL
  |
  +------> S3
  |
  +------> SQS
```

For example:

- **Route 53** manages the domain name.
- **CloudFront** delivers static content faster to users.
- **EC2** runs the backend application.
- **RDS MySQL** stores transactional data.
- **S3** stores images, documents, and reports.
- **SQS** handles background jobs.
- **CloudWatch** monitors application and infrastructure health.
- **IAM** controls access to AWS resources.

### Interview Tip

A good senior-level answer should not only define AWS. Explain **why you would select specific AWS services for a real application**.

---

## 2. Explain the key components of Amazon S3.

### Answer

**Amazon S3 (Simple Storage Service)** is a highly scalable **object storage service** used to store and retrieve virtually any amount of data.

Unlike a traditional file system, S3 stores data as **objects inside buckets**.

An S3 object consists primarily of:

- Object data
- Object key
- Metadata
- Optional tags and other properties

### Key S3 Components

#### 1. Bucket

A **bucket** is a container used to store objects.

Example:

```text
my-company-production-files
```

A bucket can contain objects such as:

```text
documents/report.pdf
images/logo.png
users/profile.jpg
backups/database.sql
```

#### 2. Object

An **object** is the actual data stored in S3.

Example:

```text
invoice-2026-001.pdf
```

The object contains the file data along with metadata and other object properties.

#### 3. Key

The **key** is the unique name used to identify an object within a bucket.

Example:

```text
customers/1001/invoices/invoice-2026-001.pdf
```

Here:

```text
Bucket: my-company-production-files

Key:
customers/1001/invoices/invoice-2026-001.pdf
```

> **Important:** S3 does not use traditional folders in the same way as a file system. What looks like a folder structure is generally represented through object keys using prefixes.

#### 4. Metadata

Metadata contains information about an object.

Example:

```text
Content-Type: application/pdf
Content-Length: 245678
Last-Modified: 2026-08-24
```

Metadata can be useful when applications need additional information about stored objects.

#### 5. Versioning

S3 Versioning allows multiple versions of the same object to be maintained.

For example:

```text
report.pdf
    |
    +-- Version 1
    +-- Version 2
    +-- Version 3
```

If a user accidentally overwrites or deletes an object, versioning can help recover a previous version.

#### 6. Lifecycle Management

S3 Lifecycle rules allow objects to automatically transition between storage classes or expire after a defined period.

Example:

```text
0 - 30 days     -> S3 Standard
31 - 90 days    -> S3 Standard-IA
91+ days        -> S3 Glacier
```

This can reduce storage costs for data that becomes less frequently accessed.

#### 7. Encryption

S3 supports encryption for protecting stored data.

Encryption can be used to protect sensitive documents, customer files, backups, and other data.

#### 8. Access Control

Access to S3 resources can be controlled using mechanisms such as:

- IAM policies
- Bucket policies
- S3 Block Public Access
- Encryption controls

### Practical Example

Suppose a banking application allows users to upload documents.

```text
User
 |
 | Upload Passport.pdf
 v
Backend API
 |
 v
S3 Bucket
 |
 +-- customers/
       |
       +-- 10001/
             |
             +-- passport.pdf
             +-- address-proof.pdf
```

The database might store:

```text
customer_id = 10001
document_type = PASSPORT
s3_key = customers/10001/passport.pdf
```

The actual document is stored in S3 while the application database stores the reference to it.

### Interview Tip

If asked **"Why S3 instead of storing files directly on EC2?"**, mention:

- Highly scalable object storage
- High durability
- Independent of EC2 lifecycle
- Easy integration with other AWS services
- Lifecycle policies
- Versioning
- Encryption
- Cost-effective storage classes

---

## 3. What are the different types of cloud computing models?

### Answer

Cloud computing models describe how much infrastructure and software management responsibility belongs to the customer versus the cloud provider.

The three traditional models are:

1. IaaS
2. PaaS
3. SaaS

### IaaS – Infrastructure as a Service

IaaS provides basic infrastructure such as:

- Virtual machines
- Storage
- Networking
- Operating systems

The customer is responsible for managing much of the software stack.

#### Real-World Analogy

IaaS is like **renting an empty plot of land**. You need to build and manage your own house.

#### AWS Example

**Amazon EC2** is a common example of IaaS.

```text
AWS
 |
 +-- EC2
      |
      +-- Operating System
      +-- Web Server
      +-- Application
      +-- Configuration
```

You are responsible for things such as:

- OS configuration
- Application installation
- Security patches
- Web server configuration
- Application deployment

### PaaS – Platform as a Service

PaaS provides a managed application platform.

The cloud provider manages more of the underlying infrastructure, while developers primarily focus on the application.

#### Real-World Analogy

PaaS is like **renting a house that already has electricity, plumbing, and basic infrastructure configured**.

#### AWS Example

**AWS Elastic Beanstalk** is a commonly used example.

```text
Developer
    |
    v
Application Code
    |
    v
Elastic Beanstalk
    |
    +-- EC2
    +-- Load Balancer
    +-- Auto Scaling
    +-- Platform Configuration
```

Elastic Beanstalk handles much of the infrastructure provisioning and application deployment.

### SaaS – Software as a Service

SaaS provides a complete software application that users can directly consume.

The provider manages:

- Infrastructure
- Application
- Platform
- Updates
- Maintenance

#### Real-World Analogy

SaaS is like **moving into a fully furnished house**. Everything is already prepared and ready to use.

#### Examples

- Salesforce
- Microsoft 365
- Zoom
- Gmail

The user primarily consumes the application rather than managing its infrastructure.

### IaaS vs PaaS vs SaaS

| Model | Customer Responsibility | Example |
|---|---|---|
| **IaaS** | OS, application, configuration | EC2 |
| **PaaS** | Mainly application/code | Elastic Beanstalk |
| **SaaS** | Mainly application usage | Salesforce, Microsoft 365 |

### Interview Tip

A simple way to remember:

```text
IaaS -> You manage more
PaaS -> AWS manages more
SaaS -> Provider manages almost everything
```

---

## 4. What do you understand by Amazon EC2?

### Answer

**Amazon EC2 (Elastic Compute Cloud)** is a cloud-based compute service that provides resizable virtual servers.

Instead of purchasing and maintaining a physical server, we can launch an EC2 instance whenever we need compute capacity.

We can select:

- CPU
- Memory
- Storage
- Operating system
- Network configuration
- Security configuration
- Instance type

### Simple Example

Traditional infrastructure:

```text
Buy Physical Server
       |
       v
Install OS
       |
       v
Install Web Server
       |
       v
Deploy Application
```

With AWS:

```text
AWS Console
    |
    v
Launch EC2
    |
    v
Select Instance Type
    |
    v
Select AMI
    |
    v
Configure Security Group
    |
    v
Deploy Application
```

### Practical Example

Suppose we have a PHP application.

We could deploy it as:

```text
Internet
    |
    v
Application Load Balancer
    |
    +----------------+
    |                |
    v                v
 EC2 Instance 1   EC2 Instance 2
    |                |
    +-------+--------+
            |
            v
        RDS MySQL
```

This architecture provides better availability than running the application on a single server.

### Why is EC2 called "Elastic"?

Because compute capacity can be increased or decreased according to application requirements.

For example:

```text
Normal Traffic
     |
     v
2 EC2 Instances

High Traffic
     |
     v
6 EC2 Instances
```

This can be combined with **Auto Scaling** to automatically adjust the number of instances.

### Interview Tip

For a senior-level interview, mention that EC2 is not just "a virtual machine." It provides control over:

- Compute capacity
- Instance types
- Networking
- Security groups
- EBS storage
- AMIs
- Auto Scaling
- Load balancing
- Monitoring

---

## 5. What are the different types of EC2 instances and purchasing options?

### Important Clarification

There are **two different concepts** that are often confused:

1. **EC2 Instance Types/Families** – Define the hardware characteristics of the instance.
2. **EC2 Purchasing Options** – Define how you pay for the instance.

### A. EC2 Instance Types

EC2 instance families are designed for different workloads.

#### 1. General Purpose

Examples:

```text
T3
T4g
M7i
```

Suitable for:

- Web applications
- APIs
- Development environments
- Small and medium databases

#### 2. Compute Optimized

Examples:

```text
C7i
C7g
```

Designed for workloads that require high CPU performance.

Suitable for:

- Batch processing
- High-performance web servers
- Scientific workloads
- CPU-intensive applications

#### 3. Memory Optimized

Examples:

```text
R7i
X8g
```

Designed for applications requiring large amounts of memory.

Suitable for:

- In-memory databases
- Large caches
- Real-time analytics

#### 4. Storage Optimized

Examples include:

```text
I-series
D-series
H-series
```

Designed for workloads requiring high local storage performance.

Suitable for:

- Large-scale data processing
- Log processing
- Data warehouses
- High I/O workloads

#### 5. Accelerated Computing

Examples include GPU-based instances.

Suitable for:

- Machine learning
- AI workloads
- Graphics processing
- Video processing

### B. EC2 Purchasing Options

#### 1. On-Demand

You pay for compute capacity without a long-term commitment.

Suitable for:

- Development
- Testing
- Unpredictable workloads
- Short-term workloads

Example:

```text
Launch EC2
    |
    v
Use for 2 days
    |
    v
Terminate EC2
```

#### 2. Reserved Instances

Reserved Instances provide discounted pricing when committing to a specific configuration for a term, traditionally 1 or 3 years.

They are useful when workloads are predictable.

Example:

```text
Production Server
       |
       v
Runs continuously
       |
       v
Long-term predictable workload
       |
       v
Reserved Instance
```

> **Interview Note:** AWS also provides **Savings Plans**, which are often worth considering for long-term compute commitments because they can provide more flexibility than traditional Reserved Instances.

#### 3. Spot Instances

Spot Instances use spare EC2 capacity and can provide significant cost savings, but AWS can interrupt them when the capacity is needed.

Example:

```text
Image Processing Queue
        |
        v
Spot EC2 Instances
        |
        v
Process Images
        |
        +----> Interrupted
        |
        v
Resume / Retry
```

Spot is suitable because the workload is fault tolerant.

### EC2 Instance Type vs Purchasing Option

| Concept | Example | Purpose |
|---|---|---|
| Instance Family | M7i | Determines workload characteristics |
| Instance Size | `m7i.large` | Determines CPU/memory capacity |
| On-Demand | Pay as you use | Flexible workloads |
| Reserved Instance | 1/3-year commitment | Predictable workloads |
| Spot | Spare capacity | Fault-tolerant workloads |
| Savings Plan | Usage commitment | Flexible long-term savings |

### Interview Tip

If the interviewer asks:

> "Which EC2 instance should you select?"

Do not immediately answer with a specific instance.

First ask:

- What is the workload?
- Is it CPU intensive?
- Is it memory intensive?
- Is it storage intensive?
- Is GPU required?
- What is the expected traffic?
- What are the availability requirements?
- What is the budget?
- Can the workload tolerate interruption?

Then select the appropriate instance family and purchasing model.

---

## 6. What is the difference between stopping and terminating an EC2 instance?

### Answer

**Stopping** and **terminating** an EC2 instance are different operations.

### Stopping an EC2 Instance

When an EC2 instance is stopped:

```text
Running
   |
   v
Stopped
```

The virtual machine is shut down, but the instance configuration remains available and it can generally be started again.

### Example

Suppose a developer uses an EC2 instance only during working hours.

```text
9:00 AM  -> Start EC2
6:00 PM  -> Stop EC2
```

Stopping the instance can reduce compute charges because the instance is no longer running.

However, associated resources such as **EBS volumes** can continue to incur charges.

### Terminating an EC2 Instance

When an instance is terminated:

```text
Running
   |
   v
Terminated
```

The instance is permanently removed and cannot be started again.

### Example

Suppose we created an EC2 instance only for temporary testing.

```text
Test EC2
   |
   v
Testing Complete
   |
   v
Terminate
```

This removes the instance and prevents further instance compute charges.

### Important Difference

| Feature | Stop | Terminate |
|---|---|---|
| Instance shuts down | Yes | Yes |
| Can start again | Yes | No |
| Instance remains available | Yes | No |
| Instance configuration retained | Yes | No |
| EBS data | Usually retained depending on configuration | Depends on `DeleteOnTermination` setting |
| Use case | Temporary shutdown | Permanently remove instance |

### Practical Interview Example

**Question:** You have a development server that is not required at night. What would you do?

**Answer:**

> I would normally stop the EC2 instance rather than terminate it because I need the server again the next morning. I would also review attached EBS volumes and other resources because stopping an instance does not necessarily eliminate all associated AWS charges.

---

## 7. Explain Availability Zones and Regions in AWS.

### Answer

**AWS Regions** and **Availability Zones (AZs)** are fundamental concepts used to build highly available and fault-tolerant applications.

### AWS Region

An AWS **Region** is a geographic area where AWS operates multiple isolated Availability Zones.

Examples include:

```text
us-east-1
eu-west-1
ap-south-1
```

A Region is designed to be independent from other AWS Regions.

### Availability Zone

An **Availability Zone** is one or more discrete data centers with redundant power, networking, and connectivity within an AWS Region.

For example:

```text
Region: ap-south-1
        |
        +---- AZ-1
        |
        +---- AZ-2
        |
        +---- AZ-3
```

AWS states that each Region has multiple Availability Zones, and the AZs are physically separate and connected through redundant, low-latency networking.

### Why do we need Availability Zones?

Suppose we deploy our entire application in one Availability Zone:

```text
Region
   |
   +---- AZ-1
          |
          +---- Application
```

If that AZ experiences an infrastructure failure, the application could become unavailable.

Instead, we can deploy across multiple AZs:

```text
                 Region
                   |
          +--------+--------+
          |        |        |
         AZ-1     AZ-2     AZ-3
          |        |        |
        EC2      EC2      EC2
          \        |       /
           \       |      /
            Load Balancer
```

If one AZ becomes unavailable, traffic can be served from the other AZs.

### Practical Example

Suppose we have an online shopping application.

#### Single-AZ Architecture

```text
Users
  |
  v
Load Balancer
  |
  v
AZ-1
 |
 +-- EC2
 |
 +-- Database
```

If AZ-1 fails, the application may become unavailable.

#### Multi-AZ Architecture

```text
                    Users
                      |
                      v
              Application LB
                 /         \
                /           \
             AZ-1           AZ-2
              |               |
            EC2             EC2
              \               /
               \             /
                 RDS Multi-AZ
```

This provides better availability and fault tolerance.

### Region vs Availability Zone

| Feature | Region | Availability Zone |
|---|---|---|
| Meaning | Geographic AWS infrastructure area | Isolated infrastructure location within a Region |
| Contains | Multiple AZs | One or more discrete data centers |
| Example | `ap-south-1` | `ap-south-1a` |
| Main purpose | Geographic isolation | High availability and fault tolerance |
| Scope | Larger | Smaller |

### Current AWS Infrastructure

AWS continuously expands its global infrastructure, so the exact number of Regions and Availability Zones can change.

> **Interview Tip:** Avoid memorizing a fixed Region/AZ number unless the interviewer specifically asks for the current count.

A better interview answer is:

> "AWS operates multiple geographic Regions, and each Region contains multiple isolated Availability Zones. We normally deploy production workloads across multiple AZs to improve availability and fault tolerance."

---

# Quick Interview Revision

| Question | Key Point |
|---|---|
| **What is AWS?** | Cloud platform providing compute, storage, database, networking, security, and many other managed services |
| **What is S3?** | Scalable object storage |
| **What is an S3 bucket?** | Container for objects |
| **What is an S3 key?** | Identifier used to locate an object within a bucket |
| **What is IaaS?** | Infrastructure provided by cloud provider; customer manages more of the stack |
| **What is PaaS?** | Managed platform for deploying applications |
| **What is SaaS?** | Complete software application delivered as a service |
| **What is EC2?** | Resizable virtual compute capacity |
| **EC2 instance family?** | Determines workload characteristics such as CPU, memory, storage, or GPU |
| **On-Demand?** | Flexible pay-as-you-go compute |
| **Reserved Instance?** | Discount associated with a commitment to a specific EC2 configuration |
| **Spot Instance?** | Uses spare EC2 capacity at a discount and may be interrupted |
| **Stop vs Terminate?** | Stop = shut down and potentially restart; Terminate = permanently remove instance |
| **Region?** | Geographic AWS infrastructure area |
| **Availability Zone?** | Isolated infrastructure location within a Region |
| **Why multiple AZs?** | High availability and fault tolerance |

---

# Senior-Level Interview Approach

For a **10+ years experienced candidate**, avoid answering AWS questions with definitions only.

Try to structure answers like this:

```text
1. Definition
      ↓
2. Why it is used
      ↓
3. Real-world example
      ↓
4. Architecture / implementation
      ↓
5. Trade-offs
      ↓
6. When I would choose it
```

For example, instead of saying:

> "S3 is object storage."

A stronger answer is:

> "S3 is AWS's scalable object storage service. In a typical application, I would use it for documents, images, backups, logs, or generated reports rather than storing those files directly on an application server. I would typically combine S3 with IAM policies, encryption, versioning, lifecycle rules, and appropriate storage classes. For example, customer documents could be stored under customer-specific S3 keys while the application database stores only the object key or URL reference."

