### **AWS DataSync - Study Notes for SysOps Admin Exam**

---

### **1. What is AWS DataSync?**

AWS DataSync is a **managed data transfer service** that automates moving data between on-premises storage and AWS, or between AWS services. It handles large-scale data migrations, data processing workflows, and backup/archiving tasks. preserves meta data and file permissions   

---

### **2. Key Features**

1. **Automated Transfers:**
    
    - Automates scheduling, monitoring, and scaling data transfers.
2. **High-Speed Transfers:**
    
    - Accelerates data movement, up to **10 times faster** than open-source tools.
3. **Data Validation:**
    
    - Ensures data integrity during transfers by performing checksums.
4. **Supported Storage Locations:**
    
    - **On-Premises to AWS:** Connect to NFS, SMB file systems.
    - **AWS to AWS:** Transfer between Amazon S3, Amazon EFS, and Amazon FSx.
5. **Incremental Transfers:**
    
    - Transfers only changed data, reducing costs and time.
6. **Data Encryption:**
    
    - Encrypts data in transit using **TLS**.

---

### **3. Use Cases**

1. **Large-Scale Data Migration:**
    
    - Move petabytes of data from on-premises storage to AWS.
2. **Backup and Archival:**
    
    - Automate backups of on-premises data to AWS storage services like S3 and Glacier.
3. **Disaster Recovery:**
    
    - Sync data between AWS regions for redundancy.
4. **Hybrid Workloads:**
    
    - Keep data synchronized between on-premises environments and AWS.

---

### **4. Integration with AWS Services**

- **Amazon S3:** Store files in buckets for analytics, backup, or archiving.
- **Amazon EFS:** Transfer file system data to and from EFS.
- **Amazon FSx:** Sync data to FSx for Lustre or Windows File Server.

---

### **5. Key Components**

1. **DataSync Agent:**
    
    - A virtual appliance deployed on-premises to connect local storage systems with AWS.
2. **Task:**
    
    - A transfer job specifying source, destination, and configurations.
3. **Location:**
    
    - Defines the source and destination endpoints.
4. **Task Execution:**
    
    - The actual process of transferring data according to the task configuration.

---

### **6. Best Practices**

1. **Monitor Transfers:**
    
    - Use **Amazon CloudWatch** to monitor DataSync task performance and troubleshoot issues.
2. **Optimize Bandwidth:**
    
    - Use task bandwidth throttling to avoid network congestion.
3. **Data Validation:**
    
    - Enable data integrity checks to ensure accurate transfers.
4. **Use IAM Roles:**
    
    - Grant minimal permissions required for DataSync to access AWS resources.

---

### **7. Key Exam Tips**

1. **DataSync vs. AWS Transfer Family:**
    
    - DataSync is for large-scale migrations and hybrid workflows.
    - Transfer Family supports file transfers using FTP, SFTP, or FTPS.
2. **Supported Storage:**
    
    - Know which on-premises and AWS services are compatible with DataSync (e.g., NFS, SMB, S3, EFS).
3. **Data Validation:**
    
    - Understand that checksum validation ensures data accuracy during transfers.
4. **Encryption:**
    
    - DataSync encrypts data in transit, but storage encryption depends on the target service (e.g., S3 bucket policies).

---

---

### **AWS Backup - Study Notes for SysOps Admin Exam**

---

### **1. What is AWS Backup?**

AWS Backup is a centralized, fully managed service that automates and orchestrates backups across multiple AWS services, ensuring compliance and streamlining disaster recovery.

---

### **2. Key Features**

1. **Centralized Management:**
    
    - Manage backups for multiple AWS services from a single dashboard.
2. **Backup Policies:**
    
    - Define backup rules for retention, frequency, and destinations.
3. **Service Integration:**
    
    - Supports services like EC2, EBS, RDS, DynamoDB, EFS, FSx, and more.
4. **Cross-Region and Cross-Account Backups:**
    
    - Automate backups to another region or account for disaster recovery.
5. **Backup Vaults:**
    
    - Securely store backups with encryption and access controls.
6. **Compliance and Auditing:**
    
    - Monitor backup activity and enforce policies using **AWS Backup Audit Manager**.

---

### **3. Use Cases**

1. **Disaster Recovery:**
    
    - Create cross-region backups to ensure data redundancy.
2. **Compliance:**
    
    - Automate retention policies to meet regulatory requirements.
3. **Centralized Backup Management:**
    
    - Replace service-specific backup mechanisms with AWS Backup for consistency.
4. **Data Retention:**
    
    - Use long-term retention policies for data archival.

---

### **4. Supported AWS Services**

- **Compute:** EC2, EBS
- **Database:** RDS (including Aurora), DynamoDB
- **Storage:** S3 (via DataSync), EFS, FSx for Lustre/Windows
- **Other:** Storage Gateway, Amazon VMs on Outposts

---

### **5. Key Components**

1. **Backup Plan:**
    
    - A set of rules defining what to back up, how often, and how long to retain backups.
2. **Backup Vault:**
    
    - A secure storage container for backups, supporting encryption and IAM policies.
3. **Recovery Point:**
    
    - The specific instance of data backed up at a given time.
4. **IAM Roles:**
    
    - Control who can create, delete, or restore backups.

---

### **6. Best Practices**

1. **Define Backup Policies:**
    
    - Standardize backup frequency and retention using AWS Backup Plans.
2. **Secure Backups:**
    
    - Use **KMS encryption** for data at rest.
    - Apply strict access controls on backup vaults.
3. **Cross-Region Backups:**
    
    - Enable automatic replication to another region for disaster recovery.
4. **Monitor Backup Activity:**
    
    - Use CloudWatch and AWS Backup Audit Manager to track compliance.
5. **Test Restores:**
    
    - Regularly test backup restores to validate data integrity.

---

### **7. AWS Backup vs. Service-Specific Backups**

|Feature|AWS Backup|Service-Specific Backup|
|---|---|---|
|**Management**|Centralized|Per service|
|**Automation**|Automated policies|Manual or semi-automated|
|**Cross-Region Backups**|Supported|Limited|
|**Compliance Tracking**|Audit Manager integration|None|

---

### **8. Key Exam Tips**

1. **Service Integration:**
    
    - Understand which AWS services integrate with AWS Backup.
2. **Backup Vaults:**
    
    - Know how backup vaults secure and isolate backups using encryption and IAM policies.
3. **Cross-Region and Cross-Account Backups:**
    
    - Be familiar with how to configure these features for disaster recovery.
4. **Monitoring:**
    
    - Use AWS Backup Audit Manager to track policy compliance.
5. **Cost Management:**
    
    - Understand the pricing model (storage costs, data transfer for cross-region backups).