# AWS Networking Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Amazon VPC, and why is it used?

**Answer**

Amazon Virtual Private Cloud (VPC) is a logically isolated virtual network where you can launch AWS resources securely.

It allows you to:

- Define your own IP address range (CIDR)
- Create public and private subnets
- Configure routing
- Control inbound and outbound traffic
- Connect securely to on-premises networks

**Explanation**

A VPC provides complete network isolation within AWS. Every production workload runs inside a VPC, making it the foundation of AWS networking.

**Where it is used in Production**

- Hosting web applications
- Multi-tier architectures
- Kubernetes clusters (EKS)
- Databases
- Hybrid cloud deployments

**Common Mistake**

Thinking a VPC automatically provides internet access. Internet connectivity must be configured using an Internet Gateway and proper routing.

---

### Question 2

**Question**

What is the difference between a Public Subnet and a Private Subnet?

**Answer**

A Public Subnet has a route to an Internet Gateway, allowing internet connectivity.

A Private Subnet does not have a direct route to the Internet Gateway and is typically accessed through a NAT Gateway or VPN.

**Explanation**

Public subnets host internet-facing resources like web servers or load balancers, while private subnets host databases and backend services.

**Where it is used in Production**

- Public Subnet: ALB, Bastion Host, Web Servers
- Private Subnet: Databases, Application Servers, Kubernetes Worker Nodes

**Common Mistake**

Launching a server in a public subnet without assigning a public IP and expecting internet access.

---

### Question 3

**Question**

What is a Route Table in AWS?

**Answer**

A Route Table contains routing rules that determine where network traffic from a subnet is directed.

**Explanation**

Each subnet is associated with a Route Table that defines paths to destinations such as:

- Local VPC
- Internet Gateway
- NAT Gateway
- VPN Gateway
- VPC Peering

**Where it is used in Production**

- Internet access
- Private networking
- Hybrid connectivity
- Multi-VPC architectures

**Common Mistake**

Forgetting to associate the correct Route Table with a subnet.

---

### Question 4

**Question**

What is an Internet Gateway (IGW)?

**Answer**

An Internet Gateway enables communication between a VPC and the public internet.

**Explanation**

An IGW is attached to a VPC and works with Route Tables and public IP addresses to provide internet connectivity.

**Where it is used in Production**

- Public web servers
- Bastion hosts
- Internet-facing load balancers

**Common Mistake**

Attaching an IGW but forgetting to add a default route (0.0.0.0/0) in the Route Table.

---

### Question 5

**Question**

What is a NAT Gateway, and why is it used?

**Answer**

A NAT Gateway allows instances in private subnets to access the internet while preventing inbound internet connections.

**Explanation**

Private EC2 instances often require internet access for software updates or downloading packages. A NAT Gateway provides outbound-only internet connectivity.

**Where it is used in Production**

- Private application servers
- Kubernetes worker nodes
- Backend services

**Common Mistake**

Using an Internet Gateway instead of a NAT Gateway for private subnet instances.

---

### Question 6

**Question**

What are Security Groups?

**Answer**

Security Groups are stateful virtual firewalls that control inbound and outbound traffic for AWS resources.

**Explanation**

Security Groups evaluate only Allow rules. If inbound traffic is allowed, the corresponding outbound response is automatically permitted because they are stateful.

**Where it is used in Production**

- EC2
- RDS
- ECS
- EKS
- Load Balancers

**Common Mistake**

Trying to configure Deny rules, which Security Groups do not support.

---

### Question 7

**Question**

What are Network ACLs?

**Answer**

Network ACLs (NACLs) are stateless firewalls that operate at the subnet level.

**Explanation**

Unlike Security Groups, NACLs support both Allow and Deny rules, and inbound and outbound rules must be configured separately.

**Where it is used in Production**

- Additional subnet-level security
- Blocking specific IP ranges
- Compliance requirements

**Common Mistake**

Forgetting that return traffic must be explicitly allowed because NACLs are stateless.

---

### Question 8

**Question**

What is the difference between Security Groups and Network ACLs?

**Answer**

| Security Groups | Network ACLs |
|-----------------|--------------|
| Instance-level firewall | Subnet-level firewall |
| Stateful | Stateless |
| Allow rules only | Allow and Deny rules |
| Return traffic automatically allowed | Return traffic must be explicitly allowed |

**Explanation**

Security Groups protect individual resources, while NACLs provide an additional security layer for entire subnets.

**Where it is used in Production**

Both are commonly used together to implement defense-in-depth security.

---

### Question 9

**Question**

What is an Elastic Network Interface (ENI)?

**Answer**

An ENI is a virtual network interface that can be attached to an EC2 instance.

**Explanation**

An ENI contains:

- Private IP addresses
- Public IP (optional)
- Security Groups
- MAC Address

It can be detached from one instance and attached to another.

**Where it is used in Production**

- High availability
- Network appliances
- Failover solutions
- Multi-network configurations

**Common Mistake**

Confusing ENIs with Elastic IP addresses.

---

### Question 10

**Question**

Can an EC2 instance in a private subnet access the internet?

**Answer**

Yes.

The instance can access the internet through a NAT Gateway, provided the Route Table points to the NAT Gateway.

**Explanation**

Private instances do not communicate directly with the Internet Gateway. Outbound internet traffic flows through the NAT Gateway.

**Where it is used in Production**

- Backend applications
- Patch management
- Software installation
- Container image downloads

---

### Question 11

**Question**

Why do production architectures use multiple Availability Zones for networking?

**Answer**

Using multiple Availability Zones improves high availability and fault tolerance.

**Explanation**

Resources are distributed across multiple AZs so that if one AZ experiences an outage, applications continue running in another AZ.

**Where it is used in Production**

- Highly available web applications
- Databases
- Auto Scaling Groups
- Kubernetes clusters

**Common Mistake**

Deploying all resources into a single Availability Zone.

---

### Question 12

**Question**

How does traffic flow from a user's browser to a public EC2 instance?

**Answer**

Typical flow:

1. User accesses the public IP or DNS.
2. Traffic reaches the Internet Gateway.
3. The Route Table forwards traffic to the public subnet.
4. Security Group allows the request.
5. The EC2 instance processes the request and returns the response.

**Explanation**

Every networking component plays a role in enabling secure communication.

**Where it is used in Production**

Understanding this flow is essential for troubleshooting connectivity issues.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

You launched an EC2 instance in a public subnet, but you cannot SSH into it. What would you check?

**Answer**

Check:

- Security Group allows TCP port 22
- Public IP is assigned
- Internet Gateway is attached
- Route Table has 0.0.0.0/0 pointing to the IGW
- Network ACL allows SSH traffic
- SSH key pair is correct

**Explanation**

Missing any one of these components can prevent SSH access.

---

### Scenario 2

**Question**

An EC2 instance in a private subnet cannot download software updates. What is the likely cause?

**Answer**

The subnet is missing a properly configured NAT Gateway or Route Table entry.

**Explanation**

Private instances require a NAT Gateway for outbound internet access.

---

### Scenario 3

**Question**

A web application is publicly accessible, but the database should never be exposed to the internet. How would you design the network?

**Answer**

- Web servers in public subnets
- Database in private subnets
- Internet Gateway for public subnets
- NAT Gateway for private subnet outbound access
- Security Groups allowing database access only from application servers

**Explanation**

This is the standard multi-tier AWS architecture used in production.

---

### Scenario 4

**Question**

Users report that a website hosted on EC2 is unreachable after deployment. How would you troubleshoot?

**Answer**

Verify:

- EC2 instance is running
- Security Group allows HTTP/HTTPS
- Internet Gateway exists
- Route Table is correct
- Public IP or Load Balancer is configured
- Web server (Apache/Nginx) is running

**Explanation**

Connectivity issues often result from missing routing or firewall rules.

---

### Scenario 5

**Question**

A private application server suddenly loses internet access after infrastructure changes. What would you investigate?

**Answer**

Check:

- NAT Gateway health
- Route Table entries
- Subnet associations
- Security Groups
- Network ACLs

**Explanation**

Routing changes are a common cause of connectivity failures in production.

---

### Scenario 6

**Question**

A Security Group allows HTTP traffic, but users still cannot access the application. What else could block the traffic?

**Answer**

Possible causes include:

- Network ACL Deny rules
- Missing Internet Gateway
- Incorrect Route Table
- Application not listening on port 80
- EC2 instance stopped

**Explanation**

Security Groups are only one component of the networking path.

---

### Scenario 7

**Question**

A company wants to block traffic from a specific IP range. Would you use Security Groups or Network ACLs?

**Answer**

Use a Network ACL because it supports explicit Deny rules.

**Explanation**

Security Groups cannot deny traffic; they only allow traffic.

---

### Scenario 8

**Question**

You need to move a network configuration quickly from one EC2 instance to another during failover. Which AWS networking feature would help?

**Answer**

Elastic Network Interface (ENI).

**Explanation**

An ENI can be detached from one instance and attached to another, preserving IP configuration and Security Groups.

---

### Scenario 9

**Question**

Your application servers need internet access for package updates but must not accept inbound internet traffic. How would you configure the network?

**Answer**

- Place servers in private subnets.
- Configure a NAT Gateway in a public subnet.
- Add a Route Table entry pointing to the NAT Gateway.
- Do not assign public IP addresses.

**Explanation**

This design provides secure outbound internet access without exposing the servers.

---

### Scenario 10

**Question**

After migrating an application to AWS, users experience intermittent connectivity issues. What networking components would you investigate first?

**Answer**

Check:

- Route Tables
- Security Groups
- Network ACLs
- Internet Gateway
- NAT Gateway
- Elastic Network Interfaces
- Subnet configuration
- Availability Zone distribution

**Explanation**

Most AWS networking issues are caused by incorrect routing, firewall rules, or subnet configuration. Verifying these components systematically helps identify and resolve connectivity problems efficiently.
