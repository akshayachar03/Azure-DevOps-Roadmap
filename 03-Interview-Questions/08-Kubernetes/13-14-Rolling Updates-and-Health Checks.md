# Rolling Updates & Health Checks Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is a Rolling Update in Kubernetes?

**Answer**

A Rolling Update is the default deployment strategy in Kubernetes that gradually replaces old Pods with new ones without causing application downtime.

Instead of stopping all existing Pods at once, Kubernetes creates new Pods and terminates old Pods incrementally.

**Explanation**

Rolling Updates ensure high availability during application deployments. Kubernetes maintains the desired number of running Pods while updating them one by one.

**Used in Production**

- Zero-downtime application deployments
- Updating container images
- Deploying new application versions

**Common Mistake**

Many candidates think all Pods restart simultaneously. Kubernetes updates Pods gradually based on the deployment strategy.

---

### Question 2

**Question**

What is a Rollback in Kubernetes?

**Answer**

A Rollback restores a Deployment to a previous stable version if the latest deployment introduces issues.

It can be performed using:

```bash
kubectl rollout undo deployment <deployment-name>
```

**Explanation**

Kubernetes stores Deployment revision history, allowing administrators to quickly revert failed releases.

**Used in Production**

- Failed application deployments
- Buggy releases
- Emergency production recovery

**Common Mistake**

Assuming rollback recreates the Deployment from scratch. Kubernetes restores the previous Deployment revision.

---

### Question 3

**Question**

What are Deployment Strategies in Kubernetes?

**Answer**

Deployment Strategies define how application updates are rolled out.

Common strategies include:

- Rolling Update (default)
- Recreate

**Explanation**

Rolling Update minimizes downtime, while Recreate terminates all old Pods before creating new ones.

**Used in Production**

Rolling Update is used for most production workloads because it provides continuous availability.

---

### Question 4

**Question**

What is the difference between Rolling Update and Recreate deployment strategies?

**Answer**

| Rolling Update | Recreate |
|----------------|-----------|
| Gradually replaces Pods | Deletes all old Pods first |
| Minimal or zero downtime | Causes downtime |
| Default strategy | Used when downtime is acceptable |

**Explanation**

Rolling Updates maintain service availability, whereas Recreate is suitable when multiple application versions cannot run simultaneously.

---

### Question 5

**Question**

What is a Liveness Probe?

**Answer**

A Liveness Probe checks whether a container is still running correctly.

If the probe fails repeatedly, Kubernetes restarts the container automatically.

**Explanation**

Liveness Probes detect applications that have become unresponsive or deadlocked.

**Used in Production**

- Recovering hung applications
- Restarting unhealthy containers automatically

**Common Mistake**

Confusing Liveness Probes with Readiness Probes. Liveness restarts containers, while Readiness controls traffic routing.

---

### Question 6

**Question**

What is a Readiness Probe?

**Answer**

A Readiness Probe determines whether a container is ready to receive application traffic.

If the probe fails, Kubernetes removes the Pod from the Service endpoints without restarting it.

**Explanation**

Readiness ensures users are not routed to Pods that are still starting or temporarily unavailable.

**Used in Production**

- Waiting for application initialization
- Database connection establishment
- Cache warm-up

---

### Question 7

**Question**

What is a Startup Probe?

**Answer**

A Startup Probe checks whether an application has completed its startup process.

Until the Startup Probe succeeds, Kubernetes ignores Liveness and Readiness Probe failures.

**Explanation**

This prevents slow-starting applications from being restarted before they finish initialization.

**Used in Production**

- Java applications
- Spring Boot services
- Large enterprise applications
- Applications with long initialization times

**Common Mistake**

Using only a Liveness Probe for slow applications, causing continuous restart loops.

---

### Question 8

**Question**

What is the difference between Liveness, Readiness, and Startup Probes?

**Answer**

| Probe | Purpose |
|--------|----------|
| Startup Probe | Checks whether the application has started |
| Readiness Probe | Checks whether the application is ready to serve traffic |
| Liveness Probe | Checks whether the application is still healthy and should continue running |

**Explanation**

Each probe serves a different purpose, and together they improve application reliability.

---

### Question 9

**Question**

What happens if a Liveness Probe fails?

**Answer**

Kubernetes restarts the container after the configured failure threshold is reached.

**Explanation**

The kubelet continuously monitors the Liveness Probe. If it repeatedly fails, Kubernetes assumes the application is unhealthy and restarts it.

**Used in Production**

Recovering from application hangs or deadlocks.

---

### Question 10

**Question**

What happens if a Readiness Probe fails?

**Answer**

The Pod is removed from the Service endpoints, and Kubernetes stops routing traffic to it.

The container continues running.

**Explanation**

Readiness failures do not restart the application. They only affect traffic routing.

**Common Mistake**

Believing a failed Readiness Probe restarts the container.

---

### Question 11

**Question**

Why are Rolling Updates preferred in production environments?

**Answer**

Rolling Updates provide:

- Zero or minimal downtime
- Gradual deployments
- Easy rollback
- Improved application availability
- Reduced deployment risk

**Explanation**

By updating Pods incrementally, Kubernetes ensures users continue accessing the application during deployments.

---

### Question 12

**Question**

Can Kubernetes automatically recover from an unhealthy application?

**Answer**

Yes.

Using Liveness Probes, Kubernetes can detect unhealthy containers and automatically restart them.

**Explanation**

This self-healing capability is one of Kubernetes' core features and improves application reliability.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

After deploying version 2 of your application, users begin reporting errors. How would you restore the previous working version?

**Answer**

Rollback the Deployment using:

```bash
kubectl rollout undo deployment <deployment-name>
```

**Explanation**

Kubernetes restores the previous Deployment revision, minimizing production downtime.

---

### Scenario 2

**Question**

Your application freezes due to a memory leak but the container process is still running. Which Kubernetes feature can automatically recover the application?

**Answer**

Configure a Liveness Probe.

**Explanation**

The Liveness Probe detects the unhealthy application and restarts the container automatically.

---

### Scenario 3

**Question**

A Java application requires three minutes to start. Kubernetes continuously restarts the container before startup completes. What should you configure?

**Answer**

Use a Startup Probe.

**Explanation**

The Startup Probe delays Liveness and Readiness checks until the application finishes starting.

---

### Scenario 4

**Question**

Your application starts successfully, but it requires an additional 30 seconds to connect to a database before serving requests. Which probe should you use?

**Answer**

Use a Readiness Probe.

**Explanation**

The Pod will not receive traffic until the database connection is established successfully.

---

### Scenario 5

**Question**

Your production deployment must not experience downtime during upgrades. Which deployment strategy should you choose?

**Answer**

Rolling Update.

**Explanation**

Rolling Updates replace Pods gradually while keeping the application available.

---

### Scenario 6

**Question**

A legacy application cannot run multiple versions simultaneously because of database compatibility issues. Which deployment strategy should you use?

**Answer**

Recreate.

**Explanation**

The Recreate strategy removes all existing Pods before creating new ones, preventing version conflicts.

---

### Scenario 7

**Question**

Users report intermittent "503 Service Unavailable" errors immediately after a deployment. What is the most likely cause?

**Answer**

The application is receiving traffic before it is ready because a proper Readiness Probe is missing or incorrectly configured.

**Explanation**

A correctly configured Readiness Probe prevents traffic from reaching Pods until they are fully initialized.

---

### Scenario 8

**Question**

Your application becomes unresponsive but Kubernetes does not restart the container. What should you investigate?

**Answer**

Verify the Liveness Probe configuration.

Check:

- Probe path
- Port
- Initial delay
- Timeout
- Failure threshold

**Explanation**

Without a correctly configured Liveness Probe, Kubernetes cannot detect hung applications.

---

### Scenario 9

**Question**

During a deployment, only a few Pods are updated at a time while the remaining Pods continue serving users. Which Kubernetes feature is responsible for this behavior?

**Answer**

Rolling Update Deployment Strategy.

**Explanation**

Rolling Updates gradually replace old Pods with new ones, maintaining application availability throughout the deployment.

---

### Scenario 10

**Question**

Your application passes the Startup Probe but later becomes unhealthy due to an internal issue. Which probe detects this condition?

**Answer**

The Liveness Probe.

**Explanation**

After the Startup Probe succeeds, Kubernetes begins using the Liveness Probe to continuously monitor the application's health and restart it if necessary.
