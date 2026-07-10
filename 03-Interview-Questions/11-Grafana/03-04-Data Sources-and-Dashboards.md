# Data Sources & Dashboards Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is a data source in Grafana?

**Answer**

A data source is the backend system from which Grafana retrieves monitoring or log data for visualization. Grafana connects to the data source, executes queries, and displays the results in dashboards.

**Explanation**

Grafana does not store metrics or logs itself. It acts as a visualization layer that queries external systems.

**Where it is used in Production**

- Infrastructure monitoring
- Application monitoring
- Cloud monitoring
- Log analysis

**Common Mistake**

Many candidates think Grafana stores metrics. In reality, the data is stored in external systems such as Prometheus or Elasticsearch.

---

### Question 2

**Question**

Which data sources are commonly used with Grafana?

**Answer**

Common Grafana data sources include:

- Prometheus
- Azure Monitor
- Elasticsearch
- Loki
- InfluxDB
- MySQL
- PostgreSQL
- CloudWatch

**Explanation**

Grafana supports hundreds of data source plugins, allowing organizations to visualize metrics, logs, and traces from multiple platforms in a single interface.

**Where it is used in Production**

Unified monitoring across cloud platforms, Kubernetes clusters, servers, and applications.

---

### Question 3

**Question**

How does Grafana integrate with Prometheus?

**Answer**

Grafana connects to the Prometheus server using its HTTP API. It executes PromQL queries against Prometheus and visualizes the returned metrics.

**Explanation**

Prometheus collects and stores time-series metrics, while Grafana provides dashboards and graphs for those metrics.

**Where it is used in Production**

- Kubernetes monitoring
- Server monitoring
- Container monitoring
- Application performance monitoring

**Common Mistake**

Assuming Grafana collects metrics from exporters directly instead of querying Prometheus.

---

### Question 4

**Question**

How is Azure Monitor used as a Grafana data source?

**Answer**

Grafana connects to Azure Monitor using Azure authentication credentials and retrieves metrics, logs, and resource information from Azure services.

**Explanation**

Azure Monitor allows Grafana to visualize metrics from Azure Virtual Machines, App Services, AKS, Storage Accounts, SQL Databases, and other Azure resources.

**Where it is used in Production**

Organizations running workloads in Microsoft Azure.

---

### Question 5

**Question**

What is Elasticsearch used for in Grafana?

**Answer**

Elasticsearch is commonly used as a log analytics data source. Grafana queries Elasticsearch to visualize logs and create operational dashboards.

**Explanation**

While Prometheus is optimized for metrics, Elasticsearch is optimized for searching and analyzing log data.

**Where it is used in Production**

- Application logs
- Web server logs
- Security logs
- System logs

---

### Question 6

**Question**

What is Loki, and why is it used with Grafana?

**Answer**

Loki is a log aggregation system developed by Grafana Labs. It collects and stores logs while using labels similar to Prometheus for efficient querying.

**Explanation**

Grafana integrates directly with Loki to provide centralized log visualization alongside metrics.

**Where it is used in Production**

- Kubernetes logging
- Docker logging
- Application log monitoring

**Common Mistake**

Confusing Loki with Elasticsearch. Loki indexes labels instead of the entire log content, making it more storage-efficient.

---

### Question 7

**Question**

How do you verify whether a data source is configured correctly?

**Answer**

After configuring the data source, use the **Test & Save** option. If the connection is successful, Grafana confirms that it can communicate with the backend.

**Explanation**

This verifies connectivity, authentication, and API communication before dashboards are created.

**Where it is used in Production**

Whenever a new data source is added or existing credentials are updated.

---

### Question 8

**Question**

How do you create a dashboard in Grafana?

**Answer**

The typical steps are:

1. Create a new dashboard.
2. Add a panel.
3. Select the data source.
4. Write the query.
5. Choose a visualization type.
6. Save the dashboard.

**Explanation**

A dashboard combines multiple panels into a single monitoring view.

**Where it is used in Production**

Infrastructure, application, database, and cloud monitoring dashboards.

---

### Question 9

**Question**

Why would you import an existing dashboard instead of creating one from scratch?

**Answer**

Importing dashboards saves time because many community dashboards are already optimized for popular technologies like Prometheus, Kubernetes, Docker, and Node Exporter.

**Explanation**

Grafana supports importing dashboards using JSON files or dashboard IDs from Grafana Labs.

**Where it is used in Production**

Quick deployment of standardized monitoring dashboards.

---

### Question 10

**Question**

How do you export a Grafana dashboard?

**Answer**

Dashboards can be exported as JSON files from the dashboard settings menu.

**Explanation**

The exported JSON contains the dashboard configuration and can be imported into another Grafana instance.

**Where it is used in Production**

- Dashboard backup
- Migration
- Version control
- Sharing dashboards across environments

---

### Question 11

**Question**

What are dashboard variables in Grafana?

**Answer**

Dashboard variables are dynamic values that allow users to filter dashboards without modifying queries.

Examples include:

- Server
- Namespace
- Cluster
- Pod
- Environment

**Explanation**

Variables make dashboards reusable across multiple environments and resources.

**Where it is used in Production**

Monitoring hundreds of servers or Kubernetes clusters using a single dashboard.

**Common Mistake**

Creating separate dashboards for each server instead of using variables.

---

### Question 12

**Question**

What settings can be configured for a Grafana dashboard?

**Answer**

Common dashboard settings include:

- Dashboard title
- Refresh interval
- Time range
- Variables
- Permissions
- Tags
- Version history

**Explanation**

These settings improve dashboard usability and control how data is displayed.

**Where it is used in Production**

Managing dashboards for different teams and environments.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

You configured Prometheus as a data source, but the "Test & Save" operation fails. How would you troubleshoot it?

**Answer**

I would:

- Verify the Prometheus server is running.
- Check the Prometheus URL.
- Test network connectivity.
- Verify firewall rules.
- Confirm Prometheus is accessible from the Grafana server.
- Review Grafana logs.

**Explanation**

Most data source failures are caused by incorrect URLs, network issues, or unavailable Prometheus services.

---

### Scenario 2

**Question**

Your dashboard shows "No Data" even though Prometheus is collecting metrics. What would you check?

**Answer**

I would verify:

- The selected data source.
- The PromQL query.
- Dashboard time range.
- Metric availability in Prometheus.
- Dashboard variables.

**Explanation**

Incorrect queries or time ranges are common reasons for empty dashboards.

---

### Scenario 3

**Question**

Your company wants the same dashboard to work for Development, QA, and Production environments. How would you implement it?

**Answer**

I would create dashboard variables for environment selection and reference those variables in all queries.

**Explanation**

Variables eliminate the need to maintain multiple dashboards for different environments.

---

### Scenario 4

**Question**

After importing a community dashboard, several panels display errors. What would you investigate?

**Answer**

I would check:

- Correct data source selection.
- Required metrics availability.
- Dashboard variables.
- Prometheus job names.
- Exporter configuration.

**Explanation**

Community dashboards often expect specific metric names and labels that may differ in your environment.

---

### Scenario 5

**Question**

Your manager wants to migrate dashboards from the staging Grafana server to production. How would you do it?

**Answer**

I would export the dashboards as JSON files from staging and import them into the production Grafana instance.

**Explanation**

Grafana dashboards are portable because they are stored in JSON format.

---

### Scenario 6

**Question**

A newly added Azure Monitor data source fails authentication. What would you verify?

**Answer**

I would verify:

- Azure credentials.
- Tenant ID.
- Subscription ID.
- Client ID.
- Client Secret.
- Required Azure permissions.

**Explanation**

Authentication failures are usually caused by incorrect credentials or insufficient permissions.

---

### Scenario 7

**Question**

Users complain that dashboard loading is very slow. How would you troubleshoot it?

**Answer**

I would:

- Optimize queries.
- Reduce dashboard refresh frequency.
- Limit returned data.
- Check data source performance.
- Remove unnecessary panels.

**Explanation**

Complex queries and excessive panel refreshes commonly cause slow dashboards.

---

### Scenario 8

**Question**

Your organization wants standard dashboards across all Kubernetes clusters. What approach would you recommend?

**Answer**

I would create standardized dashboards with variables for cluster, namespace, and node selection, then export and reuse them across environments.

**Explanation**

Dashboard variables make one dashboard reusable across multiple clusters.

---

### Scenario 9

**Question**

A dashboard that previously worked suddenly stops displaying Loki logs. What would you check?

**Answer**

I would verify:

- Loki service availability.
- Data source connectivity.
- Label queries.
- Time range.
- Grafana logs.
- Loki logs.

**Explanation**

Missing logs are often caused by connectivity issues or incorrect label filters.

---

### Scenario 10

**Question**

A developer accidentally deleted an important dashboard. How would you recover it?

**Answer**

I would restore it by:

- Importing the previously exported JSON backup.
- Restoring from Grafana database backups if available.
- Retrieving it from version control if dashboard JSON files are maintained.

**Explanation**

Regular dashboard exports and version control are common production best practices to prevent permanent dashboard loss.
