# Argo CD CLI Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is the Argo CD CLI, and why is it used?

**Answer**

The Argo CD CLI (`argocd`) is a command-line tool used to interact with the Argo CD server. It allows users to manage applications, repositories, clusters, projects, and synchronization operations directly from the terminal.

**Explanation**

The CLI communicates with the Argo CD API Server to perform operations such as creating applications, synchronizing deployments, checking application health, and managing repositories.

**Where it is used in Production**

- CI/CD pipelines
- Automation scripts
- Remote cluster management
- DevOps administration

**Common Mistake**

Many candidates think the CLI communicates directly with Kubernetes. It actually communicates with the Argo CD API Server.

---

### Question 2

**Question**

How do you log in to Argo CD using the CLI?

**Answer**

Use the following command:

```bash
argocd login <ARGOCD_SERVER>
```

For example:

```bash
argocd login argocd.example.com
```

**Explanation**

The login command authenticates the user with the Argo CD API Server using username/password or Single Sign-On (SSO).

**Where it is used in Production**

Before performing any administrative or deployment operations.

**Common Mistake**

Candidates often forget that the Argo CD server must be reachable from the machine running the CLI.

---

### Question 3

**Question**

How do you add a Git repository to Argo CD using the CLI?

**Answer**

Use:

```bash
argocd repo add <repository-url>
```

Example:

```bash
argocd repo add https://github.com/company/app-config.git
```

**Explanation**

This registers a Git repository with Argo CD so it can be used as an application source.

**Where it is used in Production**

Connecting Git repositories that store Kubernetes manifests, Helm charts, or Kustomize configurations.

---

### Question 4

**Question**

Why must a Git repository be added before creating an application?

**Answer**

Argo CD must be able to access the Git repository containing the application's desired state.

**Explanation**

Without a registered repository and valid credentials, Argo CD cannot retrieve manifests for deployment.

**Where it is used in Production**

GitOps-based Continuous Delivery workflows.

---

### Question 5

**Question**

How do you create an application using the Argo CD CLI?

**Answer**

Use:

```bash
argocd app create
```

along with required options such as:

- Application name
- Repository URL
- Repository path
- Destination cluster
- Destination namespace

**Explanation**

This creates an Argo CD Application resource that defines what should be deployed and where.

**Where it is used in Production**

Deploying new applications into Kubernetes clusters.

---

### Question 6

**Question**

How do you synchronize an application using the CLI?

**Answer**

Use:

```bash
argocd app sync <application-name>
```

**Explanation**

The sync command compares Git with the cluster and applies any required changes.

**Where it is used in Production**

- Manual deployments
- Emergency production updates
- CI/CD pipelines

**Common Mistake**

Candidates sometimes think synchronization is always automatic. Manual Sync is common when Auto Sync is disabled.

---

### Question 7

**Question**

How do you check application details using the CLI?

**Answer**

Use:

```bash
argocd app get <application-name>
```

**Explanation**

This command displays information such as:

- Sync status
- Health status
- Repository
- Target revision
- Destination cluster
- Namespace

**Where it is used in Production**

Application monitoring and troubleshooting.

---

### Question 8

**Question**

How do you delete an application using the CLI?

**Answer**

Use:

```bash
argocd app delete <application-name>
```

**Explanation**

This removes the Argo CD Application resource. Depending on configuration, Kubernetes resources may also be deleted.

**Where it is used in Production**

Application decommissioning and cleanup.

**Common Mistake**

Some candidates assume only the Argo CD application is deleted. If cascading deletion is enabled, Kubernetes resources can also be removed.

---

### Question 9

**Question**

What information does the `argocd app get` command provide?

**Answer**

It displays:

- Application health
- Sync status
- Git repository
- Target revision
- Kubernetes cluster
- Namespace
- Resource tree

**Explanation**

This command provides a quick overview of an application's current deployment status.

**Where it is used in Production**

Daily monitoring and troubleshooting.

---

### Question 10

**Question**

When would you use the Argo CD CLI instead of the Web UI?

**Answer**

The CLI is preferred for automation, scripting, CI/CD pipelines, and remote administration.

**Explanation**

It allows repetitive tasks to be executed programmatically and integrates easily with DevOps workflows.

**Where it is used in Production**

- Jenkins
- GitHub Actions
- Azure DevOps
- GitLab CI/CD

---

### Question 11

**Question**

Can the Argo CD CLI manage multiple applications?

**Answer**

Yes.

**Explanation**

The CLI supports managing multiple applications individually or through automation scripts, making it suitable for enterprise environments.

**Where it is used in Production**

Organizations managing hundreds of Kubernetes applications.

---

### Question 12

**Question**

What are the most commonly used Argo CD CLI commands?

**Answer**

Frequently used commands include:

```bash
argocd login
argocd repo add
argocd app create
argocd app sync
argocd app get
argocd app delete
```

**Explanation**

These commands cover the majority of daily Argo CD administration tasks.

**Where it is used in Production**

Routine GitOps operations and application lifecycle management.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

You have installed Argo CD and need to manage it from your local machine. What is your first CLI command?

**Answer**

```bash
argocd login <ARGOCD_SERVER>
```

**Explanation**

Authentication is required before performing any operations.

---

### Scenario 2

**Question**

Your deployment fails because Argo CD cannot access the Git repository. What would you check?

**Answer**

Verify that the repository has been added correctly and that the repository credentials are valid.

**Explanation**

Missing or incorrect credentials prevent Argo CD from retrieving manifests.

---

### Scenario 3

**Question**

A developer pushes changes to Git, but the application is not updated because Auto Sync is disabled. What command would you run?

**Answer**

```bash
argocd app sync <application-name>
```

**Explanation**

Manual synchronization applies the latest Git changes to the Kubernetes cluster.

---

### Scenario 4

**Question**

An application deployment completed successfully, but you want to verify its health and synchronization status. Which command would you use?

**Answer**

```bash
argocd app get <application-name>
```

**Explanation**

The command displays both Sync Status and Health Status, helping verify deployment success.

---

### Scenario 5

**Question**

A new Kubernetes application needs to be deployed from an existing Git repository. Which CLI command creates the application?

**Answer**

```bash
argocd app create
```

**Explanation**

This command registers the application with Argo CD by specifying the repository, path, destination cluster, and namespace.

---

### Scenario 6

**Question**

An obsolete application must be removed from Argo CD. Which command should you use?

**Answer**

```bash
argocd app delete <application-name>
```

**Explanation**

This deletes the Argo CD Application resource and, depending on configuration, may also remove Kubernetes resources.

---

### Scenario 7

**Question**

Your CI/CD pipeline must deploy an application immediately after a Git commit. Which Argo CD CLI command should be included?

**Answer**

```bash
argocd app sync <application-name>
```

**Explanation**

This triggers synchronization so the cluster matches the latest Git commit.

---

### Scenario 8

**Question**

A newly created application does not appear in the Argo CD UI. What would you verify first?

**Answer**

Check whether the `argocd app create` command completed successfully and verify the application using:

```bash
argocd app get <application-name>
```

**Explanation**

The command confirms whether the application exists and displays any configuration issues.

---

### Scenario 9

**Question**

A Git repository has been migrated to a new URL. What should you do before synchronization?

**Answer**

Update or re-add the repository in Argo CD with the correct URL and credentials.

**Explanation**

Argo CD must access the correct Git repository to retrieve application manifests.

---

### Scenario 10

**Question**

During an interview, you are asked to describe a typical CLI workflow for deploying an application with Argo CD. What would you answer?

**Answer**

The typical workflow is:

1. Log in to Argo CD using `argocd login`.
2. Add the Git repository using `argocd repo add`.
3. Create the application using `argocd app create`.
4. Synchronize the application using `argocd app sync`.
5. Verify the deployment using `argocd app get`.
6. Delete the application with `argocd app delete` when it is no longer needed.

**Explanation**

These commands represent the complete lifecycle of managing an application using the Argo CD CLI and are among the most frequently used in production environments.
