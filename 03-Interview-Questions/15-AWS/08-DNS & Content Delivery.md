# AWS DNS & Content Delivery Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Amazon Route 53, and why is it used?

**Answer**

Amazon Route 53 is AWS's highly available and scalable Domain Name System (DNS) web service. It translates domain names (such as `www.example.com`) into IP addresses and routes users to AWS or non-AWS resources.

Its primary functions include:

- Domain registration
- DNS management
- Traffic routing
- Health checking
- Failover routing

**Explanation**

Route 53 helps users access applications using domain names instead of IP addresses. It supports multiple routing policies to improve availability and performance.

**Where it is used in Production**

- Website hosting
- API endpoints
- Multi-region applications
- Disaster recovery
- Load-balanced applications

**Common Mistake**

Assuming Route 53 hosts websites. It only manages DNS resolution and routing.

---

### Question 2

**Question**

What is a Hosted Zone in Amazon Route 53?

**Answer**

A Hosted Zone is a container for DNS records that manages how traffic is routed for a specific domain.

There are two types:

- Public Hosted Zone
- Private Hosted Zone

**Explanation**

A Public Hosted Zone resolves internet-facing domain names, while a Private Hosted Zone provides DNS resolution only within one or more VPCs.

**Where it is used in Production**

- Public websites
- Internal enterprise applications
- Hybrid cloud environments

**Common Mistake**

Using a Public Hosted Zone for internal-only services.

---

### Question 3

**Question**

What are the common DNS record types in Route 53?

**Answer**

Common DNS records include:

- A Record
- AAAA Record
- CNAME
- MX
- TXT
- NS
- SOA
- Alias Record

**Explanation**

Each record type serves a different purpose. For example, an A Record maps a domain to an IPv4 address, while an Alias Record points to AWS resources without requiring an IP address.

**Where it is used in Production**

- Website routing
- Email configuration
- Domain verification
- AWS service integration

---

### Question 4

**Question**

What is an Alias Record in Route 53?

**Answer**

An Alias Record maps a domain name directly to supported AWS resources such as:

- Application Load Balancer
- CloudFront Distribution
- S3 Static Website
- API Gateway

**Explanation**

Unlike a CNAME record, Alias Records work at the root domain (example.com) and incur no additional Route 53 DNS query charges for supported AWS resources.

**Where it is used in Production**

- Root domain routing
- Load balancers
- CloudFront distributions
- Static websites

**Common Mistake**

Using a CNAME record for the root domain instead of an Alias Record.

---

### Question 5

**Question**

What are Route 53 Health Checks?

**Answer**

Health Checks monitor the availability of endpoints such as websites or APIs.

They periodically verify whether an endpoint is responding correctly.

**Explanation**

If a health check fails, Route 53 can automatically redirect traffic to healthy resources using supported routing policies.

**Where it is used in Production**

- High availability
- Disaster recovery
- Multi-region applications
- Automatic failover

**Common Mistake**

Creating health checks without configuring failover routing.

---

### Question 6

**Question**

What is Amazon CloudFront?

**Answer**

Amazon CloudFront is AWS's Content Delivery Network (CDN) that delivers content from edge locations located around the world.

**Explanation**

CloudFront caches static and dynamic content closer to users, reducing latency and improving application performance.

**Where it is used in Production**

- Static websites
- Media streaming
- APIs
- Software downloads
- Global web applications

**Common Mistake**

Assuming CloudFront permanently stores application data instead of caching it.

---

### Question 7

**Question**

How does Amazon CloudFront improve application performance?

**Answer**

CloudFront improves performance by:

- Caching content at edge locations
- Reducing latency
- Decreasing origin server load
- Serving users from the nearest edge location

**Explanation**

Instead of every request reaching the origin server, cached content is served directly from nearby edge locations.

**Where it is used in Production**

- Global websites
- Video streaming
- APIs
- Image delivery

---

### Question 8

**Question**

What is the relationship between Route 53 and CloudFront?

**Answer**

Route 53 resolves the domain name, while CloudFront delivers the content.

Typical flow:

User → Route 53 → CloudFront → Origin (S3, ALB, EC2)

**Explanation**

Route 53 handles DNS resolution, and CloudFront accelerates content delivery.

**Where it is used in Production**

Nearly every globally accessible AWS web application.

---

### Question 9

**Question**

What is the difference between a Public Hosted Zone and a Private Hosted Zone?

**Answer**

| Public Hosted Zone | Private Hosted Zone |
|--------------------|---------------------|
| Accessible from the internet | Accessible only within associated VPCs |
| Used for public websites | Used for internal applications |
| Public DNS resolution | Private DNS resolution |

**Explanation**

Choose the hosted zone type based on whether the application is public or internal.

**Where it is used in Production**

- Public websites
- Enterprise internal services

---

### Question 10

**Question**

Why is CloudFront commonly placed in front of an S3 bucket?

**Answer**

CloudFront caches objects stored in S3 and delivers them from edge locations.

Benefits include:

- Faster downloads
- Lower latency
- Reduced S3 requests
- Improved security

**Explanation**

Frequently requested objects are served directly from edge locations instead of the origin bucket.

**Where it is used in Production**

- Static websites
- Images
- Videos
- Downloads

---

### Question 11

**Question**

What happens if a Route 53 Health Check detects that an endpoint has failed?

**Answer**

If configured with Failover Routing, Route 53 automatically routes traffic to a healthy backup endpoint.

**Explanation**

Health checks improve application availability by avoiding failed resources.

**Where it is used in Production**

- Disaster recovery
- Multi-region applications
- High availability

---

### Question 12

**Question**

Why do global applications use Amazon CloudFront?

**Answer**

CloudFront provides:

- Lower latency
- Faster content delivery
- Reduced origin server load
- Better scalability
- Improved user experience

**Explanation**

Users receive content from nearby AWS edge locations rather than directly from the origin server.

**Where it is used in Production**

Most production web applications with global users.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your website is hosted in Mumbai, but users in Europe experience slow page loads. How would you improve performance?

**Answer**

Deploy Amazon CloudFront in front of the application.

**Explanation**

CloudFront caches content at edge locations close to European users, significantly reducing latency.

---

### Scenario 2

**Question**

Your primary web server becomes unavailable. How can Route 53 automatically redirect users to a standby server?

**Answer**

Configure:

- Route 53 Health Checks
- Failover Routing Policy
- Primary and secondary endpoints

**Explanation**

If the primary endpoint fails the health check, Route 53 automatically routes traffic to the healthy backup endpoint.

---

### Scenario 3

**Question**

Your company wants employees to access an internal application using a custom domain that should not be accessible from the internet. Which Route 53 feature would you use?

**Answer**

Private Hosted Zone.

**Explanation**

Private Hosted Zones provide DNS resolution only inside associated VPCs.

---

### Scenario 4

**Question**

A company wants users to access an Application Load Balancer using the root domain (`example.com`). Which DNS record should be created?

**Answer**

An Alias Record.

**Explanation**

Alias Records can point directly to AWS resources such as ALBs and support root domains.

---

### Scenario 5

**Question**

Users report intermittent website failures. How would you determine whether the problem is related to DNS or the application?

**Answer**

Check:

- Route 53 Health Checks
- DNS resolution
- CloudFront status
- ALB health
- Application logs
- EC2 health

**Explanation**

Separating DNS issues from application issues speeds up troubleshooting.

---

### Scenario 6

**Question**

A static website hosted in Amazon S3 receives millions of daily requests, increasing storage service costs. How would you optimize the architecture?

**Answer**

Place Amazon CloudFront in front of the S3 bucket.

**Explanation**

CloudFront serves cached content from edge locations, reducing requests to S3 and improving performance.

---

### Scenario 7

**Question**

A business wants users to be automatically directed to the nearest application endpoint in different AWS Regions. Which AWS service would help?

**Answer**

Amazon Route 53 using Latency-Based Routing.

**Explanation**

Latency-Based Routing directs users to the AWS Region with the lowest network latency.

---

### Scenario 8

**Question**

A website becomes inaccessible because the domain name no longer resolves correctly. What would you investigate first?

**Answer**

Verify:

- Hosted Zone configuration
- DNS records
- Domain registration
- Name Server (NS) records
- Alias or CNAME configuration

**Explanation**

Incorrect DNS configuration is one of the most common causes of website accessibility issues.

---

### Scenario 9

**Question**

Your application serves large images and videos to users worldwide. Which AWS service would improve download speed?

**Answer**

Amazon CloudFront.

**Explanation**

CloudFront caches media files at global edge locations, reducing latency and improving download performance.

---

### Scenario 10

**Question**

Your organization wants maximum availability for a production website hosted across multiple AWS Regions. How would you design the DNS solution?

**Answer**

Use:

- Amazon Route 53
- Health Checks
- Failover or Latency-Based Routing
- Amazon CloudFront
- Regional Application Load Balancers

**Explanation**

This architecture provides global traffic routing, automatic failover, lower latency, and high availability by directing users to healthy application endpoints.
