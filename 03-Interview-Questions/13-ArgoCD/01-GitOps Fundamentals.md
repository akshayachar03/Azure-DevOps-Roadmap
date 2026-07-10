# GitOps Fundamentals Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is GitOps?

**Answer**

GitOps is a deployment methodology that uses Git as the single source of truth for both infrastructure and application configurations. Changes are made by updating files in Git, and a GitOps tool such as ArgoCD automatically synchronizes those changes with the target environment.

**Explanation**

GitOps extends Infrastructure as Code by using Git repositories to manage the entire deployment lifecycle. Instead of manually applying changes to a cluster, engineers update manifests in Git. The GitOps controller continuously monitors the repository and ensures the cluster matches the desired configuration.

**Where it is used in Production**

- Kubernetes deployments
- Application delivery
- Infrastructure management
- Multi-cluster environments

**Common Mistake**

Many candidates think GitOps is just storing YAML files in Git. GitOps also requires automated reconciliation between Git and the actual environment.

---

### Question 2

**Question**

What is the main purpose of GitOps?

**Answer**

The main purpose of GitOps is to automate deployments while ensuring that the running environment always matches the configuration stored in Git.

**Explanation**

GitOps improves consistency, traceability, security, and rollback capabilities because every infrastructure or application change is version-controlled.

**Where it is used in Production**

Organizations use GitOps to automate deployments to Kubernetes clusters while reducing manual intervention.

**Common Mistake**

Some candidates believe GitOps replaces CI/CD. In reality, GitOps complements CI/CD by automating deployments after CI pipelines complete.

---

### Question 3

**Question**

What is meant by "Git as the Single Source of Truth"?

**Answer**

It means that Git contains the authoritative and approved configuration for infrastructure and applications. The actual environment should always match what is stored in Git.

**Explanation**

Engineers should make configuration changes only through Git commits or pull requests. Direct changes to production clusters are avoided.

**Where it is used in Production**

- Kubernetes manifests
- Helm charts
- Infrastructure configuration
- Application deployment manifests

**Common Mistake**

Candidates often assume manual kubectl changes are acceptable. In GitOps, manual changes are treated as configuration drift and are usually reverted.

---

### Question 4

**Question**

What is Desired State in GitOps?

**Answer**

Desired State is the intended configuration of infrastructure or applications stored in Git.

**Explanation**

The GitOps controller continuously compares the actual cluster state with the desired state defined in Git. If differences are detected, it automatically reconciles them.

**Where it is used in Production**

Every Kubernetes deployment managed through ArgoCD relies on the desired state concept.

**Common Mistake**

Many candidates confuse desired state with the current running state. Desired state is the target configuration stored in Git.

---

### Question 5

**Question**

What is Declarative Configuration?

**Answer**

Declarative Configuration defines the final desired outcome rather than the steps required to achieve it.

**Explanation**

In Kubernetes, YAML manifests describe what resources should exist. Kubernetes and GitOps controllers determine how to reach that state.

**Where it is used in Production**

- Kubernetes manifests
- Helm charts
- Kustomize
- ArgoCD deployments

**Common Mistake**

Some candidates confuse declarative and imperative approaches. Declarative focuses on the desired end state, while imperative specifies each command.

---

### Question 6

**Question**

What is the difference between Declarative and Imperative configuration?

**Answer**

- **Declarative:** Specifies the desired end state.
- **Imperative:** Specifies the exact commands to execute.

**Explanation**

GitOps relies on declarative configuration because it enables automatic reconciliation and easier version control.

**Where it is used in Production**

Declarative configuration is the standard approach for Kubernetes and GitOps platforms.

---

### Question 7

**Question**

What is Pull-Based Deployment in GitOps?

**Answer**

Pull-Based Deployment means the GitOps controller running inside the Kubernetes cluster continuously pulls changes from Git and applies them automatically.

**Explanation**

Instead of external systems pushing changes into the cluster, the cluster itself retrieves approved configurations from Git.

**Where it is used in Production**

ArgoCD continuously monitors Git repositories and synchronizes changes with Kubernetes clusters.

**Common Mistake**

Many candidates mistakenly believe CI pipelines deploy applications directly in GitOps workflows.

---

### Question 8

**Question**

Why is Pull-Based Deployment preferred over Push-Based Deployment in GitOps?

**Answer**

Pull-based deployments improve security because external CI systems do not require direct access to production clusters.

**Explanation**

The GitOps controller securely runs inside the cluster and performs deployments after detecting changes in Git.

**Where it is used in Production**

Enterprise Kubernetes platforms commonly use pull-based deployments to reduce security risks.

---

### Question 9

**Question**

How does GitOps improve deployment reliability?

**Answer**

GitOps improves reliability through:

- Version-controlled configuration
- Automated synchronization
- Automatic drift correction
- Easy rollback
- Consistent deployments

**Explanation**

Since deployments are fully automated and version-controlled, configuration errors and manual mistakes are significantly reduced.

**Where it is used in Production**

Cloud-native production environments.

---

### Question 10

**Question**

What are the major benefits of GitOps?

**Answer**

Benefits include:

- Automated deployments
- Version control
- Easy rollback
- Audit trail
- Improved security
- Faster recovery
- Reduced manual effort
- Consistent environments

**Explanation**

GitOps simplifies operations while making deployments more predictable and repeatable.

**Where it is used in Production**

Modern DevOps teams managing Kubernetes clusters.

---

### Question 11

**Question**

How does GitOps support collaboration among development and operations teams?

**Answer**

All infrastructure and deployment changes are made through Git pull requests, allowing code reviews, approvals, and version tracking before deployment.

**Explanation**

Git becomes the collaboration platform for infrastructure and application changes, improving visibility and accountability.

**Where it is used in Production**

Enterprise DevOps workflows where multiple teams manage shared environments.

---

### Question 12

**Question**

What happens if someone manually changes a Kubernetes resource managed by GitOps?

**Answer**

The GitOps controller detects the configuration drift and automatically restores the resource to match the desired state stored in Git.

**Explanation**

Continuous reconciliation ensures the running environment remains consistent with the approved configuration.

**Where it is used in Production**

Production Kubernetes clusters managed using ArgoCD.

**Common Mistake**

Candidates often think manual changes remain permanent. In GitOps, unauthorized manual changes are typically overwritten during synchronization.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A developer manually changes the replica count of a Deployment in the Kubernetes cluster. A few minutes later, the replica count returns to its previous value. Why did this happen?

**Answer**

The GitOps controller detected that the cluster configuration no longer matched the desired state stored in Git and automatically synchronized it back.

**Explanation**

GitOps continuously reconciles the actual cluster state with the desired state, correcting configuration drift.

---

### Scenario 2

**Question**

Your organization wants every infrastructure change to be reviewed before deployment. How does GitOps help?

**Answer**

All changes are made through Git pull requests, where reviewers approve modifications before merging. The GitOps controller deploys only the approved changes.

**Explanation**

Git provides version control, approvals, and an audit trail for every deployment.

---

### Scenario 3

**Question**

An engineer directly updates a Kubernetes Service using `kubectl edit`. Why is this considered a bad practice in GitOps?

**Answer**

The change bypasses Git, creating configuration drift. The GitOps controller will eventually overwrite the manual modification to match the Git repository.

**Explanation**

Git should always remain the single source of truth.

---

### Scenario 4

**Question**

Your security team does not want the CI server to have direct access to the production Kubernetes cluster. How does GitOps solve this?

**Answer**

The CI pipeline only updates the Git repository. The GitOps controller inside the cluster pulls the approved changes and applies them.

**Explanation**

This pull-based model reduces the attack surface by eliminating direct cluster access from external systems.

---

### Scenario 5

**Question**

A deployment introduces a bug into production. How can GitOps simplify the rollback process?

**Answer**

Revert the commit in Git to the previous stable version. The GitOps controller automatically synchronizes the cluster with the reverted configuration.

**Explanation**

Git history provides a simple and reliable rollback mechanism.

---

### Scenario 6

**Question**

Your development and production environments are configured differently because engineers made manual changes over time. How would GitOps prevent this?

**Answer**

Both environments should be managed from version-controlled Git repositories, ensuring deployments are consistent and reproducible.

**Explanation**

GitOps eliminates configuration drift between environments.

---

### Scenario 7

**Question**

During an interview, you are asked why GitOps is considered declarative rather than imperative. How would you answer?

**Answer**

GitOps stores the desired configuration in Git using declarative manifests. The GitOps controller determines how to make the cluster match that configuration instead of executing manually defined deployment commands.

**Explanation**

The focus is on the desired end state rather than execution steps.

---

### Scenario 8

**Question**

A deployment succeeds in the CI pipeline, but no changes appear in the Kubernetes cluster. What would you check first?

**Answer**

I would verify whether the updated manifests were committed to the correct Git repository and branch monitored by the GitOps controller.

**Explanation**

GitOps deployments begin only after changes are committed to the configured Git repository.

---

### Scenario 9

**Question**

Your manager asks why Git is called the "Single Source of Truth" in GitOps. How would you explain it?

**Answer**

Git stores the approved configuration for infrastructure and applications. The GitOps controller continuously ensures the running environment matches what is stored in Git, making Git the authoritative source.

**Explanation**

Any configuration outside Git is considered temporary or unauthorized.

---

### Scenario 10

**Question**

Your organization wants deployment history, approval records, and rollback capability without additional tools. How does GitOps provide these features?

**Answer**

Git naturally provides commit history, pull request approvals, version tracking, and rollback through commit reverts. GitOps leverages these built-in Git capabilities for deployment management.

**Explanation**

This is one of the primary reasons GitOps has become the preferred deployment model for Kubernetes-based environments.
