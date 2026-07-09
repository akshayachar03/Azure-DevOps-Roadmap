# Terraform Infrastructure as Code (IaC) Fundamentals & Installation Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Infrastructure as Code (IaC)?

**Answer**

Infrastructure as Code (IaC) is the practice of provisioning, configuring, and managing infrastructure using code instead of performing manual operations.

Examples of infrastructure managed using IaC include:

- Virtual Machines
- Virtual Networks
- Storage Accounts
- Kubernetes Clusters
- Databases
- Load Balancers

Terraform uses configuration files (`.tf`) to define infrastructure.

**Explanation**

IaC makes infrastructure repeatable, version-controlled, automated, and consistent across environments.

**Used in Production**

- Cloud provisioning
- Environment automation
- Disaster recovery
- CI/CD infrastructure deployment

**Common Mistake**

Thinking Terraform manages only cloud resources. It can also manage SaaS platforms, DNS, Kubernetes, GitHub, and many other providers.

---

### Question 2

**Question**

What are the benefits of Infrastructure as Code?

**Answer**

Major benefits include:

- Automation
- Consistency
- Version Control
- Reduced Human Errors
- Faster Deployments
- Easy Rollback
- Reusable Infrastructure
- Better Collaboration

**Explanation**

IaC eliminates repetitive manual tasks and ensures identical infrastructure can be recreated whenever needed.

**Used in Production**

DevOps pipelines and cloud infrastructure management.

**Common Mistake**

Using manual portal changes after Terraform deployment, causing infrastructure drift.

---

### Question 3

**Question**

What is the difference between Declarative and Imperative Infrastructure as Code?

**Answer**

| Declarative | Imperative |
|-------------|------------|
| Defines the desired final state | Defines the exact steps to reach the final state |
| Terraform uses this approach | Shell scripts and many automation tools use this approach |
| Focuses on "What" | Focuses on "How" |

**Explanation**

Terraform automatically determines the sequence of operations required to reach the desired state.

**Used in Production**

Modern cloud provisioning.

**Common Mistake**

Expecting Terraform to execute resources in the exact order they are written instead of relying on dependencies.

---

### Question 4

**Question**

What is Terraform?

**Answer**

Terraform is an open-source Infrastructure as Code (IaC) tool developed by HashiCorp that provisions and manages infrastructure using declarative configuration files.

Terraform supports providers such as:

- Azure
- AWS
- Google Cloud
- Kubernetes
- Docker
- GitHub
- VMware

**Explanation**

Terraform enables infrastructure automation using a single workflow across multiple platforms.

**Used in Production**

Cloud provisioning and infrastructure lifecycle management.

---

### Question 5

**Question**

Explain the Terraform architecture.

**Answer**

Terraform architecture consists of:

- Terraform CLI
- Configuration Files (`.tf`)
- Providers
- State File
- APIs of Cloud Providers

Workflow:

```
Terraform Configuration
        ↓
Terraform CLI
        ↓
Provider Plugin
        ↓
Cloud Provider API
        ↓
Infrastructure
```

**Explanation**

Terraform translates configuration files into API calls through provider plugins.

**Used in Production**

Provisioning infrastructure across multiple cloud platforms.

---

### Question 6

**Question**

Explain the Terraform workflow.

**Answer**

The standard Terraform workflow is:

1. Write Configuration
2. Initialize (`terraform init`)
3. Validate (`terraform validate`)
4. Preview Changes (`terraform plan`)
5. Apply Changes (`terraform apply`)
6. Destroy Infrastructure (`terraform destroy`) when required

**Explanation**

Each command has a specific purpose, ensuring infrastructure changes are reviewed before deployment.

**Used in Production**

Every Terraform project.

**Common Mistake**

Running `terraform apply` without reviewing the execution plan.

---

### Question 7

**Question**

How do you install Terraform?

**Answer**

Installation steps:

1. Download Terraform from HashiCorp.
2. Extract the binary.
3. Add it to the system PATH.
4. Verify installation.

Example:

```bash
terraform version
```

**Explanation**

Adding Terraform to the PATH allows it to be executed from any terminal.

**Used in Production**

Developer workstations, CI/CD agents, and automation servers.

---

### Question 8

**Question**

What is the Terraform CLI?

**Answer**

The Terraform CLI is the command-line interface used to manage infrastructure.

Common commands include:

- `terraform init`
- `terraform validate`
- `terraform plan`
- `terraform apply`
- `terraform destroy`
- `terraform fmt`

**Explanation**

The CLI performs initialization, planning, deployment, validation, formatting, and destruction of infrastructure.

**Used in Production**

Daily infrastructure automation.

---

### Question 9

**Question**

How do you verify that Terraform is installed correctly?

**Answer**

Run:

```bash
terraform version
```

If Terraform is installed successfully, it displays:

- Terraform version
- Installed provider versions (when initialized)

**Explanation**

This confirms that the executable is available in the system PATH.

**Used in Production**

Before configuring or deploying infrastructure.

**Common Mistake**

Installing Terraform but forgetting to update the PATH environment variable.

---

### Question 10

**Question**

What is a Terraform Provider?

**Answer**

A Provider is a plugin that enables Terraform to communicate with a specific platform.

Examples:

- AzureRM
- AWS
- Google
- Kubernetes
- Docker
- GitHub

Example:

```hcl
provider "azurerm" {
  features {}
}
```

**Explanation**

Providers translate Terraform configurations into API requests for the target platform.

**Used in Production**

Every Terraform deployment.

**Common Mistake**

Assuming providers are built into Terraform. They are downloaded during initialization.

---

### Question 11

**Question**

What happens during `terraform init`?

**Answer**

`terraform init` performs several tasks:

- Downloads provider plugins
- Initializes the working directory
- Configures backend (if defined)
- Prepares Terraform for execution

Example:

```bash
terraform init
```

**Explanation**

Initialization must be performed before running `plan` or `apply`.

**Used in Production**

First step in every Terraform project.

**Common Mistake**

Editing provider configurations but forgetting to rerun `terraform init`.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A new developer clones your Terraform repository and immediately runs `terraform apply`, but the command fails because the provider is missing. What should they do?

**Answer**

Run:

```bash
terraform init
```

This downloads the required provider plugins and initializes the working directory.

**Explanation**

Terraform cannot communicate with cloud providers until the required provider plugins are installed.

---

### Scenario 2

**Question**

Your team manually creates Azure resources through the Azure Portal after Terraform has already provisioned the environment. What problem can this cause?

**Answer**

It can cause **Infrastructure Drift**, where the actual infrastructure differs from Terraform's expected state.

**Explanation**

Infrastructure drift leads to inconsistent deployments and unexpected changes during future Terraform runs.

---

### Scenario 3

**Question**

A Terraform deployment fails immediately with "terraform: command not found." How would you troubleshoot it?

**Answer**

Check:

- Terraform installation
- PATH environment variable
- Terminal restart
- Installation directory
- `terraform version`

**Explanation**

This error usually indicates that Terraform is either not installed or not accessible through the system PATH.

---

### Scenario 4

**Question**

Your organization wants identical Development, QA, and Production environments. Why would Terraform be a good choice?

**Answer**

Terraform uses reusable configuration files that provision identical infrastructure across multiple environments with minimal changes, such as different variable values.

**Explanation**

IaC ensures consistency, repeatability, and reduces manual configuration errors.

---

### Scenario 5

**Question**

A colleague edits Terraform configuration files and immediately runs `terraform apply` without reviewing the changes. Why is this risky?

**Answer**

They may unknowingly create, modify, or delete infrastructure.

The recommended workflow is:

1. `terraform validate`
2. `terraform plan`
3. Review the execution plan
4. `terraform apply`

**Explanation**

Reviewing the plan helps identify unintended infrastructure changes before they occur.

---

### Scenario 6

**Question**

Your Terraform configuration uses the AzureRM provider, but initialization fails while downloading plugins. What would you investigate?

**Answer**

Check:

- Internet connectivity
- Provider version constraints
- Proxy configuration
- Firewall restrictions
- HashiCorp registry availability

**Explanation**

Provider plugins are downloaded during `terraform init`, so connectivity issues commonly cause initialization failures.

---

### Scenario 7

**Question**

Your team wants to manage Azure and GitHub resources from the same Terraform project. Is this possible?

**Answer**

Yes. Terraform supports multiple providers in a single project.

Example:

- AzureRM Provider
- GitHub Provider

Terraform communicates with each provider independently.

**Explanation**

Multi-provider support is one of Terraform's strengths for automating complete infrastructure ecosystems.

---

### Scenario 8

**Question**

After installing Terraform, one engineer has version 1.8 while another has version 1.10. Could this create issues?

**Answer**

Yes. Different Terraform versions may introduce behavioral changes, provider compatibility differences, or new language features.

Teams should standardize on a supported Terraform version.

**Explanation**

Version consistency improves reproducibility and avoids unexpected pipeline failures.

---

### Scenario 9

**Question**

Your company wants every infrastructure change to go through code review before deployment. How does Terraform support this?

**Answer**

Terraform configuration files are stored in Git repositories. Engineers submit Pull Requests, reviewers examine both the code and the `terraform plan` output, and only approved changes are applied.

**Explanation**

Treating infrastructure as code enables the same review and approval process used for application code.

---

### Scenario 10

**Question**

A manager asks why the team should use Terraform instead of creating resources manually through the Azure Portal. How would you explain?

**Answer**

Terraform provides:

- Repeatable deployments
- Version-controlled infrastructure
- Automation
- Faster provisioning
- Reduced human errors
- Easy disaster recovery
- Consistent environments
- Better collaboration through code reviews

**Explanation**

Manual portal-based provisioning is difficult to reproduce, audit, and scale, whereas Terraform delivers predictable, automated, and maintainable infrastructure management.
