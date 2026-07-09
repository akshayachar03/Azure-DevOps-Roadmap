# Prometheus Fundamentals Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Prometheus, and why is it widely used in modern monitoring?

**Answer**

Prometheus is an open-source monitoring and alerting system designed to collect, store, and query time-series metrics from applications, servers, containers, and cloud infrastructure.

Its key features include:

- Pull-based metric collection
- Time-series database (TSDB)
- Powerful query language (PromQL)
- Built-in alerting support
- Easy integration with Grafana
- Service discovery for dynamic environments like Kubernetes

**Explanation**

Prometheus continuously scrapes metrics from configured targets, stores them as time-series data, and allows engineers to visualize and analyze system health. It is cloud-native and particularly well-suited for monitoring microservices and Kubernetes environments.

**Used in Production**

- Kubernetes clusters
- Docker containers
- Linux servers
- Cloud infrastructure
- CI/CD environments
- Microservices

**Common Mistake**

Many candidates confuse Prometheus with Grafana. Prometheus collects and stores metrics, while Grafana visualizes them.

---

### Question 2

**Question**

Explain the Prometheus architecture.

**Answer**

The Prometheus architecture consists of:

- Prometheus Server
- Targets
- Exporters
- Time-Series Database (TSDB)
- Alertmanager (optional)
- Grafana (optional for visualization)

Architecture Flow:

```text
Applications/Servers
        │
        ▼
 Exporters / Metric Endpoints
        │
        ▼
 Prometheus Server
        │
        ▼
      TSDB
        │
        ▼
Grafana / Alertmanager
```

**Explanation**

Prometheus periodically scrapes metrics from targets, stores them in its TSDB, and allows users to query the data using PromQL. Alerts can be forwarded to Alertmanager, while dashboards are commonly built using Grafana.

**Used in Production**

Enterprise monitoring platforms for cloud-native applications.

---

### Question 3

**Question**

What is the Prometheus Server?

**Answer**

The Prometheus Server is the core component responsible for:

- Scraping metrics
- Storing metrics in the TSDB
- Executing PromQL queries
- Evaluating alert rules
- Exposing APIs

**Explanation**

The server acts as the monitoring engine. It periodically collects metrics from configured targets and stores them for querying and visualization.

**Used in Production**

Every Prometheus deployment includes a Prometheus Server.

**Common Mistake**

Assuming Prometheus automatically discovers every system. Targets must be configured manually or through service discovery.

---

### Question 4

**Question**

What are Targets in Prometheus?

**Answer**

Targets are endpoints from which Prometheus collects metrics.

Examples include:

- Linux servers
- Kubernetes nodes
- Applications
- Databases
- Network devices
- Exporters

**Explanation**

Each target exposes a `/metrics` endpoint that Prometheus scrapes at regular intervals.

**Used in Production**

Thousands of targets may be monitored in large enterprise environments.

---

### Question 5

**Question**

What are Exporters, and why are they required?

**Answer**

Exporters are applications that expose metrics from systems that do not natively support the Prometheus metrics format.

Common exporters include:

- Node Exporter
- MySQL Exporter
- Blackbox Exporter
- Windows Exporter
- SNMP Exporter

**Explanation**

Prometheus can only scrape metrics in its expected format. Exporters collect system-specific information and expose it through an HTTP metrics endpoint.

**Used in Production**

Monitoring operating systems, databases, storage systems, and networking devices.

**Common Mistake**

Believing exporters store data. Exporters only expose metrics; Prometheus stores them.

---

### Question 6

**Question**

What is the Prometheus Time-Series Database (TSDB)?

**Answer**

The TSDB is the built-in database used by Prometheus to store metrics along with timestamps and labels.

Each metric consists of:

- Metric name
- Labels
- Value
- Timestamp

Example:

```text
node_cpu_seconds_total
instance="server1"
job="node"
timestamp=...
value=45
```

**Explanation**

The TSDB is optimized for high-performance storage and retrieval of time-series data.

**Used in Production**

Stores infrastructure and application metrics for dashboards, alerts, and historical analysis.

---

### Question 7

**Question**

How does Prometheus collect metrics?

**Answer**

Prometheus uses a Pull model.

The Prometheus Server periodically sends HTTP requests to configured targets and retrieves metrics from their `/metrics` endpoints.

**Explanation**

Instead of monitored systems sending data, Prometheus initiates the collection process according to the configured scrape interval.

**Used in Production**

Default behavior in Prometheus deployments.

**Common Mistake**

Confusing Prometheus with Push-based monitoring tools like CloudWatch Agent.

---

### Question 8

**Question**

What is the purpose of the `prometheus.yml` configuration file?

**Answer**

`prometheus.yml` is the main configuration file that defines:

- Global settings
- Scrape jobs
- Target endpoints
- Alert rule files
- Service discovery configuration

**Explanation**

Without this file, Prometheus does not know which targets to monitor or how frequently to scrape them.

**Used in Production**

Every Prometheus installation uses `prometheus.yml`.

---

### Question 9

**Question**

What is Global Configuration in Prometheus?

**Answer**

Global Configuration defines default settings applied across all scrape jobs.

Common settings include:

- `scrape_interval`
- `evaluation_interval`
- External labels

Example:

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s
```

**Explanation**

Global settings reduce repetitive configuration by providing default values for all jobs.

**Used in Production**

Used to standardize monitoring intervals across environments.

---

### Question 10

**Question**

What is Scrape Configuration?

**Answer**

Scrape Configuration tells Prometheus:

- Which targets to monitor
- How often to scrape them
- How to discover them
- Which labels to assign

Example:

```yaml
scrape_configs:
  - job_name: node
    static_configs:
      - targets:
          - localhost:9100
```

**Explanation**

Each scrape job defines a set of monitoring targets and the method used to collect metrics.

**Used in Production**

Used for monitoring servers, applications, Kubernetes clusters, and cloud services.

---

### Question 11

**Question**

How do you reload Prometheus configuration without restarting the service?

**Answer**

You can reload the configuration by:

- Sending a `SIGHUP` signal to the Prometheus process, or
- Calling the reload HTTP endpoint (if lifecycle management is enabled):

```bash
curl -X POST http://localhost:9090/-/reload
```

**Explanation**

Reloading applies configuration changes without interrupting metric collection.

**Used in Production**

Common after updating scrape jobs or alert rules.

**Common Mistake**

Restarting Prometheus for every configuration change instead of performing a reload.

---

### Question 12

**Question**

How do you verify that Prometheus is successfully scraping targets?

**Answer**

You can:

- Open the Prometheus UI.
- Navigate to **Status → Targets**.
- Verify that targets are in the **UP** state.
- Check the last scrape time and scrape duration.

**Explanation**

The Targets page provides the current health of all configured scrape jobs and quickly identifies connectivity or configuration issues.

**Used in Production**

Frequently used during initial setup and troubleshooting.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

You have installed Prometheus, but none of your servers are appearing in the Targets page. How would you troubleshoot?

**Answer**

I would:

- Verify the `prometheus.yml` configuration.
- Confirm the target IP and port.
- Check that the exporter is running.
- Ensure the `/metrics` endpoint is accessible.
- Reload the Prometheus configuration.
- Review Prometheus logs for errors.

**Explanation**

Missing or incorrect target configuration is one of the most common causes of scrape failures.

---

### Scenario 2

**Question**

Your Node Exporter service is running, but the target status shows **DOWN**. What would you check?

**Answer**

I would verify:

- Node Exporter service status
- Port 9100 accessibility
- Firewall rules
- Network connectivity
- Correct target configuration
- Metrics endpoint using:

```bash
curl http://server-ip:9100/metrics
```

**Explanation**

A target marked **DOWN** usually indicates connectivity issues or an unavailable metrics endpoint.

---

### Scenario 3

**Question**

You modified `prometheus.yml`, but Prometheus is still using the old configuration. What could be the problem?

**Answer**

Possible causes:

- Configuration was not reloaded.
- YAML syntax errors.
- Wrong configuration file edited.
- Reload request failed.

**Explanation**

Prometheus does not automatically reload configuration files after they are modified.

---

### Scenario 4

**Question**

Your Prometheus server is consuming excessive disk space. What would you investigate?

**Answer**

I would check:

- Metric retention period
- Number of monitored targets
- High-cardinality metrics
- TSDB storage usage
- Retention configuration

**Explanation**

Large environments generate significant amounts of time-series data, making retention tuning essential.

---

### Scenario 5

**Question**

A newly added application is not exposing any metrics. How would you proceed?

**Answer**

I would:

- Verify the application exposes a `/metrics` endpoint.
- Confirm the exporter is installed if required.
- Test the endpoint manually.
- Add the target to `prometheus.yml`.
- Reload Prometheus.

**Explanation**

Applications must expose metrics in Prometheus format before they can be scraped.

---

### Scenario 6

**Question**

Prometheus displays an error stating that the configuration file is invalid. What would you do?

**Answer**

I would:

- Validate YAML indentation.
- Check for syntax errors.
- Verify required fields.
- Use:

```bash
promtool check config prometheus.yml
```

**Explanation**

Most configuration issues are caused by incorrect YAML formatting or missing fields.

---

### Scenario 7

**Question**

One scrape job is working correctly, while another always shows **DOWN**. How would you isolate the issue?

**Answer**

I would compare:

- Target addresses
- Ports
- Exporter status
- Firewall rules
- Job configuration
- Network connectivity

**Explanation**

Comparing a working configuration with a failing one often identifies configuration mistakes quickly.

---

### Scenario 8

**Question**

A server becomes unreachable after a firewall update. How would Prometheus indicate this?

**Answer**

The target would change to **DOWN**, and scrape errors would appear in the Targets page and Prometheus logs.

**Explanation**

Prometheus continuously checks target availability during each scrape interval.

---

### Scenario 9

**Question**

Your manager asks why Prometheus uses a Pull model instead of a Push model. How would you explain?

**Answer**

The Pull model provides:

- Simpler service discovery
- Better health checking
- Easier troubleshooting
- Centralized scrape scheduling
- Reduced agent complexity

**Explanation**

Prometheus controls metric collection, making it easier to manage large and dynamic infrastructures such as Kubernetes.

---

### Scenario 10

**Question**

You deploy a new Node Exporter on a production server, but no metrics appear in Grafana. What troubleshooting steps would you perform?

**Answer**

I would:

1. Verify Node Exporter is running.
2. Check the `/metrics` endpoint.
3. Confirm the target is **UP** in Prometheus.
4. Verify the scrape job configuration.
5. Reload Prometheus.
6. Test the PromQL query in Prometheus.
7. Verify the Grafana data source.

**Explanation**

The issue may exist in the exporter, Prometheus configuration, PromQL query, or Grafana rather than the monitoring server itself.
