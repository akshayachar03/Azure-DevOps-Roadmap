# Terraform Modules Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is a Module in Terraform?

**Answer**

A Terraform module is a reusable collection of Terraform configuration files that groups related resources together to simplify infrastructure deployment and management.

Example:

```hcl
module "network" {
  source = "./modules/network"
}
```

**Explanation**

Modules help eliminate duplicate code by encapsulating infrastructure components into reusable units.

For example, instead of repeatedly defining a Virtual Network, Subnets, and Network Security Groups in multiple projects, you can create a module and reuse it.

**Used in Production**

- Virtual Networks
- Virtual Machines
- Kubernetes Clusters
- Storage Accounts
- Resource Groups

**Common Mistake**

Copying the same Terraform code across projects instead of creating reusable modules.

---

### Question 2

**Question**

What is the difference between the Root Module and a Child Module?

**Answer**

The **Root Module** is the main Terraform configuration executed directly using Terraform commands.

The **Child Module** is a module called from another module or the root module.

Example:

```
terraform-project/

main.tf
variables.tf
outputs.tf
```

This is the Root Module.

```
modules/

vm/
network/
storage/
```

These are Child Modules.

**Explanation**

Terraform always starts execution from the Root Module, which can invoke one or more Child Modules.

**Used in Production**

Enterprise projects typically have one Root Module and multiple reusable Child Modules.

---

### Question 3

**Question**

Why are Modules important in Terraform?

**Answer**

Modules provide:

- Code reusability
- Standardization
- Easier maintenance
- Reduced duplication
- Better collaboration

**Explanation**

Instead of writing the same infrastructure code multiple times, modules allow teams to maintain a single implementation and reuse it across projects.

**Used in Production**

Organizations commonly maintain shared modules for networking, compute, storage, and security.

---

### Question 4

**Question**

How do you call a Module in Terraform?

**Answer**

Modules are called using the `module` block.

Example:

```hcl
module "network" {

  source = "./modules/network"

}
```

Example with inputs:

```hcl
module "vm" {

  source   = "./modules/vm"

  vm_name  = "web01"

  location = "East US"

}
```

**Explanation**

The `source` argument specifies where Terraform can find the module.

**Used in Production**

Deploying reusable infrastructure across multiple environments.

---

### Question 5

**Question**

What are Module Inputs?

**Answer**

Module inputs are variables passed from the Root Module to a Child Module.

Child Module:

```hcl
variable "location" {}
```

Root Module:

```hcl
module "storage" {

  source = "./modules/storage"

  location = "East US"

}
```

**Explanation**

Module inputs make modules configurable and reusable.

**Used in Production**

Passing:

- Environment names
- Resource names
- Locations
- VM sizes
- Tags

**Common Mistake**

Hardcoding values inside modules instead of using input variables.

---

### Question 6

**Question**

What are Module Outputs?

**Answer**

Module outputs expose values from a Child Module back to the Root Module.

Child Module:

```hcl
output "vm_id" {

  value = azurerm_linux_virtual_machine.vm.id

}
```

Root Module:

```hcl
module.vm.vm_id
```

**Explanation**

Outputs allow information created inside a module to be used elsewhere.

**Used in Production**

Returning:

- Resource IDs
- Public IPs
- DNS names
- Storage Account Names

---

### Question 7

**Question**

What is a Local Module?

**Answer**

A Local Module is stored within the same project directory.

Example:

```
modules/

network/

storage/

vm/
```

Reference:

```hcl
module "network" {

  source = "./modules/network"

}
```

**Explanation**

Local modules are ideal for small projects and internal reusable components.

**Used in Production**

Enterprise repositories often organize infrastructure into multiple local modules.

---

### Question 8

**Question**

What is the typical directory structure for Terraform Modules?

**Answer**

Example:

```
terraform-project/

main.tf

variables.tf

outputs.tf

modules/

├── network

│   ├── main.tf

│   ├── variables.tf

│   └── outputs.tf

├── storage

└── vm
```

**Explanation**

Each module usually contains:

- main.tf
- variables.tf
- outputs.tf

This organization improves maintainability.

---

### Question 9

**Question**

Can one Terraform Module call another Module?

**Answer**

Yes.

A Child Module can call another Child Module.

Example:

```
Root Module

↓

Network Module

↓

Security Module
```

**Explanation**

Terraform supports nested modules, allowing complex infrastructure to be built from smaller reusable components.

**Used in Production**

Large enterprise deployments with layered infrastructure.

---

### Question 10

**Question**

What are the benefits of using Modules in large Terraform projects?

**Answer**

Benefits include:

- Reusability
- Easier maintenance
- Standardized deployments
- Smaller configuration files
- Better collaboration
- Faster development
- Consistent infrastructure

**Explanation**

Modules reduce duplication and improve consistency across environments.

**Used in Production**

Organizations managing hundreds of cloud resources.

---

### Question 11

**Question**

How do Modules improve Infrastructure as Code (IaC)?

**Answer**

Modules encourage reusable, modular, and maintainable Infrastructure as Code.

Instead of duplicating infrastructure definitions, teams create standardized modules that are reused across environments.

**Explanation**

This improves consistency, reduces errors, and simplifies updates.

**Used in Production**

Shared platform modules maintained by DevOps teams.

---

### Question 12

**Question**

What are some best practices when creating Terraform Modules?

**Answer**

Best practices include:

- Keep modules focused on a single purpose.
- Use input variables instead of hardcoded values.
- Expose only necessary outputs.
- Use descriptive names.
- Organize files into `main.tf`, `variables.tf`, and `outputs.tf`.
- Document module usage.
- Version modules when shared across teams.

**Explanation**

Well-designed modules are easier to reuse, test, and maintain over time.

**Used in Production**

Enterprise Infrastructure as Code repositories.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Your team has copied the same Virtual Machine configuration into ten different Terraform projects. How would you improve this?

**Answer**

Create a reusable VM module and call it from each project.

**Explanation**

A single module eliminates duplicate code and ensures that updates only need to be made in one place.

---

### Scenario 2

**Question**

Development and Production environments deploy identical infrastructure with different VM sizes and locations. How would you avoid maintaining separate Terraform code?

**Answer**

Create a reusable module and pass different values using module input variables.

Example:

```hcl
module "vm" {

  vm_size = "Standard_B2s"

}
```

or

```hcl
module "vm" {

  vm_size = "Standard_D4s_v3"

}
```

**Explanation**

The same module can deploy multiple environments with different configurations.

---

### Scenario 3

**Question**

A networking team has already created a standardized Virtual Network module. Your project needs networking. What should you do?

**Answer**

Reuse the existing module instead of creating another network configuration.

**Explanation**

Reusing standardized modules ensures consistency and reduces maintenance effort.

---

### Scenario 4

**Question**

Your Root Module needs the public IP address created inside a VM module. How can it access the value?

**Answer**

Create an output in the Child Module and reference it from the Root Module.

Example:

```hcl
module.vm.public_ip
```

**Explanation**

Outputs allow data to flow from Child Modules to the Root Module.

---

### Scenario 5

**Question**

A developer hardcodes the Azure region inside a Child Module. Why is this a poor practice?

**Answer**

Hardcoded values reduce module reusability. Instead, define the region as an input variable.

**Explanation**

Input variables allow the same module to be deployed in multiple regions without code changes.

---

### Scenario 6

**Question**

Your organization wants all projects to use identical tagging standards. How would Terraform Modules help?

**Answer**

Create a shared module that accepts resource-specific inputs while applying a standardized tagging strategy.

**Explanation**

This ensures consistent governance and compliance across all deployments.

---

### Scenario 7

**Question**

A Child Module creates a Storage Account, and another module needs its name. How should this information be shared?

**Answer**

Expose the Storage Account name using an output in the first module and reference that output where needed.

**Explanation**

Module outputs enable clean communication between modules without hardcoding values.

---

### Scenario 8

**Question**

A Terraform repository has one large `main.tf` file containing hundreds of resources. What would you recommend?

**Answer**

Refactor the configuration into smaller modules such as:

- Network Module
- Compute Module
- Storage Module
- Security Module

**Explanation**

Smaller modules improve readability, maintainability, testing, and team collaboration.

---

### Scenario 9

**Question**

A DevOps engineer modifies the networking configuration separately in every project, leading to inconsistent infrastructure. How can this be avoided?

**Answer**

Maintain a single shared networking module and update it centrally.

**Explanation**

Standardized modules ensure that infrastructure remains consistent across all projects.

---

### Scenario 10

**Question**

A new application requires the same infrastructure pattern used by several existing applications. What is the fastest and most reliable deployment approach?

**Answer**

Reuse the existing Terraform modules and provide application-specific values through module inputs.

**Explanation**

Reusing proven modules accelerates deployment, minimizes configuration errors, and ensures compliance with organizational standards.
