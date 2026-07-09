# Application Monitoring, Labels & Recording Rules Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Application Monitoring in Prometheus?

**Answer**

Application Monitoring is the process of collecting and monitoring metrics exposed directly by an application to measure its health, performance, and availability.

Common application metrics include:

- HTTP request count
- Response time
- Error rate
- CPU usage
- Memory usage
- Database connections
- Custom business metrics

**Explanation**

Unlike infrastructure monitoring, application monitoring focuses on how the application behaves rather than the server it runs on. Prometheus periodically scrapes metrics from application endpoints (typically `/metrics`) and stores them in its TSDB.

**Where it is used in Production**

- Web applications
- APIs
- Microservices
- Java, Go, Python, and .NET applications

**Common Mistake**

Monitoring only server metrics while ignoring application-specific metrics such as request latency and error rates.

---

### Question 2

**Question**

Which HTTP metrics are commonly monitored in Prometheus?

**Answer**

Common HTTP metrics include:

- Total HTTP requests
- Request rate
- Response latency
- HTTP status codes (200, 404, 500)
- Error rate
- Active requests

**Explanation**

These metrics help identify slow applications, failed requests, and traffic patterns.

**Where it is used in Production**

Monitoring REST APIs, web applications, and microservices.

---

### Question 3

**Question**

Why are CPU metrics important in application monitoring?

**Answer**

CPU metrics indicate how much processor time an application or container is consuming.

They help identify:

- High CPU utilization
- Infinite loops
- Resource bottlenecks
- Performance degradation

**Explanation**

High CPU usage may indicate increased workload or inefficient application code.

**Where it is used in Production**

Performance monitoring and capacity planning.

---

### Question 4

**Question**

Why should memory metrics be monitored?

**Answer**

Memory metrics help detect:

- Memory leaks
- Excessive memory usage
- Out-of-memory (OOM) conditions
- Inefficient resource utilization

**Explanation**

Monitoring memory prevents application crashes caused by resource exhaustion.

**Where it is used in Production**

Long-running services and containerized applications.

**Common Mistake**

Ignoring gradual memory growth that eventually leads to application failures.

---

### Question 5

**Question**

What disk and network metrics are commonly monitored?

**Answer**

**Disk Metrics**

- Disk usage
- Read/write operations
- Disk latency
- Filesystem utilization

**Network Metrics**

- Network throughput
- Packet loss
- Network errors
- Incoming traffic
- Outgoing traffic

**Explanation**

These metrics help identify storage bottlenecks and network-related issues.

**Where it is used in Production**

Infrastructure monitoring and troubleshooting.

---

### Question 6

**Question**

What are labels in Prometheus?

**Answer**

Labels are key-value pairs attached to metrics that provide additional information.

Example:

```text
http_requests_total{job="web",instance="10.0.0.5",method="GET"}
```

**Explanation**

Labels uniquely identify metrics and make querying and filtering much more flexible.

**Where it is used in Production**

Filtering metrics by:

- Environment
- Service
- Instance
- Region
- Namespace

---

### Question 7

**Question**

Why are labels important in Prometheus?

**Answer**

Labels enable:

- Metric filtering
- Aggregation
- Grouping
- Alert routing
- Dashboard customization

**Explanation**

Without labels, it would be difficult to distinguish metrics from different applications, environments, or instances.

**Where it is used in Production**

Multi-service and multi-cluster monitoring.

---

### Question 8

**Question**

What are label selectors?

**Answer**

Label selectors filter metrics based on label values.

Example:

```promql
http_requests_total{job="frontend"}
```

**Explanation**

Prometheus returns only metrics whose labels match the specified criteria.

**Where it is used in Production**

Filtering metrics for specific applications, namespaces, or environments.

---

### Question 9

**Question**

How is label filtering used in PromQL?

**Answer**

Label filtering allows users to query only the required metrics.

Examples:

```promql
node_cpu_seconds_total{instance="server01"}
```

```promql
http_requests_total{environment="production"}
```

**Explanation**

Filtering reduces unnecessary data and focuses queries on relevant resources.

**Where it is used in Production**

Dashboards, alerts, and troubleshooting.

---

### Question 10

**Question**

What are Recording Rules in Prometheus?

**Answer**

Recording Rules precompute frequently used PromQL expressions and store the results as new time-series.

Example:

```yaml
groups:
- name: cpu
  rules:
  - record: job:cpu_usage:avg
    expr: avg(rate(node_cpu_seconds_total[5m]))
```

**Explanation**

Instead of executing expensive queries repeatedly, Prometheus calculates them once at regular intervals.

**Where it is used in Production**

Large monitoring environments with complex dashboards and alerts.

---

### Question 11

**Question**

Why are Recording Rules used?

**Answer**

Recording Rules provide:

- Faster dashboard loading
- Reduced PromQL computation
- Improved query performance
- Lower Prometheus CPU utilization

**Explanation**

Complex queries become simple metric lookups after they are recorded.

**Where it is used in Production**

Grafana dashboards, alert rules, and high-scale monitoring systems.

**Common Mistake**

Using Recording Rules for simple queries that do not benefit from precomputation.

---

### Question 12

**Question**

How are Recording Rules evaluated?

**Answer**

Prometheus evaluates Recording Rules at configured intervals and stores the calculated results as new metrics in the TSDB.

**Explanation**

The evaluation interval determines how frequently recorded metrics are updated.

**Where it is used in Production**

Continuous generation of precomputed metrics for dashboards and alerting.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Users report that an application has become slow, but the server CPU utilization is normal. Which application metrics would you investigate?

**Answer**

I would check:

- HTTP request latency
- Request rate
- Error rate
- Database response time
- Application-specific metrics

**Explanation**

Application performance problems are often caused by code or downstream dependencies rather than server resource usage.

---

### Scenario 2

**Question**

A container crashes every few hours because it runs out of memory. Which metrics would help identify the issue?

**Answer**

I would monitor:

- Memory utilization
- Memory growth trend
- Container restart count
- OOM events

**Explanation**

Gradually increasing memory usage often indicates a memory leak.

---

### Scenario 3

**Question**

A manager wants dashboards showing metrics only for production servers. How would you achieve this?

**Answer**

I would use label filtering, for example:

```promql
node_cpu_seconds_total{environment="production"}
```

**Explanation**

Labels allow Prometheus to filter metrics based on environment.

---

### Scenario 4

**Question**

A Grafana dashboard is slow because it executes multiple complex PromQL queries. How would you improve performance?

**Answer**

I would create Recording Rules for the frequently executed complex queries and use the recorded metrics in Grafana.

**Explanation**

Precomputed metrics significantly reduce query execution time.

---

### Scenario 5

**Question**

Your team wants to compare CPU utilization across multiple Kubernetes namespaces. How would you organize the metrics?

**Answer**

I would use namespace labels and aggregate metrics by namespace using PromQL.

**Explanation**

Labels make grouping and comparison straightforward.

---

### Scenario 6

**Question**

A new application has been deployed, but no metrics appear in Prometheus. What would you verify?

**Answer**

I would verify:

- The application exposes a `/metrics` endpoint.
- Prometheus is scraping the endpoint.
- The scrape configuration is correct.
- The target status is UP.

**Explanation**

Missing metrics are usually caused by incorrect instrumentation or scrape configuration.

---

### Scenario 7

**Question**

HTTP 500 errors suddenly increase after a deployment. Which Prometheus metrics would you examine?

**Answer**

I would review:

- HTTP status code metrics
- Request rate
- Response latency
- Error rate
- Deployment timeline

**Explanation**

These metrics help determine whether the deployment introduced application errors.

---

### Scenario 8

**Question**

Your Prometheus server has high CPU utilization because dashboards execute expensive aggregation queries. What is the recommended solution?

**Answer**

I would create Recording Rules for the expensive queries and update dashboards to use the recorded metrics.

**Explanation**

Recording Rules reduce Prometheus query workload and improve dashboard responsiveness.

---

### Scenario 9

**Question**

A DevOps engineer wants alerts only for the payment service. How would you configure Prometheus?

**Answer**

I would use label selectors such as:

```promql
http_requests_total{service="payment"}
```

and create alert rules using those filtered metrics.

**Explanation**

Labels allow alerts to target specific applications or services.

---

### Scenario 10

**Question**

Your manager requests dashboards showing CPU, memory, disk, network, and HTTP metrics for every application. How would you implement this?

**Answer**

I would:

- Instrument applications with Prometheus client libraries.
- Collect infrastructure metrics using Node Exporter.
- Collect container metrics using cAdvisor.
- Configure Prometheus to scrape all targets.
- Build Grafana dashboards using PromQL.

**Explanation**

Combining application and infrastructure metrics provides complete observability, enabling faster troubleshooting and better capacity planning.
