### **AWS Lambda Overview for SysOps Admin Exam**

---

### **What is AWS Lambda?**

AWS Lambda is a serverless compute service that runs code in response to events and automatically manages the compute resources for you. It allows you to focus on your application code without worrying about managing servers.

---

### **Core Concepts**

1. **Event-Driven Computing:**
    
    - Lambda functions are triggered by events from AWS services, such as S3, DynamoDB, API Gateway, and CloudWatch.
2. **Runtime Environments:**
    
    - Supports various programming languages (Python, Node.js, Java, Go, Ruby, .NET, etc.).
    - Custom runtimes can be created for unsupported languages.
3. **Execution Environment:**
    
    - Lambda runs in isolated environments called execution environments.
    - Functions share resources if re-used, optimizing performance.
4. **Pricing Model:**
    
    - Pay only for:
        - **Execution time:** Billed per millisecond.
        - **Requests:** First 1M requests are free.
    - Cost scales automatically with usage.

---

### **Key Features**

1. **Triggers and Event Sources:**
    
    - Direct Integration:
        - S3 (e.g., object uploads).
        - DynamoDB (stream changes).
        - API Gateway (HTTP triggers).
        - CloudWatch Logs and Events (monitoring/alerts).
    - Polling Sources:
        - SQS (standard and FIFO queues).
        - Kinesis streams.
2. **Execution Model:**
    
    - **Concurrency:** Number of instances of a function that can run simultaneously.
    - **Provisioned Concurrency:** Keeps functions "warm" to reduce latency for high-demand applications.
3. **Limits:**
    
    - **Memory:** 128 MB to 10 GB.
    - **Timeout:** Up to 15 minutes.
    - **Ephemeral Storage:** 512 MB (can be increased to 10 GB).
    - **Deployment Package Size:**
        - 50 MB (direct upload).
        - 250 MB (with layers or zipped in S3).
4. **Environment Variables:**
    
    - Securely pass configuration values to Lambda functions.
5. **Layers:**
    
    - Reusable packages for sharing libraries, dependencies, or code across multiple Lambda functions.
6. **VPC Integration:**
    
    - Functions can access resources in a VPC, such as RDS or ElastiCache.
    - Requires proper IAM permissions and configured subnets/security groups.

---

### **Key Components**

1. **Handler Function:**
    
    - Entry point for executing the Lambda function.
    - Receives event data and returns a response.
    
    Example (Python):
    ```python
    def lambda_handler(event, context):
	    print("Event: ", event)
	    return {"statusCode": 200, "body": "Hello, World!"}

```
2. **IAM Roles and Permissions:**
    
    - Lambda requires an **execution role** to interact with other AWS services.
    - Attach the necessary policies (e.g., `AmazonS3ReadOnlyAccess`).
3.  **CloudWatch Monitoring:**
    
    - Logs function execution, errors, and metrics.
    - Key Metrics:
        - **Invocations**
        - **Duration**
        - **Errors**
        - **Throttles**
        - **Concurrency**
4. **Dead Letter Queue (DLQ):**

    - Configured for asynchronous functions to handle failed invocations.
    - Supports SQS or SNS as targets.
---

### **Deployment and Updates**

1. **Code Deployment:**
    
    - Direct upload via the AWS Management Console or CLI.
    - Use S3 for larger deployments.
2. **Versioning:**
    
    - Immutable versions of Lambda functions.
    - `$LATEST` points to the most recent unpublished version.
3. **Aliases:**
    
    - Pointers to specific function versions.
    - Used for stable references (e.g., production vs staging environments).
4. **Blue/Green Deployments:**
    
    - Gradual traffic shifting with aliases to reduce deployment risks.

---

### **Monitoring and Troubleshooting**

1. **CloudWatch Logs:**
    
    - Automatically collects logs when enabled.
    - Use log groups to monitor and debug function executions.
2. **X-Ray Tracing:**
    
    - Provides end-to-end request tracing for analyzing performance and bottlenecks.
3. **Metrics and Alerts:**
    
    - Use CloudWatch Alarms to monitor metrics like error rates and throttling.
4. **Error Handling:**
    
    - **Retries:** Automatically retries asynchronous invocations twice.
    - **DLQ:** Stores failed events for manual processing.

---

### **Common Use Cases**

1. **File Processing:**
    
    - Triggered by S3 events (e.g., image resizing, log processing).
2. **Real-Time Data Processing:**
    
    - Processes streams from Kinesis or DynamoDB.
3. **API Backends:**
    
    - Serve HTTP requests via API Gateway.
4. **Serverless Automation:**
    
    - Automate operational tasks triggered by CloudWatch Events.
5. **Database Triggers:**
    
    - Respond to changes in DynamoDB tables.
6. **Event Notifications:**
    
    - Process SNS messages or queue tasks with SQS.

---

### **Best Practices**

1. **Optimize Cold Start:**
    
    - Use provisioned concurrency for critical functions.
    - Minimize initialization time by reusing libraries and resources.
2. **Use Layers:**
    
    - Share dependencies and reduce deployment size.
3. **Minimize Execution Time:**
    
    - Only load dependencies when needed.
    - Optimize algorithms and database queries.
4. **Secure Functions:**
    
    - Follow the principle of least privilege for IAM roles.
    - Encrypt sensitive data with KMS.
5. **Test Locally:**
    
    - Use tools like AWS SAM or LocalStack for local testing.
6. **Log Analysis:**
    
    - Use centralized tools (e.g., CloudWatch Logs Insights) for monitoring logs at scale.

---

### **Key Exam Topics**

1. **Event Sources:**
    
    - Be familiar with all trigger sources (e.g., S3, DynamoDB, API Gateway).
2. **IAM Role Configuration:**
    
    - Understand how to grant permissions for Lambda functions to interact with AWS services.
3. **Error Handling:**
    
    - Know the retry behavior and how DLQs work for failed invocations.
4. **Performance Metrics:**
    
    - Monitor concurrency, throttling, and error rates in CloudWatch.
5. **Security:**
    
    - Encrypt environment variables and secure roles.
    - Lambda functions accessing VPC resources require appropriate subnet and security group configuration.
6. **Deployment Strategies:**
    
    - Versioning and aliasing for rolling updates.
7. **Integration with VPC:**
    
    - Understand how Lambda interacts with private resources inside a VPC.

---

### **CLI Commands**

1. Deploy Lambda Function

```bash 
aws lambda create-function \
  --function-name MyFunction \
  --runtime python3.9 \
  --role arn:aws:iam::123456789012:role/MyLambdaRole \
  --handler lambda_function.lambda_handler \
  --zip-file fileb://function.zip

```

2.  Invoke Function

```bash
aws lambda invoke \
  --function-name MyFunction \
  output.json

```

3. Update Code

```bash 
aws lambda update-function-code \
  --function-name MyFunction \
  --zip-file fileb://function.zip

```

4. Monitor Metrics

	```bash
aws cloudwatch get-metric-statistics \
  --metric-name Duration \
  --namespace AWS/Lambda \
  --dimensions Name=FunctionName,Value=MyFunction \
  --start-time 2024-11-15T00:00:00Z \
  --end-time 2024-11-16T00:00:00Z \
  --period 300 \
  --statistics Average

```
