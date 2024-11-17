
### **AWS EBS (Elastic Block Store) and EFS (Elastic File System) Overview for SysOps Admin Exam**

---

### **Elastic Block Store (EBS)**

#### **What is EBS?**

EBS provides block storage for use with EC2 instances. It is persistent, durable, and high-performance storage that integrates seamlessly with EC2.

---

#### **Key Features**

1. **Volume Types:**
    
    - **General Purpose SSD (gp3, gp2):**
        - Balances price and performance.
        - **gp3**: Baseline performance of 3,000 IOPS, customizable IOPS and throughput.
        - **gp2**: Performance scales with volume size (up to 16,000 IOPS).
    - **Provisioned IOPS SSD (io2, io1):**
        - High-performance storage for mission-critical workloads.
        - Offers up to 64,000 IOPS for large volumes.
    - **Throughput Optimized HDD (st1):**
        - Low-cost option for big data and sequential workloads.
        - Not suitable for boot volumes.
    - **Cold HDD (sc1):**
        - Lowest cost, for infrequently accessed data.
        - Not suitable for boot volumes.
    - **Magnetic (Standard):**
        - Deprecated, legacy use cases only.
2. **Snapshots:**
    
    - Point-in-time backups stored in S3.
    - Incremental backups save only the changes since the last snapshot.
    - Can be used to create new EBS volumes.
3. **Encryption:**
    
    - Uses AWS Key Management Service (KMS).
    - Encrypts data at rest, in transit, and snapshots.
4. **Multi-Attach (io1/io2):**
    
    - Allows multiple EC2 instances to simultaneously attach to the same volume for read/write.
5. **Performance Metrics:**
    
    - **IOPS (Input/Output Operations Per Second):** Measures performance.
    - **Throughput:** Measures data transfer rates.

---

#### **Common Use Cases**

1. **Boot Volumes:**
    
    - Supports launching EC2 instances.
    - General Purpose SSD (gp2, gp3) is commonly used.
2. **Databases:**
    
    - Use Provisioned IOPS SSD (io2, io1) for high-performance requirements.
3. **Big Data and Analytics:**
    
    - Throughput Optimized HDD (st1) for sequential workloads.
4. **Backup and Recovery:**
    
    - Snapshots for disaster recovery.

---

#### **Key Exam Topics for EBS**

1. **Volume Management:**
    
    - Know how to create, attach, detach, and delete EBS volumes.
    - Understand resizing volumes (modify volume without downtime).
2. **Snapshots:**
    
    - Understand how to create and restore from snapshots.
    - Know the use of **Amazon Data Lifecycle Manager** to automate snapshot management.
3. **Performance Optimization:**
    
    - Choose the right volume type based on workload (e.g., gp3 for cost-efficiency, io2 for high performance).
4. **Availability and Durability:**
    
    - EBS volumes are AZ-specific but can be copied across AZs using snapshots.
5. **Encryption:**
    
    - Use KMS-managed keys for encryption.
    - Understand how encryption works for volumes and snapshots.
6. **Multi-Attach:**
    
    - Use for applications that support concurrent access (e.g., clustering).

---

### **Elastic File System (EFS)**

#### **What is EFS?**

Amazon EFS is a fully managed, scalable, and elastic file storage system that can be mounted by multiple EC2 instances. It supports the **NFS protocol**.

---

#### **Key Features**

1. **Elastic and Scalable:**
    
    - Automatically scales up or down as files are added or removed.
    - No need to provision or manage capacity.
2. **Performance Modes:**
    
    - **General Purpose (Default):** For latency-sensitive workloads.
    - **Max I/O:** For high throughput and parallel workloads, with slightly higher latency.
3. **Throughput Modes:**
    
    - **Bursting (Default):** Provides baseline throughput that scales with storage.
    - **Provisioned:** Specify desired throughput independently of storage size.
4. **Access Control:**
    
    - Integrates with IAM and POSIX permissions for file access.
    - Supports encryption at rest and in transit using AWS KMS.
5. **Regional Availability:**
    
    - Files are stored redundantly across multiple AZs for high availability.
6. **Lifecycle Management:**
    
    - Move files not accessed for a specified time to **Infrequent Access (IA)** storage class to reduce costs.
7. **EFS Mount Targets:**
    
    - Creates **mount targets** in each AZ for access across VPC subnets.

---

#### **Common Use Cases**

1. **Shared File Systems:**
    
    - Access by multiple EC2 instances in the same or different AZs.
2. **Container Storage:**
    
    - Use with ECS, EKS, or Kubernetes for persistent shared storage.
3. **Big Data and Analytics:**
    
    - High throughput access for analytics workloads.
4. **Backup and Archive:**
    
    - Store and access backups with lifecycle management to IA.

---

#### **Key Exam Topics for EFS**

1. **File Storage vs. Block Storage:**
    
    - Know the differences between EBS and EFS and when to use each.
2. **Access and Permissions:**
    
    - Configure NFS mount points, security groups, and IAM policies.
3. **Performance Tuning:**
    
    - Understand performance and throughput modes (General Purpose vs. Max I/O, Bursting vs. Provisioned).
4. **Encryption and Security:**
    
    - Use KMS for encryption and understand IAM for access control.
5. **High Availability and Scalability:**
    
    - EFS is multi-AZ and automatically scales; know how this impacts use cases.
6. **Cost Management:**
    
    - Leverage lifecycle management to move unused files to Infrequent Access.

---

### **Comparison of EBS vs. EFS**

|Feature|EBS|EFS|
|---|---|---|
|**Type**|Block Storage|File Storage|
|**Access**|Single EC2 instance (unless multi-attach)|Multiple EC2 instances|
|**Scalability**|Fixed size, manually resized|Automatically scales|
|**Performance**|High performance for single instance|High throughput for shared workloads|
|**Use Case**|Databases, boot volumes|Shared file systems, analytics|
|**Availability**|AZ-specific|Multi-AZ|
|**Pricing**|Per GB/month + IOPS (for SSD)|Pay per use (standard or IA storage)|
|**Encryption**|KMS integration|KMS integration|

---

### **Best Practices**

#### **EBS:**

1. Use **gp3** for cost-efficient SSD performance.
2. Regularly back up volumes using **snapshots**.
3. Monitor IOPS and throughput to avoid performance bottlenecks.
4. Encrypt sensitive data using KMS.

#### **EFS:**

1. Use **General Purpose** mode for most applications; switch to **Max I/O** for highly parallel workloads.
2. Configure lifecycle policies to save on costs by using **IA storage** for infrequently accessed files.
3. Leverage **VPC security groups** to restrict file system access.

---

### **Key Exam Tips**

1. **When to Use EBS vs. EFS:**
    
    - Use **EBS** for single-instance, high-performance block storage needs (e.g., databases).
    - Use **EFS** for shared, scalable storage for multiple EC2 instances (e.g., shared file systems).
2. **EBS Snapshots:**
    
    - Understand how incremental backups work and how to use snapshots for disaster recovery.
3. **EFS Performance and Lifecycle:**
    
    - Know the differences between performance modes and how to optimize storage costs using IA.
4. **Encryption:**
    
    - Be familiar with enabling and managing encryption for both EBS and EFS.
5. **Monitoring:**
    
    - Use CloudWatch to monitor EBS and EFS performance and costs.

---
### **Performance Tuning for AWS EBS and EFS**

---

### **Elastic Block Store (EBS) Performance Tuning**

#### **1. Choose the Right Volume Type**

EBS performance heavily depends on the volume type you select based on your workload:

- **General Purpose SSD (gp3):**
    - Baseline of 3,000 IOPS, with customizable IOPS (up to 16,000) and throughput (up to 1,000 MB/s).
    - Use for boot volumes, development/test environments, and general workloads.
- **Provisioned IOPS SSD (io2, io1):**
    - Designed for latency-sensitive, high IOPS applications like relational databases.
    - io2 offers higher durability (99.999%).
- **Throughput Optimized HDD (st1):**
    - Ideal for big data, data warehouses, and log processing with high throughput.
- **Cold HDD (sc1):**
    - Best for infrequently accessed data at the lowest cost.

---

#### **2. Optimize Volume Size**

- IOPS and throughput for **gp2** increase with volume size:
    - Up to **16,000 IOPS** for volumes ≥5,334 GiB.
- With **gp3**, you can independently adjust size, IOPS, and throughput.

---

#### **3. Leverage RAID Configurations**

- Use RAID for increased performance or reliability:
    - **RAID 0 (striping):** Combines multiple EBS volumes for higher IOPS and throughput.
    - **RAID 1 (mirroring):** Provides redundancy but doesn’t increase performance.

---

#### **4. Use EBS-Optimized Instances**

- Ensure your EC2 instance is **EBS-optimized** for dedicated bandwidth.
- Check instance documentation for supported throughput and IOPS.

---

#### **5. Monitor and Adjust Performance**

- Use **CloudWatch Metrics** to monitor:
    - `VolumeReadOps`, `VolumeWriteOps`, `VolumeQueueLength`.
    - Watch for high queue lengths or latency.
- Modify volume size, type, or IOPS using the **ModifyVolume** API without downtime.

---

#### **6. Manage Snapshots Effectively**

- Restore volumes from snapshots during off-peak hours to avoid performance degradation.
- If a volume is restored from a snapshot, initialize it fully using a `dd` or `fio` command for optimal performance.

---

#### **7. Partition Workloads**

- Spread high-throughput applications across multiple EBS volumes to avoid bottlenecks.

---

#### **8. Enable Multi-Attach (io1/io2 only)**

- For highly available, distributed applications, use **multi-attach** to allow multiple EC2 instances to access the same volume.

---

---

### **Elastic File System (EFS) Performance Tuning**

#### **1. Choose the Right Performance Mode**

- **General Purpose:**
    - Default mode, low latency.
    - Suitable for web servers, content management systems, and DevOps workflows.
- **Max I/O:**
    - Supports highly parallelized workloads (e.g., big data analysis, media processing).
    - Higher throughput but with slightly increased latency.

---

#### **2. Select the Appropriate Throughput Mode**

- **Bursting Throughput (Default):**
    - Scales with storage size.
    - Provides burst credits to handle short-term spikes.
    - Example: 1 TB file system provides 50 MB/s baseline throughput, with bursts up to 100 MB/s.
- **Provisioned Throughput:**
    - Specify throughput (up to 1 GB/s) independent of storage size.
    - Use for workloads with consistent high throughput needs.

---

#### **3. Optimize Access Patterns**

- Minimize cross-AZ latency by using **EFS mount targets** within the same AZ as your EC2 instances.
- Optimize file sizes to avoid unnecessary metadata operations for many small files.

---

#### **4. Use Lifecycle Management**

- Move infrequently accessed files to **EFS Infrequent Access (IA)** to reduce costs.
- Lifecycle policy automatically transitions files to IA based on the age of last access (7–90 days).

---

#### **5. Optimize File System Mounting**

- Use the **EFS mount helper** for enhanced performance and easier setup.
```bash
sudo mount -t efs -o tls fs-12345678:/ /mnt/efs

```    
    
- Use the `nconnect` option to improve performance by allowing multiple TCP connections.
    
```bash
sudo mount -t nfs4 -o nconnect=4 fs-12345678:/ /mnt/efs
```
    

---

#### **6. Monitor Performance Metrics**

- Use **CloudWatch Metrics**:
    - `BurstCreditBalance`: Ensure you're not exhausting credits in bursting mode.
    - `PercentIOLimit`: Monitor throughput relative to provisioned or bursting limits.

---

#### **7. Security Best Practices**

- Enable **encryption at rest and in transit** to minimize performance impact while securing data.
- Use fine-grained access controls (IAM and POSIX permissions) to avoid bottlenecks caused by unauthorized access attempts.

---

### **Comparison of EBS and EFS Performance Tuning**

| Feature               | EBS                                       | EFS                             |
| --------------------- | ----------------------------------------- | ------------------------------- |
| **Scaling**           | Manual resizing (gp3 allows tuning)       | Automatically scales with usage |
| **Concurrency**       | Single instance (or Multi-Attach for io2) | Multiple EC2 instances          |
| **Performance Modes** | Select volume type (gp3, io2, etc.)       | General Purpose, Max I/O        |
| **Throughput Modes**  | Based on IOPS and volume size             | Bursting, Provisioned           |
| **Monitoring Tools**  | CloudWatch Metrics                        | CloudWatch Metrics              |

---

### **Best Practices Summary**

1. **EBS:**
    
    - Use the right volume type (gp3 or io2 for high performance).
    - Monitor CloudWatch metrics for bottlenecks.
    - Optimize instance configuration (EBS-optimized instances).
2. **EFS:**
    
    - Choose appropriate performance and throughput modes.
    - Optimize for large files and minimize metadata overhead.
    - Use lifecycle management to save costs on infrequent access data.