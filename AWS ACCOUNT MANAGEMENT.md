### **Comprehensive AWS SysOps Admin Study Guide**

---

### **1. AWS Account Management**

#### **Account Structure**

1. **Root User:**
    
    - Created during account signup with full access to all AWS resources.
    - **Best Practices:**
        - Use root user only for account setup and billing tasks.
        - Enable **Multi-Factor Authentication (MFA)** for added security.
2. **IAM Users:**
    
    - Created to provide individual access to AWS resources.
    - Managed through IAM policies.
    - **Best Practices:**
        - Use IAM groups to assign permissions to users collectively.
        - Rotate access keys and use temporary credentials where possible.
3. **IAM Roles:**
    
    - Temporary access to resources without needing long-term credentials.
    - Commonly used for:
        - Applications (e.g., EC2 instances accessing S3).
        - Cross-account access.

---

#### **Billing and Cost Management**

1. **Billing Dashboard:**
    
    - View and manage monthly charges, usage, and trends.
2. **AWS Budgets:**
    
    - Set cost or usage limits with automatic notifications (e.g., alerts via SNS).
3. **Cost Explorer:**
    
    - Analyze historical and current cost trends.
    - Identify unused or underutilized resources to optimize costs.
4. **Billing Alarms:**
    
    - Use CloudWatch metrics to monitor charges in real-time.
    - Example:
    ```bash
aws cloudwatch put-metric-alarm --alarm-name BillingAlarm --metric-name EstimatedCharges --namespace AWS/Billing --statistic Maximum --period 86400 --threshold 100 --comparison-operator GreaterThanThreshold --evaluation-periods 1 --actions-enabled

```
        
5. **Best Practices:**
    
    - Consolidate accounts using **AWS Organizations**.
    - Use **Savings Plans** or **Reserved Instances** for predictable workloads.
    - Enable **Cost and Usage Reports** for granular insights.

---

#### **AWS Organizations**

1. **Overview:**
    
    - Manage multiple AWS accounts centrally.
    - Features:
        - Consolidated billing.
        - Policy-based account management via Service Control Policies (SCPs).
2. **Key Components:**
    
    - **Master Account:** Manages member accounts.
    - **Organizational Units (OUs):** Logical groupings for hierarchical management.
3. **Best Practices:**
    
    - Use SCPs to enforce security and compliance.
    - Organize accounts by environment (e.g., Production, Development).

---

#### **Service Quotas and Limits**

1. **Service Quotas:**
    
    - Limits on resource usage (e.g., EC2 instances per region).
    - Request increases via the **Service Quotas Dashboard** or Support Ticket.
2. **Monitoring:**
    
    - Use CloudWatch metrics to track resource usage and avoid hitting limits.
3. **Best Practices:**
    
    - Monitor quota usage proactively.
    - Request quota increases ahead of anticipated workload spikes.

---

#### **Security Best Practices**

1. **IAM Policies:**
    
    - Follow the **principle of least privilege**.
    - Define granular access using managed or custom policies.
2. **MFA:**
    
    - Require MFA for root and privileged users.
3. **Account Security:**
    
    - Enable **AWS CloudTrail** for logging API activity.
    - Use **AWS Config** to monitor resource compliance.

---

#### **Resource and Tag Management**

1. **Tags:**
    
    - Key-value pairs for organizing and tracking resources.
    - Example:
        - `Key: Environment, Value: Production`
        - `Key: Owner, Value: DevOps`
2. **Benefits:**
    
    - Cost allocation and tracking.
    - Automation (e.g., shutting down non-production resources).
3. **Best Practices:**
    
    - Establish a **tagging policy**.
    - Use **AWS Tag Editor** for centralized management.

---

### **2. Control Tower**

1. **Overview:**
    
    - Simplifies the setup and governance of multi-account environments using AWS Organizations.
2. **Key Features:**
    
    - **Landing Zone:** Pre-configured accounts and guardrails.
    - **Guardrails:** Policies for security and compliance.
3. **Best Practices:**
    
    - Use Control Tower to standardize account creation.
    - Enable mandatory guardrails for critical environments.

---

### **3. AWS Service Catalog**

1. **Overview:**
    
    - Centralized repository for deploying pre-approved AWS resources.
2. **Use Cases:**
    
    - Standardize infrastructure across teams.
    - Enforce compliance with organizational policies.
3. **Best Practices:**
    
    - Keep portfolios updated with the latest configurations.
    - Limit access to approved templates.

---

### **4. Cost Explorer**

1. **Overview:**
    
    - Analyze historical and forecasted costs.
2. **Features:**
    
    - Filter by service, account, or tag.
    - Visualize trends to identify savings opportunities.
3. **Best Practices:**
    
    - Regularly review spending to optimize costs.
    - Use Savings Plans and Reserved Instances for predictable workloads.

---

### **5. Compute Optimizer**

1. **Overview:**
    
    - Provides recommendations for optimizing EC2 instances, Auto Scaling Groups, and Lambda functions.
2. **Features:**
    
    - Identify underutilized or overprovisioned resources.
    - Optimize costs by downsizing or right-sizing resources.
3. **Best Practices:**
    
    - Regularly review Compute Optimizer reports.
    - Implement recommendations for cost savings and performance.

---

### **6. Cost and Usage Reports**

1. **Overview:**
    
    - Detailed reports providing granular insights into AWS usage and costs.
2. **Use Cases:**
    
    - Allocate costs by team or project.
    - Integrate with analytics tools like QuickSight for custom dashboards.
3. **Best Practices:**
    
    - Enable reports to track resource costs over time.
    - Use tags to filter and organize data.

---

### **7. AWS Budgets**

1. **Overview:**
    
    - Create budgets for cost, usage, or Reserved Instance/Savings Plan utilization.
2. **Alerts:**
    
    - Notify via SNS when thresholds are exceeded.
3. **Best Practices:**
    
    - Set proactive budgets for team or project-level spending.
    - Regularly review budget thresholds.

---

### **Practical Scenarios**

1. **Tagging and Cost Allocation:**
    
    - Use tags like `Environment` and `Owner` to track resource usage by team.
2. **Cost Control:**
    
    - Set up **billing alarms** and use **Cost Explorer** to optimize costs.
3. **Account Governance:**
    
    - Use **Control Tower** and **AWS Organizations** to manage multi-account setups.

---

### **Key Exam Tips**

1. **Account and Cost Management:**
    
    - Understand IAM structure, root user restrictions, and consolidated billing.
    - Be familiar with Cost Explorer, Compute Optimizer, and Budgets.
2. **Tagging and Resource Management:**
    
    - Know how to use tags for tracking and automation.
3. **Multi-Account Management:**
    
    - Use AWS Organizations and SCPs effectively.
4. **Cost Optimization:**
    
    - Recognize when to use Savings Plans, Reserved Instances, or Compute Optimizer.
5. **Control Tower and Service Catalog:**
    
    - Understand their role in standardizing account setup and resource deployment.

### **AWS Reserved Instances (RIs) - Study Notes for SysOps Admin Exam**

---

### **1. What Are Reserved Instances?**

Reserved Instances (RIs) provide **cost savings** for EC2 instances by committing to a specific instance type, region, and term length. They are ideal for predictable workloads.

- **Savings:** Up to **75%** compared to On-Demand pricing.
- **Commitment:** Typically for 1-year or 3-year terms.
- **Flexibility:** Convertible RIs offer flexibility in changing instance types or sizes.

---

### **2. Types of Reserved Instances**

1. **Standard Reserved Instances:**
    
    - Offer the highest discount (up to 75%).
    - Fixed to a specific instance type, region, and availability zone.
    - Cannot be modified, but you can sell unused RIs on the **AWS Reserved Instance Marketplace**.
2. **Convertible Reserved Instances:**
    
    - Slightly lower discount (up to 54%).
    - Allows you to change the instance family, size, OS, or tenancy during the term.
    - Useful for evolving workloads.
3. **Scheduled Reserved Instances:**
    
    - Reserved for specific time windows.
    - Useful for workloads that run periodically (e.g., nightly data processing).

---

### **3. Payment Options**

1. **All Upfront (AURI):**
    
    - Pay the full cost upfront for maximum savings.
2. **Partial Upfront (PURI):**
    
    - Pay part upfront, with the remaining cost spread over the term.
3. **No Upfront (NURI):**
    
    - No upfront payment, but savings are less compared to AURI or PURI.

---

### **4. Key Features of Reserved Instances**

1. **Scope:**
    
    - **Regional:** Discount applies across all Availability Zones (AZs) in a region.
    - **Zonal:** Tied to a specific AZ and provides capacity reservation.
2. **Instance Attributes:**
    
    - RIs are specific to:
        - **Instance family** (e.g., t3, m5, c5).
        - **Size** (e.g., t3.micro, m5.large).
        - **Operating System** (e.g., Linux, Windows).
        - **Tenancy** (Shared or Dedicated).
3. **Modifications:**
    
    - Standard RIs can’t be modified, but Convertible RIs allow flexibility.
    - Both can adjust AZ or switch between Regional and Zonal scopes (if supported).

---

### **5. Use Cases**

1. **Steady-State Workloads:**
    
    - Applications with predictable usage patterns (e.g., always-on web servers, databases).
2. **Critical Applications:**
    
    - Workloads requiring guaranteed capacity in specific AZs (use Zonal RIs).
3. **Cost Optimization:**
    
    - For workloads with long-term stability, RIs provide significant savings.
4. **Dynamic Workloads:**
    
    - Use Convertible RIs if you anticipate changing instance types.

---

### **6. Monitoring and Managing RIs**

1. **AWS Cost Explorer:**
    
    - Analyze RI utilization and coverage.
    - Identify unused or underutilized RIs.
2. **RI Marketplace:**
    
    - Sell unused Standard RIs to other AWS customers.
    - Useful if your needs change during the RI term.
3. **CloudWatch Alarms:**
    
    - Monitor instance usage to ensure full RI utilization.
4. **RI Reports:**
    
    - Use Cost and Usage Reports to track RI usage and savings.

---

### **7. Benefits of Reserved Instances**

1. **Cost Savings:**
    
    - Predictable workloads cost significantly less with RIs compared to On-Demand instances.
2. **Capacity Reservation (Zonal RIs):**
    
    - Guarantees instance availability in specific AZs.
3. **Predictable Billing:**
    
    - Lock in pricing for 1 or 3 years, reducing billing fluctuations.

---

### **8. Differences Between RIs and Savings Plans**

|Feature|Reserved Instances|Savings Plans|
|---|---|---|
|**Commitment**|Instance-specific|Flexible across EC2, Fargate, Lambda|
|**Flexibility**|Limited (Standard) or Moderate (Convertible)|High (covers multiple instance types, regions)|
|**Payment Options**|AURI, PURI, NURI|Same (AURI, PURI, NURI)|
|**Scope**|Instance-specific, Zonal or Regional|Regional|
|**Use Case**|Predictable, fixed workloads|Dynamic, flexible workloads|

---

### **9. Best Practices**

1. **Analyze Workloads:**
    
    - Use Cost Explorer to identify steady-state workloads suitable for RIs.
    - Ensure workloads match the attributes of the RI (e.g., instance type, size, region).
2. **Mix and Match:**
    
    - Combine On-Demand, Spot, and RIs to optimize costs while maintaining flexibility.
3. **Monitor Utilization:**
    
    - Regularly review RI coverage and utilization.
    - Address underutilized RIs by shifting workloads or selling them on the RI Marketplace.
4. **Use Convertible RIs for Evolving Workloads:**
    
    - If your instance needs may change, Convertible RIs offer flexibility.
5. **Consider Savings Plans:**
    
    - For greater flexibility, evaluate **Savings Plans** instead of RIs.

---

### **10. Exam Tips**

1. **RI Basics:**
    
    - Understand the types (Standard, Convertible, Scheduled) and their use cases.
2. **Payment Options:**
    
    - Be familiar with the difference between All Upfront, Partial Upfront, and No Upfront.
3. **Use Cases:**
    
    - Be able to identify workloads that benefit from RIs, such as steady-state applications.
4. **RI Monitoring:**
    
    - Know how to track RI utilization and cost savings using Cost Explorer and reports.
5. **Capacity Reservation:**
    
    - Remember that Zonal RIs provide reserved capacity, while Regional RIs do not.
6. **RI Marketplace:**
    
    - Be aware that Standard RIs can be sold in the marketplace if they are unused.

### **S3 Organizational ID (Org ID) - AWS SysOps Admin Exam Notes**

---

### **1. What is S3 Org ID?**

An **S3 Org ID** is a feature that allows you to manage access to S3 buckets across multiple accounts within an **AWS Organization**. By associating an S3 bucket policy with an AWS Organization’s **Org ID**, you can enforce consistent permissions for accounts in the organization, simplifying cross-account access management.

---

### **2. Key Features of S3 Org ID**

1. **Centralized Access Management:**
    
    - Allows administrators to manage S3 bucket access across multiple accounts within an AWS Organization.
2. **Simplified Policies:**
    
    - Use the Org ID in bucket policies instead of specifying individual account IDs.
3. **Dynamic Membership:**
    
    - Automatically applies bucket policies to new accounts added to the organization.
4. **Improved Security:**
    
    - Ensures that only accounts in your AWS Organization can access specified S3 buckets.

---

### **3. How S3 Org ID Works**

1. **Org ID Format:**
    
    - The Org ID is a unique identifier for an AWS Organization.
    - Example:
        `o-exampleorgid 
2. **Bucket Policy with Org ID:**
    
    - Use the `"aws:PrincipalOrgID"` condition key in the bucket policy to restrict access to accounts within your organization.
3. **Integration with AWS Organizations:**
    
    - The Org ID ensures that only accounts explicitly part of the organization can access the bucket, even if access keys or IAM roles are compromised.    
---
### **4. Bucket Policy Example**

The following bucket policy grants access only to accounts within the specified AWS Organization:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:*",
      "Resource": [
        "arn:aws:s3:::example-bucket",
        "arn:aws:s3:::example-bucket/*"
      ],
      "Condition": {
        "StringEquals": {
          "aws:PrincipalOrgID": "o-exampleorgid"
        }
      }
    }
  ]
}

```
- **Principal:** `*` allows all principals, but access is limited to those matching the Org ID condition.
- **Condition Key:** `aws:PrincipalOrgID` ensures the request comes from an account in the specified organization.

---

### **5. Use Cases**

1. **Cross-Account Access Control:**
    
    - Grant access to S3 buckets for all accounts in an AWS Organization without listing individual account IDs.
2. **Centralized Governance:**
    
    - Simplify policies for shared resources like data lakes or logging buckets.
3. **Dynamic Access Management:**
    
    - Automatically includes new accounts added to the organization.
4. **Enhanced Security for Shared Resources:**
    
    - Prevents external accounts from accessing the bucket, even if other IAM conditions are met.

---

### **6. Benefits**

1. **Simplified Administration:**
    
    - No need to update bucket policies when accounts are added or removed from the organization.
2. **Improved Scalability:**
    
    - Scales seamlessly as the organization grows.
3. **Increased Security:**
    
    - Restricts access to trusted accounts within the organization.
4. **Cost Efficiency:**
    
    - Reduces the overhead of managing individual cross-account permissions.

---

### **7. Best Practices**

1. **Use Org ID for Shared Buckets:**
    
    - For buckets accessed by multiple accounts, use Org ID in the policy to simplify access control.
2. **Monitor Bucket Access:**
    
    - Use **CloudTrail** and **S3 Server Access Logs** to monitor access requests and ensure compliance.
3. **Combine with SCPs:**
    
    - Use **Service Control Policies (SCPs)** to further restrict actions for accounts within the organization.
4. **Secure Root User:**
    
    - Ensure the root user of the master account in AWS Organizations has MFA enabled to secure Org ID management.

---

### **8. Limitations**

1. **AWS Organization Dependency:**
    
    - Only works for accounts that are part of an AWS Organization.
2. **Complex Conditions:**
    
    - Org ID policies may need to be combined with additional conditions (e.g., VPC Endpoint policies) for more granular control.
3. **Scope of Access:**
    
    - Cannot restrict access to individual accounts within the organization; access applies to all accounts under the Org ID.

---

### **9. Monitoring and Auditing Org ID Usage**

1. **CloudTrail Integration:**
    
    - Track API calls and ensure Org ID conditions are being used in bucket policies.
2. **AWS Config Rules:**
    
    - Use Config to enforce that S3 buckets must include `"aws:PrincipalOrgID"` in their policies.
3. **Access Analyzer:**
    
    - Review bucket policies to identify unintended public or cross-account access.

---

### **10. Key Exam Tips**

1. **Condition Key:**
    
    - Remember the `"aws:PrincipalOrgID"` condition key for restricting S3 bucket access to AWS Organization accounts.
2. **Policy Structure:**
    
    - Understand how to structure bucket policies using Org ID, including specifying actions, resources, and conditions.
3. **Integration with AWS Organizations:**
    
    - Be familiar with the relationship between S3 Org ID and AWS Organizations for cross-account resource sharing.
4. **Use Cases:**
    
    - Be prepared to identify scenarios where Org ID simplifies access control (e.g., shared data lakes, logging buckets).
5. **Monitoring:**
    
    - Know how to use AWS Config and CloudTrail to audit and enforce Org ID policies.