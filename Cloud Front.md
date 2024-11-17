
### **Amazon CloudFront Notes for SysOps Admin Exam**

---

### **1. Introduction to CloudFront**

1. **What is CloudFront?**
    
    - Amazon CloudFront is a **Content Delivery Network (CDN)** that accelerates the delivery of content (e.g., websites, videos, APIs) to users by caching content in a global network of edge locations.
2. **Primary Purpose:**
    
    - Deliver content with **low latency** and **high transfer speeds** by serving it from the edge location closest to the user.
    - Reduces load on origin servers and improves performance.
3. **How It Works:**
    
    - Content is fetched from the **origin server** (e.g., S3, HTTP server) and cached at edge locations.
    - Subsequent requests are served directly from the cache until the cache expires or is invalidated.

---

### **2. CloudFront Distributions**

1. **What is a Distribution?**
    
    - A configuration entity that tells CloudFront how to serve your content.
2. **Types of Distributions:**
    
    - **Web Distributions:**
        - Used for websites, APIs, and other HTTP/HTTPS content delivery.
    - **RTMP Distributions:**
        - Used for streaming media via Adobe's Real-Time Messaging Protocol (RTMP).
        - **Note:** RTMP is deprecated and may not be relevant in most scenarios.
3. **Key Configuration Options:**
    
    - Specify **origin servers**.
    - Define **cache behaviors** for content.
    - Set up **security policies**, such as SSL/TLS.
    - Enable logging and monitoring.

---

### **3. Origins**

1. **Supported Origin Types:**
    
    - **Amazon S3 Buckets:**
        - Use S3 to host static websites or other objects.
    - **HTTP Servers:**
        - Custom origins such as on-premises servers or EC2 instances.
    - **Media Services:**
        - AWS MediaStore and AWS Elemental MediaPackage for video streaming.
2. **Origin Settings:**
    
    - Specify origin domain name or bucket.
    - Configure origin paths to fetch specific content.
    - Set headers for custom caching rules.

---

### **4. Cache Behavior**

1. **What is Cache Behavior?**
    
    - Defines how CloudFront handles requests based on **URL patterns**.
2. **Key Cache Behavior Settings:**
    
    - **Path Pattern:**
        - Match specific URLs (e.g., `/images/*` for images).
    - **Allowed HTTP Methods:**
        - GET, POST, DELETE, etc., for dynamic content.
    - **Viewer Protocol Policy:**
        - Redirect HTTP to HTTPS or enforce HTTPS-only access.
    - **Object Caching:**
        - Set Time-to-Live (TTL) for cached content.
    - **Query String Forwarding:**
        - Forward query strings to the origin for dynamic content requests.
3. **Default Cache Behavior:**
    
    - Acts as a catch-all for requests not matching specific path patterns.

---

### **5. Security Features**

1. **Signed URLs and Signed Cookies:**
    
    - Restrict access to specific content.
    - Use case: Distribute private videos or documents.
2. **AWS WAF (Web Application Firewall):**
    
    - Protect CloudFront distributions from malicious traffic like SQL injection or cross-site scripting.
    - Define rules to allow, block, or monitor traffic.
3. **Access Controls:**
    
    - Use **Origin Access Control (OAC)** to restrict access to S3 buckets so content can only be fetched via CloudFront.
4. **TLS/SSL:**
    
    - Encrypt traffic between viewers and CloudFront using HTTPS.
    - Use custom SSL certificates from **AWS Certificate Manager (ACM)**.

---

### **6. Custom Domain Names**

1. **Why Use Custom Domains?**
    
    - Provide a professional URL instead of the default CloudFront domain (e.g., `d123abc.cloudfront.net`).
2. **Setup:**
    
    - Add a **CNAME record** in your DNS to point to the CloudFront distribution.
    - Example:
        ```bash
        www.example.com -> d123abc.cloudfront.net
```
        
3. **SSL/TLS Configuration:**
    
    - Use ACM to issue a certificate for your domain.
    - Enable HTTPS for secure content delivery.

---

### **7. Invalidation**

1. **What is Invalidation?**
    
    - Removes specific objects from CloudFront's cache, forcing it to fetch the updated content from the origin.
2. **Invalidation Process:**
    
    - Specify paths for invalidation (e.g., `/index.html` or `/images/*`).
    - Example (CLI):
        
    ```bash
    aws cloudfront create-invalidation \
	  --distribution-id EXAMPLE123 \
	  --paths "/index.html"

```
        
3. **Cost:**
    
    - First 1,000 invalidation paths per month are free; charges apply beyond that.

---

### **8. Logging and Monitoring**

1. **Access Logs:**
    
    - Enable logging to S3 for detailed insights into viewer requests.
2. **CloudWatch Metrics:**
    
    - Monitor performance and usage metrics:
        - Requests
        - Cache hit/miss ratios
        - Error rates
        - Bandwidth
3. **Real-Time Metrics:**
    
    - Use real-time CloudWatch metrics for near-instantaneous performance insights.

---

### **9. Use Cases**

1. **Dynamic Content Delivery:**
    
    - Accelerate APIs and personalized web content.
2. **Static Content Delivery:**
    
    - Distribute assets like CSS, JavaScript, and images globally.
3. **Video Streaming:**
    
    - Use HLS, DASH, or CMAF protocols with AWS Media Services for live or on-demand video.
4. **Reducing Origin Load:**
    
    - Cache frequently accessed content at edge locations to minimize requests to origin servers.
5. **DDoS Protection:**
    
    - Use AWS Shield and AWS WAF with CloudFront for enhanced protection against DDoS attacks.

---

### **Key Exam Topics**

1. **Understanding Core Features:**
    
    - Know the difference between web and RTMP distributions.
    - Understand how CloudFront integrates with origins like S3 and HTTP servers.
2. **Security:**
    
    - Be familiar with signed URLs, signed cookies, AWS WAF, and TLS/SSL.
3. **Caching and Behaviors:**
    
    - Configure cache behaviors with path patterns and caching rules.
4. **Invalidation:**
    
    - Know when and how to invalidate cached objects.
5. **Custom Domain Names:**
    
    - Be able to set up custom domains and configure SSL certificates.
6. **Monitoring:**
    
    - Know how to enable logging and use CloudWatch metrics to analyze performance.
7. **Cost Considerations:**
    
    - Understand the pricing model for data transfer, requests, and invalidations.