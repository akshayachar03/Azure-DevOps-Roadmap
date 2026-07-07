# Azure DevOps Kubernetes Integration Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Kubernetes Integration in Azure DevOps?

**Answer**

Kubernetes Integration in Azure DevOps enables CI/CD pipelines to deploy, update, and manage containerized applications running on Kubernetes clusters.

Azure DevOps can:

- Build Docker images
- Push images to a container registry
- Deploy applications to Kubernetes
- Update Kubernetes resources
- Perform rolling updates
- Monitor deployment status

Typical workflow:

```text
Source Code
      │
      ▼
Build Docker Image
      │
      ▼
Push Image to Registry
      │
      ▼
Deploy to Kubernetes
      │
      ▼
Verify Deployment
```

**Explanation**

Azure DevOps automates Kubernetes deployments, reducing manual work and ensuring consistent deployments across environments.

**Used in Production**

Organizations commonly integrate Azure DevOps with Azure Kubernetes Service (AKS) or self-managed Kubernetes clusters.

**Common Mistake**

Many candidates think Azure DevOps hosts Kubernetes clusters. Azure DevOps only automates deployments to Kubernetes.

---

### Question 2

**Question**

What is Azure Kubernetes Service (AKS)?

**Answer**

Azure Kubernetes Service (AKS) is Microsoft's managed Kubernetes service that simplifies deploying and managing containerized applications.

Features include:

- Managed control plane
- Automatic upgrades
- Scaling
- Azure integration
- High availability
- RBAC support

**Explanation**

AKS reduces operational overhead by managing the Kubernetes control plane while allowing organizations to manage their workloads.

**Used in Production**

Many organizations deploy microservices and containerized applications on AKS.

---

### Question 3

**Question**

How does Azure DevOps deploy applications to AKS?

**Answer**

Typical deployment process:

1. Build Docker image.
2. Push image to Azure Container Registry (ACR).
3. Authenticate to Azure.
4. Connect to AKS.
5. Deploy Kubernetes manifests.
6. Verify deployment.

Workflow:

```text
Pipeline
     │
     ▼
Docker Build
     │
     ▼
Azure Container Registry
     │
     ▼
AKS Deployment
```

**Explanation**

Azure DevOps automates the complete deployment process using Kubernetes manifests or Helm charts.

**Used in Production**

Most AKS deployments follow this workflow.

---

### Question 4

**Question**

What is a Kubernetes Manifest?

**Answer**

A Kubernetes Manifest is a YAML file that defines Kubernetes resources.

Examples include:

- Deployment
- Service
- ConfigMap
- Secret
- Ingress
- Namespace

Example:

```yaml
apiVersion: apps/v1
kind: Deployment
```

**Explanation**

The manifest describes the desired state of Kubernetes resources, and Kubernetes works to maintain that state.

**Used in Production**

All Kubernetes deployments are managed through manifest files or Helm charts.

**Common Mistake**

Thinking manifests execute commands. They describe the desired configuration declaratively.

---

### Question 5

**Question**

What is the Kubernetes Manifest Task in Azure DevOps?

**Answer**

The Kubernetes Manifest Task is a built-in Azure DevOps task that deploys Kubernetes manifests to a Kubernetes cluster.

Example:

```yaml
- task: KubernetesManifest@1
```

It supports:

- Deploy
- Bake
- Scale
- Patch
- Delete

**Explanation**

The task simplifies Kubernetes deployments and integrates with Azure Kubernetes Service and other Kubernetes clusters.

**Used in Production**

Many organizations use the Kubernetes Manifest Task to automate application deployments.

---

### Question 6

**Question**

What is the Kubectl Task?

**Answer**

The Kubectl Task executes `kubectl` commands directly from Azure DevOps pipelines.

Examples:

```bash
kubectl apply -f deployment.yaml
kubectl get pods
kubectl delete pod
```

**Explanation**

The Kubectl Task provides flexibility for managing Kubernetes resources beyond predefined deployment tasks.

**Used in Production**

Teams use Kubectl tasks for troubleshooting, administration, and custom deployment operations.

---

### Question 7

**Question**

What is the difference between the Kubernetes Manifest Task and the Kubectl Task?

**Answer**

| Kubernetes Manifest Task | Kubectl Task |
|---------------------------|--------------|
| Designed for application deployments | Executes any kubectl command |
| Declarative deployment workflow | Command-line flexibility |
| Supports image substitution and deployment tracking | Supports administrative and troubleshooting tasks |
| Easier for standard deployments | Better for advanced Kubernetes operations |

**Explanation**

The Kubernetes Manifest Task is optimized for CI/CD deployments, while the Kubectl Task provides full Kubernetes command-line capabilities.

**Used in Production**

Many pipelines combine both tasks when deployment and operational commands are required.

---

### Question 8

**Question**

How does Azure DevOps authenticate with AKS?

**Answer**

Authentication typically uses:

- Azure Resource Manager Service Connection
- Kubernetes Service Connection
- Service Principal
- Managed Identity (where supported)

Workflow:

```text
Pipeline
      │
      ▼
Service Connection
      │
      ▼
AKS Cluster
      │
      ▼
Deployment
```

**Explanation**

Secure authentication ensures only authorized pipelines can deploy to Kubernetes clusters.

**Used in Production**

AKS deployments commonly use Azure Resource Manager Service Connections backed by Service Principals or managed identities.

---

### Question 9

**Question**

Why are Kubernetes manifests stored in Git repositories?

**Answer**

Benefits include:

- Version control
- Collaboration
- Change history
- Rollback capability
- Pull Request reviews
- Infrastructure as Code

**Explanation**

Treating Kubernetes manifests as code improves consistency and governance.

**Used in Production**

Most organizations manage Kubernetes manifests through Git repositories.

---

### Question 10

**Question**

What are some best practices for Kubernetes deployments using Azure DevOps?

**Answer**

Best practices include:

- Store manifests in Git.
- Use Pull Requests.
- Use separate namespaces or clusters for environments.
- Use image version tags.
- Use Azure Container Registry.
- Apply RBAC.
- Validate manifests before deployment.
- Monitor deployment health.

**Explanation**

These practices improve security, reliability, and maintainability.

**Used in Production**

Enterprise Kubernetes deployments typically follow these recommendations.

---

### Question 11

**Question**

What is a typical Azure DevOps Kubernetes CI/CD pipeline?

**Answer**

Typical workflow:

```text
Developer Commit
        │
        ▼
Checkout Source Code
        │
        ▼
Build Docker Image
        │
        ▼
Run Tests
        │
        ▼
Push Image to Azure Container Registry
        │
        ▼
Deploy Kubernetes Manifest
        │
        ▼
Verify Deployment
```

**Explanation**

This workflow ensures that only tested container images are deployed to Kubernetes.

**Used in Production**

Most enterprise Kubernetes deployments follow this CI/CD pattern.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A deployment to AKS fails because the pipeline cannot connect to the cluster. What would you check?

**Answer**

Verify:

1. Azure Service Connection.
2. Kubernetes Service Connection.
3. Cluster availability.
4. Azure RBAC permissions.
5. Network connectivity.
6. Pipeline logs.

**Explanation**

Authentication and connectivity issues are common causes of deployment failures.

---

### Scenario 2

**Question**

A Kubernetes deployment succeeds, but the application is not accessible. What would you investigate?

**Answer**

Check:

- Pod status.
- Deployment status.
- Service configuration.
- Ingress configuration.
- Container logs.
- Readiness and liveness probes.
- Network policies.

**Explanation**

Successful deployment does not guarantee application availability. Service exposure and application health must also be verified.

---

### Scenario 3

**Question**

A pipeline deploys an older Docker image to AKS instead of the latest version. What would you investigate?

**Answer**

Check:

- Image tag.
- Manifest image reference.
- Registry contents.
- Pipeline variables.
- Deployment configuration.
- Image pull policy.

**Explanation**

Static image tags or incorrect manifest references often cause outdated images to be deployed.

---

### Scenario 4

**Question**

Your manager wants every Kubernetes deployment to be traceable to a specific Git commit. How would you implement this?

**Answer**

Tag Docker images using immutable identifiers such as:

- Git commit SHA
- Azure DevOps Build ID
- Semantic application version

Update the Kubernetes manifest with the tagged image before deployment.

**Explanation**

Immutable image tags provide end-to-end traceability from source code to running workloads.

---

### Scenario 5

**Question**

A deployment fails because the Kubernetes manifest contains invalid YAML syntax. How would you troubleshoot?

**Answer**

- Validate the YAML syntax.
- Check indentation.
- Verify required fields.
- Validate API versions.
- Review pipeline logs.
- Test the manifest before deployment.

**Explanation**

YAML formatting errors are a common cause of Kubernetes deployment failures.

---

### Scenario 6

**Question**

A developer accidentally deploys directly to the Production AKS cluster. How can this be prevented?

**Answer**

Implement:

- Separate environments.
- Environment approvals.
- RBAC.
- Dedicated Service Connections.
- Protected branches.
- Production deployment approvals.

**Explanation**

Production deployments should follow controlled approval and authorization processes.

---

### Scenario 7

**Question**

Your AKS deployment fails because the Docker image cannot be pulled. What would you investigate?

**Answer**

Check:

- Azure Container Registry.
- Image name.
- Image tag.
- Registry authentication.
- AKS permissions.
- Image availability.

**Explanation**

Most image pull failures occur because the image does not exist, the tag is incorrect, or the cluster lacks permission to access the registry.

---

### Scenario 8

**Question**

Your organization uses Development, QA, and Production AKS clusters. How would you manage deployments?

**Answer**

Create:

- Separate Azure DevOps Environments.
- Separate Service Connections.
- Environment-specific Kubernetes manifests or configuration overlays.
- Approval workflows for Production.

**Explanation**

Environment isolation improves governance, security, and deployment reliability.

---

### Scenario 9

**Question**

Your deployment succeeds, but the new Pods repeatedly restart. How would you troubleshoot?

**Answer**

Check:

- Pod logs.
- Application startup errors.
- Environment variables.
- Secrets and ConfigMaps.
- Readiness probes.
- Liveness probes.
- Resource limits.

**Explanation**

Repeated restarts usually indicate application configuration issues, missing dependencies, or health check failures rather than deployment errors.

---

### Scenario 10

**Question**

Your manager wants every deployment to use the Kubernetes Manifest Task instead of manually running `kubectl apply`. Why is this a good practice?

**Answer**

The Kubernetes Manifest Task provides:

- Standardized deployments.
- Built-in deployment tracking.
- Image substitution.
- Better Azure DevOps integration.
- Improved maintainability.
- Easier pipeline management.

**Explanation**

Using the built-in task reduces manual scripting and improves consistency across deployment pipelines.

---

### Scenario 11

**Question**

During a production deployment, the Kubernetes rollout fails because some Pods never become ready. What would you do?

**Answer**

- Review the Deployment rollout status.
- Inspect Pod events and logs.
- Verify readiness and liveness probe configuration.
- Check image availability and startup configuration.
- Confirm required Secrets and ConfigMaps are present.
- Resolve the underlying issue and redeploy.
- If necessary, perform a rollback to the previous stable image.

**Explanation**

A failed rollout usually indicates that Kubernetes cannot bring the new application version into a healthy state. Investigating Pod health, configuration, and application startup issues helps identify the root cause before deciding whether to retry or roll back the deployment.
