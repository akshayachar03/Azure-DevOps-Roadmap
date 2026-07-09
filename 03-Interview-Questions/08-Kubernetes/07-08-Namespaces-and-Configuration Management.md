# Namespaces & Configuration Management Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is a Namespace in Kubernetes, and why is it used?

**Answer**

A Namespace is a logical partition within a Kubernetes cluster that allows multiple teams, applications, or environments to share the same cluster while keeping their resources isolated.

**Explanation**

Namespaces provide logical separation without requiring separate clusters. Resources such as Pods, Services, Deployments, ConfigMaps, and Secrets can exist with the same names in different namespaces.

**Used in Production**

- Multi-team environments
- Development, Testing, and Production environments
- Multi-tenant Kubernetes clusters

**Common Mistake**

Many candidates think Namespaces provide complete security isolation. They only provide logical isolation; additional mechanisms like RBAC and Network Policies are required for security.

---

### Question 2

**Question**

What are the default namespaces available in Kubernetes?

**Answer**

The commonly available namespaces are:

- **default** – Default namespace for user-created resources.
- **kube-system** – Contains Kubernetes system components.
- **kube-public** – Publicly readable resources.
- **kube-node-lease** – Stores node heartbeat information.

**Explanation**

Each namespace has a specific purpose. Most user applications are initially deployed into the `default` namespace unless another namespace is specified.

**Used in Production**

Cluster organization and system component management.

**Common Mistake**

Deploying application workloads into `kube-system`.

---

### Question 3

**Question**

Why should you create custom namespaces instead of using the default namespace?

**Answer**

Custom namespaces improve organization, isolation, and resource management.

Benefits include:

- Environment separation
- Team isolation
- Easier access control
- Better resource management
- Simplified monitoring

**Explanation**

Using dedicated namespaces keeps production resources separate from development and testing workloads.

**Used in Production**

Examples:

- dev
- test
- staging
- production

**Common Mistake**

Deploying every application into the default namespace.

---

### Question 4

**Question**

How do you create and use a custom namespace?

**Answer**

Create a namespace:

```bash
kubectl create namespace dev
```

Deploy resources into it:

```bash
kubectl apply -f deployment.yaml -n dev
```

View resources:

```bash
kubectl get pods -n dev
```

**Explanation**

Resources are isolated within the specified namespace unless explicitly referenced.

**Used in Production**

Daily Kubernetes administration.

---

### Question 5

**Question**

What is resource isolation in Kubernetes?

**Answer**

Resource isolation ensures workloads in one namespace do not interfere with workloads in another.

This is achieved using:

- Namespaces
- Resource Quotas
- Limit Ranges
- RBAC
- Network Policies

**Explanation**

Isolation prevents resource contention and improves security and governance.

**Used in Production**

Shared Kubernetes clusters.

**Common Mistake**

Believing namespaces alone prevent resource overconsumption.

---

### Question 6

**Question**

What is a ConfigMap?

**Answer**

A ConfigMap stores non-sensitive configuration data as key-value pairs.

Examples:

- Application configuration
- URLs
- Feature flags
- Configuration files

**Explanation**

ConfigMaps separate configuration from application code, making deployments more flexible.

**Used in Production**

Application configuration management.

**Common Mistake**

Storing passwords or API keys inside ConfigMaps.

---

### Question 7

**Question**

What is a Secret in Kubernetes?

**Answer**

A Secret stores sensitive information such as:

- Passwords
- API keys
- Tokens
- Certificates
- SSH keys

**Explanation**

Secrets are stored separately from application configuration and can be mounted as files or exposed as environment variables.

**Used in Production**

Secure application configuration.

**Common Mistake**

Assuming Secrets are encrypted by default. By default, they are Base64-encoded and should be protected using encryption at rest.

---

### Question 8

**Question**

What is the difference between ConfigMaps and Secrets?

**Answer**

| ConfigMap | Secret |
|-----------|--------|
| Stores non-sensitive data | Stores sensitive data |
| Plain text values | Base64-encoded values |
| Application configuration | Passwords, tokens, certificates |
| Less restrictive | More secure handling |

**Explanation**

Use ConfigMaps for general configuration and Secrets for confidential information.

**Used in Production**

Both are commonly used together.

---

### Question 9

**Question**

How can ConfigMaps and Secrets be consumed by Pods?

**Answer**

They can be used in three ways:

- Environment variables
- Mounted volumes
- Command-line arguments

**Explanation**

Kubernetes injects configuration into Pods without requiring application rebuilds.

**Used in Production**

Application configuration and secret management.

---

### Question 10

**Question**

How are environment variables used in Kubernetes?

**Answer**

Environment variables pass configuration into containers during startup.

They can be defined:

- Directly in Pod YAML
- From ConfigMaps
- From Secrets

**Explanation**

Environment variables simplify application configuration and reduce hardcoded values.

**Used in Production**

Database URLs, API endpoints, application modes, feature flags.

**Common Mistake**

Hardcoding configuration values inside application images.

---

### Question 11

**Question**

Why should configuration be separated from application code?

**Answer**

Separating configuration provides:

- Easier updates
- Environment-specific settings
- Improved security
- Better CI/CD automation
- Reusable container images

**Explanation**

The same container image can be deployed across multiple environments using different ConfigMaps and Secrets.

**Used in Production**

Every modern Kubernetes deployment.

---

### Question 12

**Question**

Which Kubernetes object would you use for the following?

- Database password
- API endpoint
- TLS certificate
- Feature flag
- Application mode

**Answer**

| Requirement | Kubernetes Object |
|-------------|-------------------|
| Database password | Secret |
| API endpoint | ConfigMap |
| TLS certificate | Secret |
| Feature flag | ConfigMap |
| Application mode | ConfigMap |

**Explanation**

Sensitive information belongs in Secrets, while general configuration belongs in ConfigMaps.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Your application cannot connect to the database because the password is incorrect. Where should you verify the configuration first?

**Answer**

Check the Kubernetes Secret.

Commands:

```bash
kubectl get secret
kubectl describe secret <secret-name>
kubectl get pod <pod-name> -o yaml
```

**Explanation**

Database credentials are typically stored in Secrets and injected into the application.

---

### Scenario 2

**Question**

Your development and production applications are accidentally accessing each other's resources. How can you prevent this?

**Answer**

Deploy them into separate namespaces.

Example:

- dev
- staging
- production

**Explanation**

Namespaces provide logical isolation between environments.

---

### Scenario 3

**Question**

A developer stored database credentials inside a ConfigMap. Is this recommended?

**Answer**

No.

Sensitive information should always be stored in Kubernetes Secrets.

**Explanation**

ConfigMaps are intended only for non-sensitive configuration.

---

### Scenario 4

**Question**

You need to change an application's API endpoint without rebuilding the Docker image. Which Kubernetes feature would you use?

**Answer**

A ConfigMap.

**Explanation**

Configuration can be updated independently of the application image.

---

### Scenario 5

**Question**

Your application cannot find the expected environment variable during startup. What would you check?

**Answer**

Verify:

- Pod YAML
- ConfigMap
- Secret
- Environment variable mapping

Commands:

```bash
kubectl describe pod <pod-name>
kubectl get configmap
kubectl get secret
```

**Explanation**

Incorrect mappings are a common production issue.

---

### Scenario 6

**Question**

Two different teams want to deploy applications named `frontend` in the same Kubernetes cluster. How can this be achieved?

**Answer**

Deploy each application into a different namespace.

**Explanation**

Resources with the same name can exist in different namespaces without conflict.

---

### Scenario 7

**Question**

A production deployment fails because a required Secret is missing. What is the likely outcome?

**Answer**

The Pod may fail to start or enter states such as `CreateContainerConfigError` or `CrashLoopBackOff`, depending on how the Secret is referenced.

**Explanation**

Applications cannot access missing sensitive configuration during startup.

---

### Scenario 8

**Question**

Your security team wants application passwords to remain outside the Docker image. Which Kubernetes feature satisfies this requirement?

**Answer**

Kubernetes Secrets.

**Explanation**

Secrets allow credentials to be injected securely during deployment instead of embedding them into container images.

---

### Scenario 9

**Question**

A ConfigMap has been updated, but the application continues using the old configuration. What could be the reason?

**Answer**

The application may require a Pod restart to reload the updated ConfigMap, especially if the configuration is consumed as environment variables.

**Explanation**

Environment variables are loaded during container startup and are not automatically refreshed.

---

### Scenario 10

**Question**

A company wants every application team to have isolated resources, separate permissions, and independent quotas while sharing the same Kubernetes cluster. Which Kubernetes feature should be implemented first?

**Answer**

Namespaces.

**Explanation**

Namespaces provide logical separation of workloads and form the foundation for implementing RBAC, Resource Quotas, and Network Policies in shared clusters.
