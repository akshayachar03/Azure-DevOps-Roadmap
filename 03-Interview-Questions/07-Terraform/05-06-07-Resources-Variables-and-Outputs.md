# Terraform Resources, Variables & Outputs Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is a Resource in Terraform?

**Answer**

A resource is the fundamental building block in Terraform that represents an infrastructure object managed by a provider, such as a Virtual Machine, Resource Group, Storage Account, VPC, or EC2 instance.

Example:

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "demo-rg"
  location = "East US"
}
```

**Explanation**

A resource block tells Terraform **what infrastructure to create, modify, or delete**. Every managed object in Terraform is defined as a resource.

**Used in Production**

- Azure Virtual Machines
- AWS EC2 Instances
- Storage Accounts
- Virtual Networks
- Kubernetes Clusters

**Common Mistake**

Confusing a resource with a provider. The provider connects to the cloud, while the resource defines the infrastructure to be managed.

---

### Question 2

**Question**

What is the structure of a Resource Block in Terraform?

**Answer**

A resource block has the following structure:

```hcl
resource "<PROVIDER_RESOURCE_TYPE>" "<LOCAL_NAME>" {

}
```

Example:

```hcl
resource "aws_instance" "web" {
  ami           = "ami-12345"
  instance_type = "t2.micro"
}
```

- `aws_instance` → Resource type
- `web` → Local resource name

**Explanation**

Terraform identifies each resource using its type and local name.

**Used in Production**

Every Terraform project.

**Common Mistake**

Thinking the local name is the cloud resource name. It is only used inside Terraform.

---

### Question 3

**Question**

What are Resource Arguments?

**Answer**

Resource arguments are configuration settings inside a resource block.

Example:

```hcl
resource "azurerm_storage_account" "storage" {
  name                     = "storage001"
  location                 = "East US"
  resource_group_name      = "demo-rg"
  account_tier             = "Standard"
  account_replication_type = "LRS"
}
```

Here:

- name
- location
- account_tier

are arguments.

**Explanation**

Arguments determine how Terraform configures the infrastructure resource.

**Used in Production**

Every Terraform resource requires arguments.

---

### Question 4

**Question**

What are Resource Attributes?

**Answer**

Attributes are values returned after Terraform creates a resource.

Example:

```hcl
azurerm_resource_group.rg.id
```

Other common attributes:

- id
- name
- location
- public_ip
- arn

**Explanation**

Terraform automatically retrieves these values from the cloud provider after resource creation.

**Used in Production**

Used for referencing one resource from another.

**Common Mistake**

Trying to manually define automatically generated attributes like IDs.

---

### Question 5

**Question**

What are Resource Dependencies in Terraform?

**Answer**

Dependencies determine the order in which Terraform creates resources.

Example:

```hcl
Resource Group
      ↓
Storage Account
      ↓
Virtual Machine
```

Terraform automatically detects dependencies through references.

Example:

```hcl
resource_group_name = azurerm_resource_group.rg.name
```

**Explanation**

Terraform builds a dependency graph to ensure infrastructure is created in the correct order.

**Used in Production**

Creating networks before virtual machines, or resource groups before dependent resources.

**Common Mistake**

Using hardcoded names instead of resource references, which breaks dependency tracking.

---

### Question 6

**Question**

What are Input Variables in Terraform?

**Answer**

Input variables make Terraform configurations reusable by allowing values to be provided at runtime.

Example:

```hcl
variable "location" {
  type = string
}
```

Usage:

```hcl
location = var.location
```

**Explanation**

Variables eliminate hardcoded values and support multiple environments.

**Used in Production**

Development, QA, Staging, and Production deployments.

---

### Question 7

**Question**

What variable types are supported in Terraform?

**Answer**

Common variable types include:

- string
- number
- bool
- list
- map
- object
- tuple
- set

Example:

```hcl
variable "vm_size" {
  type = string
}
```

**Explanation**

Terraform validates variable values based on their declared types.

**Used in Production**

Ensures consistent and error-free configurations.

**Common Mistake**

Using the wrong data type, leading to validation errors.

---

### Question 8

**Question**

How can variable values be provided in Terraform?

**Answer**

Variable values can be supplied using:

- Default values
- `.tfvars` files
- Command-line flags
- Environment variables
- Terraform Cloud variables

Example:

```bash
terraform apply -var="location=East US"
```

**Explanation**

Terraform follows a variable precedence order when determining which value to use.

**Used in Production**

Environment-specific deployments.

---

### Question 9

**Question**

What is a `.tfvars` file?

**Answer**

A `.tfvars` file stores variable values separately from the Terraform configuration.

Example:

```hcl
location = "East US"
vm_size  = "Standard_B2s"
```

Command:

```bash
terraform apply -var-file="dev.tfvars"
```

**Explanation**

`.tfvars` files simplify deployments across multiple environments.

**Used in Production**

Separate configuration for Development, QA, and Production.

**Common Mistake**

Committing sensitive `.tfvars` files containing secrets to Git.

---

### Question 10

**Question**

How are Environment Variables used with Terraform?

**Answer**

Terraform automatically reads variables prefixed with `TF_VAR_`.

Example:

Linux:

```bash
export TF_VAR_location="East US"
```

Terraform automatically assigns this value to:

```hcl
variable "location"
```

**Explanation**

Environment variables are useful in CI/CD pipelines and automation.

**Used in Production**

Azure DevOps, Jenkins, GitHub Actions, GitLab CI.

---

### Question 11

**Question**

What are Outputs in Terraform?

**Answer**

Outputs expose useful information after infrastructure is created.

Example:

```hcl
output "resource_group_name" {
  value = azurerm_resource_group.rg.name
}
```

**Explanation**

Outputs display important resource information without manually querying the cloud.

**Used in Production**

Displaying:

- VM IP Address
- Storage Account Name
- Resource IDs
- Load Balancer DNS

**Common Mistake**

Forgetting to define outputs and manually searching for resource information.

---

### Question 12

**Question**

How can one resource reference another resource or output in Terraform?

**Answer**

Terraform references resources using:

```hcl
resource_type.resource_name.attribute
```

Example:

```hcl
azurerm_resource_group.rg.name
```

Outputs can also reference resources:

```hcl
output "rg_name" {
  value = azurerm_resource_group.rg.name
}
```

**Explanation**

References create automatic dependencies and eliminate hardcoded values.

**Used in Production**

Connecting multiple resources within the same Terraform project.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A Virtual Machine creation fails because the Resource Group does not exist. How would you resolve this?

**Answer**

Reference the Resource Group directly instead of hardcoding its name.

Example:

```hcl
resource_group_name = azurerm_resource_group.rg.name
```

**Explanation**

Terraform automatically detects the dependency and creates the Resource Group before the Virtual Machine.

---

### Scenario 2

**Question**

Your organization has separate Development, QA, and Production environments. How would you avoid maintaining three different Terraform configurations?

**Answer**

Use input variables and separate `.tfvars` files.

Example:

```
dev.tfvars

qa.tfvars

prod.tfvars
```

**Explanation**

The same Terraform code can be reused by supplying different variable files for each environment.

---

### Scenario 3

**Question**

A teammate hardcodes the Azure location in every resource block. What improvement would you recommend?

**Answer**

Create a variable:

```hcl
variable "location" {}
```

Then use:

```hcl
location = var.location
```

**Explanation**

Variables improve maintainability and simplify deployments across multiple regions.

---

### Scenario 4

**Question**

Your Jenkins pipeline needs the public IP of a newly created Virtual Machine. How would Terraform provide it?

**Answer**

Create an output.

Example:

```hcl
output "vm_public_ip" {
  value = azurerm_public_ip.vm.ip_address
}
```

**Explanation**

Outputs expose resource information for CI/CD pipelines and automation scripts.

---

### Scenario 5

**Question**

Your Terraform deployment uses the same storage account name across multiple environments, causing conflicts. How would you solve this?

**Answer**

Parameterize the name using variables or environment-specific values.

Example:

```hcl
name = "${var.environment}storage001"
```

**Explanation**

Unique resource names prevent deployment failures and improve environment isolation.

---

### Scenario 6

**Question**

A deployment requires different VM sizes for Development and Production. How would you implement this?

**Answer**

Define a variable:

```hcl
variable "vm_size" {}
```

Provide different values in each `.tfvars` file.

**Explanation**

This allows the same Terraform codebase to deploy environment-specific infrastructure.

---

### Scenario 7

**Question**

A developer manually copies a Resource ID into another resource instead of referencing it. Why is this a bad practice?

**Answer**

Manual values can become outdated and prevent Terraform from tracking dependencies.

Instead, reference the resource directly:

```hcl
azurerm_resource_group.rg.id
```

**Explanation**

Resource references keep configurations dynamic and ensure correct creation order.

---

### Scenario 8

**Question**

Your Azure DevOps pipeline should not expose secrets inside `.tfvars` files. How would you securely provide variable values?

**Answer**

Store sensitive values as pipeline variables or environment variables using the `TF_VAR_` prefix.

**Explanation**

Sensitive data should be managed by secret stores or CI/CD platforms rather than committed to source control.

---

### Scenario 9

**Question**

After provisioning infrastructure, the operations team asks for the Load Balancer IP address. How would you make it easily available?

**Answer**

Create an output:

```hcl
output "lb_ip" {
  value = azurerm_public_ip.lb.ip_address
}
```

**Explanation**

Outputs provide important deployment information without additional cloud queries.

---

### Scenario 10

**Question**

A teammate creates multiple resources using hardcoded names and values. What best practices would you recommend?

**Answer**

Recommend using:

- Input variables
- Resource references
- `.tfvars` files
- Outputs
- Consistent naming conventions

**Explanation**

These practices improve reusability, reduce duplication, simplify maintenance, and make Terraform configurations suitable for enterprise-scale infrastructure.
