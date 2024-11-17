
## Enhanced Networking 


### EC2 Enhanced Networking SR-IOV

- higher bandwidth, higher PPS (packet per second), lower latency
- option 1 Elastic Network Adapter up to 100 GBps 
- option 2 intel 825899 VF up to 10 GBPS - LEGACY
- Works for newer gen ec2 instances

### EFA ELASTIC FABRIC ADAPTER

- only works on linux 
- improved for HPC 
- great inter-node communications, tightly coupled workloads 
- leverages message passing interface standard (MPI)
- bypasses the underlying Linux OS to provide low-latency reliable transport


## Placement Groups

way to control EC2 placement strategy

- cluster- grouped together in single az
	- big data job that needs to be completed fast
	- application that needs extremely low latency and high network throughput
- spread - spread across different hardware max 7 instances per az 
	- limited to 7 instances per AZ per placement group
	- Application that needs maximize high availability
	- critical applications where each instance must be isolated from failure from each other
- partition - similar to spread but spread across different hardware across AZ can scale to hundreds of instances.



## SCALE SYSTEM MANAGER SSM 


### SSM Overview
- helps manage ec2 and on prem systems at scale 
- get operation insights about stage of infra 
- Patching automations for enhanced compliance
- works windows and linux 
- full integration with cloudwatch, aws config
- free service 

### SSM FEATURES

- Resource Groups 

### Change Management

- Automations
- Maintenance windows 

### Application Management

- Parameter Store

### Node Management

- Inventory
- session manager
- Run Command
- state manager
- patch manager


- to use install onto system we control 
- if can not install issue with the SSM agent probably 
- make sure ec2 has proper IAM role to allow ssm actions 

---

### **Core Concepts**

1. **What is AWS Systems Manager?**
    
    - A unified interface to view operational data from multiple AWS services.
    - Automates operational tasks across AWS resources, such as EC2, RDS, and S3.
    - Provides tools for configuration management, operational data analysis, and automation.
2. **Key Components:**
    
    - **Session Manager**: Securely manage EC2 instances through browser-based or command-line access without needing SSH/RDP.
    - **Run Command**: Execute commands on EC2 instances or on-premises servers without logging into them.
    - **State Manager**: Automatically apply and manage configurations on AWS resources.
    - **Patch Manager**: Automate the patching of managed instances for compliance.
    - **Inventory**: Collect metadata about your instances and software installed on them.
    - **Parameter Store**: Secure storage for configuration data and secrets.
    - **Automation**: Simplify repetitive tasks using predefined or custom runbooks.

---

### **Important Features and Concepts**

1. **SSM Agent:**
    
    - Installed on instances to communicate with the Systems Manager service.
    - Pre-installed on Amazon Linux, Ubuntu, and Windows Server AMIs. Ensure it's up-to-date.
2. **Instance Profile Roles:**
    
    - EC2 instances must have an **IAM role** with the `AmazonSSMManagedInstanceCore` policy attached to interact with Systems Manager.
3. **Parameter Store:**
    
    - Securely store configuration variables, secrets, and license keys.
    - Two tiers:
        - **Standard Parameters** (free, limited to 4 KB).
        - **Advanced Parameters** (supports more size and features, charged).
    - Integration with AWS Key Management Service (KMS) for encryption.
4. **Session Manager:**
    
    - Secure, auditable, and eliminates the need to open inbound ports.
    - Logs can be stored in S3 or CloudWatch for auditing.
5. **Patch Manager:**
    
    - Allows automation of patch management for EC2 instances.
    - Supports baseline definitions (AWS-provided or custom).
    - Can schedule patching via **Maintenance Windows**.
6. **Automation Documents (SSM Documents):**
    
    - Predefined or custom YAML/JSON documents to define actions for automation tasks.
    - AWS-provided documents include actions like restarting an instance or updating AMIs.
7. **Compliance:**
    
    - Monitor instances for adherence to patching, state, and configuration baselines.

---

### **Common Use Cases**

1. **Automating Common Tasks:**
    
    - Automate deployments, AMI creation, and backups using Automation.
2. **Configuration Management:**
    
    - Enforce desired configurations with State Manager and detect drifts.
3. **Secure Secrets Management:**
    
    - Store database credentials, API keys, and passwords in Parameter Store.
4. **Patch Management:**
    
    - Keep instances up-to-date and track compliance with patch baselines.
5. **Centralized Logs:**
    
    - Use Session Manager to log all commands and interactions for auditing.

---
### **Elastic Load Balancing (ELB)**

#### **Overview**

Elastic Load Balancing (ELB) distributes incoming application traffic across multiple targets, such as EC2 instances, containers, and IP addresses, in one or more availability zones (AZs).

---

#### **Types of Load Balancers**

1. **Application Load Balancer (ALB):**
    
    - Operates at Layer 7 (Application Layer) of the OSI model.
    - Ideal for HTTP/HTTPS traffic and provides advanced request routing based on content.
    - Supports host-based and path-based routing.
    - Supports WebSocket and gRPC protocols.
    - Can integrate with AWS Web Application Firewall (WAF) for enhanced security.
2. **Network Load Balancer (NLB):**
    
    - Operates at Layer 4 (Transport Layer).
    - Ideal for handling TCP, UDP, and TLS traffic with high performance and low latency.
    - Provides static IP addresses or can assign an Elastic IP.
    - Supports ultra-high throughput and millions of requests per second.
3. **Classic Load Balancer (CLB):**
    
    - Operates at Layer 4 and 7 but is considered legacy.
    - Supports basic load balancing features for HTTP, HTTPS, and TCP protocols.
    - Not recommended for new applications; migrate to ALB or NLB.

---

#### **Key Features**

1. **Cross-Zone Load Balancing:**
    
    - Ensures that traffic is evenly distributed across all targets in all enabled AZs.
2. **Health Checks:**
    
    - ALB and NLB use target group health checks.
    - Health checks monitor the status of registered targets to route traffic only to healthy instances.
3. **Target Groups:**
    
    - A logical grouping of targets (e.g., EC2 instances, Lambda functions, IP addresses) for ALB and NLB.
    - Each target group uses a health check to determine the health of its members.
4. **SSL Termination:**
    
    - SSL/TLS certificates can be uploaded to an ALB or NLB for secure traffic termination.
5. **Sticky Sessions (Session Affinity):**
    
    - Use cookies to route a user’s requests to the same target during a session.
6. **Logging and Monitoring:**
    
    - Access logs can be enabled for ALB and NLB to store detailed request information in S3.
    - Integrated with CloudWatch for monitoring metrics like latency, request count, and error rates.

---

#### **Exam Tips**

1. **Know Load Balancer Use Cases:**
    - ALB for Layer 7, NLB for Layer 4, and CLB for legacy apps.
2. **Understand Health Checks:**
    - Be familiar with configuring health check intervals and thresholds.
3. **Cross-Zone Load Balancing:**
    - Know when and why to enable/disable cross-zone load balancing.
4. **Elasticity:**
    - Load balancers automatically scale to handle varying traffic loads.
5. **Security:**
    - ALBs can use AWS WAF for traffic filtering, and both ALB and NLB can use Security Groups.

---

### **Auto Scaling Groups (ASGs)**

#### **Overview**

Auto Scaling Groups (ASGs) automatically scale EC2 instances up or down based on traffic and load, ensuring optimal performance and cost efficiency.

---

#### **Key Components**

1. **Launch Templates and Launch Configurations:**
    
    - Define the settings for EC2 instances launched by the ASG, such as AMI, instance type, key pair, and security groups.
    - **Launch Templates** are preferred because they support versioning and advanced features.
2. **Scaling Policies:**
    
    - **Target Tracking Scaling:**
        - Automatically adjusts the number of instances to maintain a specific metric (e.g., CPU utilization at 50%).
    - **Step Scaling:**
        - Adjusts the number of instances based on predefined thresholds.
    - **Scheduled Scaling:**
        - Automatically scales based on a schedule (e.g., adding instances at peak hours).
3. **Health Checks:**
    
    - ASG can use EC2 instance status checks and ELB target group health checks.
    - Automatically replaces unhealthy instances.
4. **Desired, Minimum, and Maximum Capacity:**
    
    - Desired capacity: The number of instances the ASG attempts to maintain.
    - Minimum capacity: The minimum number of instances.
    - Maximum capacity: The maximum number of instances.
5. **Lifecycle Hooks:**
    
    - Add custom actions at instance launch or termination (e.g., running a script during instance launch).
6. **Termination Policies:**
    
    - Decide which instances are terminated first when scaling down (e.g., oldest instance, closest to billing hour).
7. **Scaling Cooldowns:**
    
    - Prevents rapid scaling by allowing time for changes to take effect.

---

#### **Integration with Load Balancers**

- **ASGs can integrate with ALB, NLB, and CLB.**
- Automatically registers and deregisters EC2 instances from load balancer target groups.
- Ensures traffic is only routed to healthy instances.

---

#### **Monitoring and Alerts**

1. **CloudWatch Alarms:**
    
    - Monitor metrics like CPU utilization, network I/O, or custom metrics.
    - Use alarms to trigger scaling policies.
2. **Scaling Activity Logs:**
    
    - View scaling activity in the ASG console or CloudWatch.

---

#### **Exam Tips**

1. **Understand Scaling Policies:**
    - Know the differences between target tracking, step scaling, and scheduled scaling.
2. **Integration with ELB:**
    - Know how ASGs and ELB work together to handle health checks and traffic routing.
3. **Lifecycle Hooks:**
    - Familiarize yourself with custom workflows during instance launch or termination.
4. **Cooldown Period:**
    - Understand how cooldown settings impact scaling operations.
5. **Launch Templates vs Configurations:**
    - Launch templates offer more features, such as support for mixed instance types and multiple network interfaces.

---

### **Comparison Table: ALB vs. NLB vs. CLB**

| Feature             | ALB                     | NLB              | CLB                  |
| ------------------- | ----------------------- | ---------------- | -------------------- |
| OSI Layer           | Layer 7                 | Layer 4          | Layer 4 and 7        |
| Protocols Supported | HTTP, HTTPS, gRPC       | TCP, UDP, TLS    | HTTP, HTTPS, TCP     |
| Routing Type        | Content-based           | Connection-based | Basic Load Balancing |
| WebSocket Support   | Yes                     | No               | No                   |
| Target Types        | Instances, IPs, Lambdas | Instances, IPs   | Instances only       |
| WAF Integration     | Yes                     | No               | No                   |

---