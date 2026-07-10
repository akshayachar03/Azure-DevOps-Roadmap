# Application Sync & Application Health Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Application Sync in Argo CD?

**Answer**

Application Sync is the process of making the Kubernetes cluster match the desired state stored in the Git repository.

**Explanation**

Argo CD continuously compares the Kubernetes cluster with the Git repository. If differences exist, synchronization updates the cluster so that it matches the desired configuration stored in Git.

**Where it is used in Production**

- Kubernetes application deployments
- GitOps workflows
- Continuous Delivery pipelines

**Common Mistake**

Many candidates think Sync simply redeploys the application. It only applies the changes required to make the cluster match Git.

---

### Question 2

**Question**

What is the difference between Manual Sync and Automatic Sync?

**Answer**

- **Manual Sync:** A user manually starts synchronization using the UI or CLI.
- **Automatic Sync:** Argo CD automatically synchronizes the application whenever changes are detected in Git.

**Explanation**

Manual Sync provides greater deployment control, while Automatic Sync enables fully automated GitOps deployments.

**Where it is used in Production**

- Manual Sync → Production environments requiring approvals.
- Automatic Sync → Development and testing environments.

**Common Mistake**

Candidates often think Automatic Sync runs continuously regardless of changes. It synchronizes only when a change is detected.

---

### Question 3

**Question**

When would you choose Manual Sync instead of Automatic Sync?

**Answer**

Manual Sync is preferred when:

- Production deployments require approval.
- Changes must be reviewed before deployment.
- Maintenance windows are enforced.
- Organizations follow change management policies.

**Explanation**

Manual Sync allows operators to control exactly when deployments occur.

**Where it is used in Production**

Enterprise production environments.

---

### Question 4

**Question**

What is Sync Status in Argo CD?

**Answer**

Sync Status indicates whether the application's resources in Kubernetes match the desired state stored in Git.

Common Sync statuses are:

- Synced
- OutOfSync

**Explanation**

Argo CD continuously compares Git and the cluster to determine synchronization status.

**Where it is used in Production**

Application monitoring dashboards.

---

### Question 5

**Question**

What does the "Synced" status mean?

**Answer**

Synced means the Kubernetes cluster exactly matches the desired configuration stored in Git.

**Explanation**

No synchronization is required because both states are identical.

**Where it is used in Production**

Healthy GitOps deployments.

---

### Question 6

**Question**

What does the "OutOfSync" status mean?

**Answer**

OutOfSync means the Kubernetes cluster differs from the desired configuration stored in Git.

**Explanation**

This can happen because:

- Git changes have not yet been synchronized.
- Manual cluster modifications created configuration drift.
- Resources were deleted or modified directly.

**Where it is used in Production**

GitOps monitoring and drift detection.

**Common Mistake**

Many candidates assume OutOfSync always indicates an error. It simply means Git and the cluster are different.

---

### Question 7

**Question**

What are Sync Options in Argo CD?

**Answer**

Sync Options are additional deployment settings that control synchronization behavior.

Examples include:

- Create Namespace
- Replace Resources
- Prune Resources
- Validate Resources

**Explanation**

These options customize how Argo CD performs deployments.

**Where it is used in Production**

Enterprise GitOps deployments with advanced deployment requirements.

---

### Question 8

**Question**

What does "Refresh Application" do in Argo CD?

**Answer**

Refresh forces Argo CD to immediately re-evaluate the Git repository and Kubernetes cluster to determine the latest synchronization and health status.

**Explanation**

Normally Argo CD refreshes automatically, but manual refresh retrieves the latest information instantly.

**Where it is used in Production**

Troubleshooting deployments and verifying recent Git commits.

---

### Question 9

**Question**

What is Application Health in Argo CD?

**Answer**

Application Health indicates whether the deployed Kubernetes resources are functioning correctly.

Common health states include:

- Healthy
- Progressing
- Degraded
- Missing

**Explanation**

Health focuses on runtime behavior, while Sync Status focuses on configuration consistency.

**Where it is used in Production**

Production monitoring dashboards.

**Common Mistake**

Candidates often confuse Sync Status with Health Status.

---

### Question 10

**Question**

What does the "Healthy" status mean?

**Answer**

Healthy means all Kubernetes resources are successfully running and operating as expected.

**Explanation**

Examples include:

- Pods are running.
- Deployments are available.
- Services are operational.

**Where it is used in Production**

Production application monitoring.

---

### Question 11

**Question**

What do the "Progressing", "Degraded", and "Missing" health statuses mean?

**Answer**

- **Progressing:** Resources are still being created or updated.
- **Degraded:** One or more resources are unhealthy or have failed.
- **Missing:** One or more expected resources do not exist in the cluster.

**Explanation**

These health states help operators quickly identify deployment problems.

**Where it is used in Production**

Application troubleshooting and monitoring.

---

### Question 12

**Question**

Can an application be "Synced" but still be "Degraded"?

**Answer**

Yes.

**Explanation**

Sync Status only indicates that the deployed configuration matches Git. Health Status indicates whether the application is actually running correctly.

For example:

- Git specifies three Pods.
- Kubernetes successfully creates all three Pods.
- Two Pods enter CrashLoopBackOff.

The application is **Synced** but **Degraded**.

**Where it is used in Production**

Real-world Kubernetes troubleshooting.

**Common Mistake**

Many candidates incorrectly assume Synced always means the application is healthy.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Your Argo CD application shows **OutOfSync**, but developers confirm they did not update the Git repository. What is the most likely reason?

**Answer**

Someone likely modified Kubernetes resources manually, creating configuration drift.

**Explanation**

Argo CD compares Git with the cluster, so manual changes cause the application to become OutOfSync.

---

### Scenario 2

**Question**

An application displays **Synced** but **Degraded**. What does this indicate?

**Answer**

The deployment configuration matches Git, but one or more Kubernetes resources are unhealthy.

**Explanation**

Common causes include:

- CrashLoopBackOff
- Failed Pods
- Readiness probe failures
- Image pull failures

---

### Scenario 3

**Question**

Your production environment requires manager approval before deployments. Which synchronization mode would you configure?

**Answer**

Manual Sync.

**Explanation**

Manual synchronization ensures deployments occur only after explicit approval.

---

### Scenario 4

**Question**

Developers want every Git commit to be deployed immediately to the development cluster. Which synchronization mode should you enable?

**Answer**

Automatic Sync.

**Explanation**

Argo CD automatically detects Git changes and synchronizes the application.

---

### Scenario 5

**Question**

After pushing a commit to Git, Argo CD does not immediately display the latest status. What can you do?

**Answer**

Use **Refresh Application**.

**Explanation**

Refreshing forces Argo CD to immediately retrieve the latest repository and cluster state.

---

### Scenario 6

**Question**

A deployment remains in the **Progressing** state for a long time. What would you investigate?

**Answer**

I would check:

- Pod status
- Deployment events
- Readiness probes
- Image pull status
- Resource availability

**Explanation**

Resources that never become ready prevent the application from reaching the Healthy state.

---

### Scenario 7

**Question**

An application suddenly changes from **Healthy** to **Missing**. What might have happened?

**Answer**

One or more Kubernetes resources were deleted manually or failed to be created.

**Explanation**

Argo CD expected the resources to exist but could no longer find them.

---

### Scenario 8

**Question**

Your organization wants deleted Kubernetes resources to be automatically removed when they are deleted from Git. Which feature would you configure?

**Answer**

Enable **Prune** through Sync Options.

**Explanation**

Pruning removes resources that no longer exist in the Git repository.

---

### Scenario 9

**Question**

During an interview, you are asked to explain the difference between Sync Status and Health Status. How would you answer?

**Answer**

- **Sync Status** indicates whether the cluster configuration matches Git.
- **Health Status** indicates whether the deployed application is functioning correctly.

**Explanation**

An application can be Synced but unhealthy, or OutOfSync while still running successfully.

---

### Scenario 10

**Question**

A developer manually scales a Deployment from 3 replicas to 6 replicas in Kubernetes. Automatic Sync is enabled. What will Argo CD do?

**Answer**

Argo CD detects that the cluster no longer matches the desired state stored in Git and automatically restores the Deployment to the replica count defined in Git.

**Explanation**

This demonstrates GitOps reconciliation, where Git remains the single source of truth and manual configuration drift is automatically corrected.
