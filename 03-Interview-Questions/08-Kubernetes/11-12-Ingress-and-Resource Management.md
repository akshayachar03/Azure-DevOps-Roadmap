# Ingress & Resource Management Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is an Ingress in Kubernetes?

**Answer**

An Ingress is a Kubernetes API resource that manages external HTTP and HTTPS access to services within a cluster.

Instead of exposing every application using a LoadBalancer or NodePort Service, an Ingress allows multiple services to share a single external entry point.

**Explanation**

Ingress acts as Layer 7 (HTTP/HTTPS) routing. It forwards incoming requests to the appropriate backend Service based on rules such as hostnames or URL paths.

**Used in Production**

- Hosting multiple web applications
- Microservices architectures
- SSL/TLS termination
- Centralized routing

**Common Mistake**

Many candidates confuse an Ingress with a Service. An Ingress routes traffic, whereas a Service exposes Pods internally or externally.

---

### Question 2

**Question**

What is an Ingress Controller?

**Answer**

An Ingress Controller is a component that watches Ingress resources and implements their routing rules.

Popular Ingress Controllers include:

- NGINX Ingress Controller
- HAProxy
- Traefik
- Azure Application Gateway Ingress Controller (AGIC)

**Explanation**

An Ingress resource only defines routing rules. Without an Ingress Controller, those rules are never applied.

**Used in Production**

Almost every production Kubernetes cluster uses an Ingress Controller for HTTP/HTTPS traffic management.

**Common Mistake**

Assuming that creating an Ingress resource alone is sufficient. It requires a running Ingress Controller.

---

### Question 3

**Question**

What is Path-Based Routing in Kubernetes Ingress?

**Answer**

Path-Based Routing directs requests to different backend services based on the URL path.

Example:

- `/api` → API Service
- `/web` → Frontend Service
- `/admin` → Admin Service

**Explanation**

The Ingress Controller inspects the request path and forwards traffic to the configured backend Service.

**Used in Production**

Microservices sharing a single domain.

**Common Mistake**

Trying to implement path routing using Services instead of an Ingress.

---

### Question 4

**Question**

What is Host-Based Routing in Kubernetes?

**Answer**

Host-Based Routing routes traffic based on the requested hostname.

Example:

- `api.company.com` → API Service
- `shop.company.com` → Shopping Service
- `admin.company.com` → Admin Service

**Explanation**

The Ingress Controller examines the Host header in the HTTP request and routes traffic accordingly.

**Used in Production**

Hosting multiple applications under different subdomains.

---

### Question 5

**Question**

What are CPU Requests in Kubernetes?

**Answer**

CPU Requests specify the minimum CPU resources a container requires.

The Kubernetes Scheduler uses CPU Requests when deciding where to place Pods.

**Explanation**

Requests guarantee resource availability but do not limit maximum CPU usage.

**Used in Production**

Ensuring critical applications receive sufficient CPU resources.

**Common Mistake**

Confusing CPU Requests with CPU Limits.

---

### Question 6

**Question**

What are Memory Requests in Kubernetes?

**Answer**

Memory Requests define the minimum amount of memory guaranteed to a container.

The Scheduler ensures that enough memory is available before scheduling the Pod.

**Explanation**

Memory Requests help prevent scheduling Pods onto nodes that lack sufficient memory.

**Used in Production**

Capacity planning and reliable workload scheduling.

---

### Question 7

**Question**

What are CPU Limits?

**Answer**

CPU Limits define the maximum CPU a container can consume.

If the application attempts to use more CPU than its limit, Kubernetes throttles the CPU usage.

**Explanation**

CPU Limits prevent a single application from consuming excessive processor resources.

**Used in Production**

Multi-tenant Kubernetes clusters.

**Common Mistake**

Assuming CPU limit violations terminate containers. CPU usage is throttled rather than killing the container.

---

### Question 8

**Question**

What are Memory Limits?

**Answer**

Memory Limits specify the maximum memory a container is allowed to use.

If the application exceeds the configured limit, Kubernetes terminates the container with an Out Of Memory (OOMKilled) error.

**Explanation**

Unlike CPU, memory cannot be throttled. Exceeding the limit results in container termination.

**Used in Production**

Preventing memory leaks from affecting other workloads.

**Common Mistake**

Believing memory behaves like CPU. Memory overuse results in OOMKilled rather than throttling.

---

### Question 9

**Question**

What is the difference between Requests and Limits?

**Answer**

| Requests | Limits |
|----------|--------|
| Minimum guaranteed resources | Maximum allowed resources |
| Used for scheduling | Used during runtime |
| Helps Kubernetes place Pods | Prevents excessive resource consumption |

**Explanation**

Requests determine where Pods can run, while Limits control resource usage after the Pod starts.

---

### Question 10

**Question**

Why should CPU and Memory Requests/Limits be configured?

**Answer**

They help:

- Improve scheduling decisions
- Prevent resource starvation
- Protect cluster stability
- Avoid noisy neighbor problems
- Improve resource utilization

**Explanation**

Without Requests and Limits, applications may consume excessive resources and negatively impact other workloads.

**Used in Production**

Every production Kubernetes cluster should define Requests and Limits for application containers.

---

### Question 11

**Question**

Can an Ingress expose multiple services using a single IP address?

**Answer**

Yes.

An Ingress can expose multiple backend Services through a single external IP or Load Balancer by using host-based or path-based routing rules.

**Explanation**

This reduces infrastructure cost and simplifies traffic management.

**Used in Production**

Hosting multiple applications behind a single Load Balancer.

---

### Question 12

**Question**

What happens if CPU and Memory Requests are not specified?

**Answer**

Kubernetes may schedule Pods inefficiently because it has no information about their expected resource requirements.

This can lead to:

- Resource contention
- Node overcommitment
- Poor application performance

**Explanation**

Resource Requests help the Scheduler make informed placement decisions.

**Common Mistake**

Leaving Requests and Limits undefined in production deployments.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Your company hosts three applications:

- app.company.com
- api.company.com
- admin.company.com

How would you expose them using Kubernetes?

**Answer**

Use a single Ingress with Host-Based Routing.

**Explanation**

Each hostname is mapped to its corresponding Kubernetes Service, allowing all applications to share one external Load Balancer.

---

### Scenario 2

**Question**

Your application is accessible internally but cannot be accessed through the Ingress. What should you check?

**Answer**

Verify:

```bash
kubectl get ingress
kubectl describe ingress
kubectl get pods -n ingress-nginx
kubectl get svc
```

Check:

- Ingress Controller is running
- Backend Service exists
- Routing rules are correct
- DNS points to the Load Balancer

**Explanation**

Ingress failures are commonly caused by missing Ingress Controllers or incorrect routing configuration.

---

### Scenario 3

**Question**

A container is repeatedly restarting with an "OOMKilled" status. What is the most likely cause?

**Answer**

The application exceeded its configured Memory Limit.

**Explanation**

Kubernetes terminates containers that exceed their Memory Limit to protect node stability.

---

### Scenario 4

**Question**

A critical production application occasionally becomes slow because another application consumes most of the CPU on the node. How would you prevent this?

**Answer**

Configure appropriate CPU Requests and CPU Limits.

**Explanation**

Requests reserve CPU for critical workloads, while Limits prevent one application from monopolizing CPU resources.

---

### Scenario 5

**Question**

Your frontend application should forward requests as follows:

- `/api` → API Service
- `/images` → Image Service
- `/admin` → Admin Service

Which Kubernetes feature should you use?

**Answer**

Ingress with Path-Based Routing.

**Explanation**

The Ingress Controller routes traffic to different Services based on the request path.

---

### Scenario 6

**Question**

A newly deployed Pod remains in the Pending state. The node has very little available memory. What is the likely reason?

**Answer**

The node cannot satisfy the Pod's Memory Request.

**Explanation**

The Scheduler will not place a Pod on a node that lacks the requested resources.

---

### Scenario 7

**Question**

A developer accidentally sets an extremely high CPU Limit for one application, causing other workloads to suffer. What is the best practice?

**Answer**

Define realistic CPU Requests and CPU Limits based on application requirements and monitoring data.

**Explanation**

Proper resource management ensures fair resource allocation across the cluster.

---

### Scenario 8

**Question**

Your organization wants all web applications to share one external Load Balancer to reduce cloud costs. Which Kubernetes feature supports this?

**Answer**

Ingress.

**Explanation**

Ingress allows multiple Services to share a single external IP using routing rules.

---

### Scenario 9

**Question**

A container uses only 200 MiB of memory but has a Memory Request of 2 GiB. What issue can this cause?

**Answer**

The Scheduler reserves unnecessary memory, reducing cluster utilization and preventing efficient Pod placement.

**Explanation**

Requests should closely match actual application requirements.

---

### Scenario 10

**Question**

Your application should never consume more than 1 CPU core, regardless of node capacity. Which Kubernetes resource configuration should you use?

**Answer**

Set a CPU Limit of `1`.

**Explanation**

The CPU Limit enforces the maximum CPU usage, ensuring the application cannot consume more than one core even if additional CPU resources are available.
