# Command Line Interface (CLI) for Azure

## Definition

- Azure Command Line Interface (Azure CLI) is a cross-platform command-line tool used to create, manage, and automate Azure resources.
- It can be installed on Windows, Linux, and macOS or used directly in Azure Cloud Shell.
- Azure CLI simplifies resource management without using the Azure Portal.

---

## Why is it used?

- Manage Azure resources from the terminal.
- Automate Azure administration.
- Create deployment scripts.
- Integrate with CI/CD pipelines.
- Perform bulk resource operations.
- Manage Azure remotely.

---

## Key Features

- Cross-platform (Windows, Linux, macOS).
- Supports Bash and PowerShell.
- Uses simple `az` commands.
- Supports JSON output.
- Supports scripting and automation.
- Integrates with Azure Cloud Shell.
- Supports authentication using Azure AD.

---

## Advantages

- Faster than Portal for repetitive tasks.
- Excellent for automation.
- Easy integration with DevOps tools.
- Free to use.
- Supports all Azure services.

---

## Disadvantages

- Requires learning command syntax.
- Errors can affect live resources if commands are incorrect.

---

## Components

### Azure CLI

- Main command-line tool.

### Azure Cloud Shell

- Browser-based shell with Azure CLI pre-installed.

### Azure Login

- Authenticates users.

### Resource Management

- Create, update, delete, and monitor Azure resources.

---

## Workflow

```text
Install Azure CLI
        ↓
Login to Azure
        ↓
Select Subscription
        ↓
Run az Commands
        ↓
Manage Azure Resources
```

---

## Common Commands

### Check Version

```bash
az version
```

### Login

```bash
az login
```

### List Subscriptions

```bash
az account list
```

### Set Active Subscription

```bash
az account set --subscription "<Subscription Name>"
```

### Logout

```bash
az logout
```

### Get Help

```bash
az --help
```

---

## Real-world Example

A DevOps engineer automates the creation of Virtual Machines, Virtual Networks, and Storage Accounts using Azure CLI inside a deployment script.

---

## Interview Tip

"Azure CLI is Microsoft's cross-platform command-line tool used to automate and manage Azure resources."

---

## Quick Revision

- Starts with `az`.
- Cross-platform.
- Supports automation.
- Works with Cloud Shell.
- Uses Azure AD authentication.
- Can output JSON, Table, YAML, or TSV.

---

## Important Interview Questions

1. What is Azure CLI?
2. Why use Azure CLI instead of the Azure Portal?
3. How do you log in using Azure CLI?
4. Can Azure CLI be used in automation?
5. What is Azure Cloud Shell?

---

# Azure CLI Deep Dive

## Definition

- Azure CLI consists of thousands of commands grouped by Azure services.
- Every command starts with `az` followed by the service name and action.

---

## Why is it used?

- Manage Azure resources efficiently.
- Automate deployments.
- Retrieve resource information.
- Configure Azure services.
- Perform scripting for DevOps.

---

## Command Structure

```text
az <service> <command> <options>
```

Example:

```bash
az vm create
```

- `az` → Azure CLI
- `vm` → Azure Virtual Machine service
- `create` → Action
- `--options` → Parameters

---

## Frequently Used Command Groups

| Command | Purpose |
|----------|----------|
| az group | Manage Resource Groups |
| az vm | Manage Virtual Machines |
| az storage | Manage Storage Accounts |
| az network | Manage Networking |
| az disk | Manage Disks |
| az aks | Manage Kubernetes |
| az sql | Manage SQL Database |
| az webapp | Manage Web Apps |
| az account | Manage Subscription |
| az monitor | Manage Monitoring |

---

## Common Output Formats

| Format | Description |
|---------|-------------|
| json | Default output |
| table | Easy to read |
| yaml | YAML format |
| tsv | Tab separated |
| none | No output |

Example:

```bash
az vm list --output table
```

---

## Useful Commands

### List Resource Groups

```bash
az group list
```

---

### List Virtual Machines

```bash
az vm list --output table
```

---

### Show VM Details

```bash
az vm show --name MyVM --resource-group MyRG
```

---

### List Storage Accounts

```bash
az storage account list
```

---

### Delete Resource Group

```bash
az group delete --name MyRG
```

---

## Workflow

```text
Login
   ↓
Select Subscription
   ↓
Create Resources
   ↓
Verify Resources
   ↓
Update Resources
   ↓
Delete Resources
```

---

## Real-world Example

A Cloud Engineer writes a Bash script using Azure CLI to create an entire development environment in less than five minutes.

---

## Interview Tip

"Azure CLI groups commands by Azure services, making resource management simple and scriptable."

---

## Quick Revision

- Uses `az`.
- Organized by services.
- Supports multiple output formats.
- Easy scripting.
- Supports automation.

---

## Important Interview Questions

1. How are Azure CLI commands structured?
2. What output formats does Azure CLI support?
3. How do you view Azure CLI help?
4. How do you list Azure resources?
5. Which Azure services can Azure CLI manage?

---

# Using Azure CLI to Create Resources on Azure

## Definition

- Azure CLI allows administrators to create and configure Azure resources using commands instead of the Azure Portal.
- This enables fast, repeatable, and automated deployments.

---

## Why is it used?

- Reduce manual work.
- Automate deployments.
- Deploy identical environments.
- Integrate with CI/CD pipelines.
- Improve deployment speed.

---

## Workflow

```text
Login
   ↓
Create Resource Group
   ↓
Create Network
   ↓
Create Storage
   ↓
Create Virtual Machine
   ↓
Verify Deployment
```

---

## Create a Resource Group

```bash
az group create \
--name DemoRG \
--location eastus
```

---

## Create a Virtual Network

```bash
az network vnet create \
--resource-group DemoRG \
--name DemoVNet \
--address-prefix 10.0.0.0/16 \
--subnet-name WebSubnet \
--subnet-prefix 10.0.1.0/24
```

---

## Create a Storage Account

```bash
az storage account create \
--name mystorage12345 \
--resource-group DemoRG \
--location eastus \
--sku Standard_LRS
```

---

## Create a Virtual Machine

```bash
az vm create \
--resource-group DemoRG \
--name DemoVM \
--image Ubuntu2204 \
--admin-username azureuser \
--generate-ssh-keys
```

---

## Open Port 80

```bash
az vm open-port \
--resource-group DemoRG \
--name DemoVM \
--port 80
```

---

## List Resources

```bash
az resource list --resource-group DemoRG
```

---

## Delete Resource Group

```bash
az group delete --name DemoRG
```

---

## Real-world Example

A DevOps engineer executes a Bash script containing Azure CLI commands to create development infrastructure whenever a new project starts.

---

## Interview Tip

"Azure CLI enables Infrastructure as Code by creating Azure resources through reusable scripts."

---

## Quick Revision

- Login first.
- Create Resource Group.
- Create networking.
- Create storage.
- Create VM.
- Verify deployment.
- Delete unused resources.

---

## Important Interview Questions

1. How do you create a Resource Group using Azure CLI?
2. How do you create a Virtual Machine using Azure CLI?
3. Why is Azure CLI preferred for automation?
4. How do you delete Azure resources?
5. Can Azure CLI be used in CI/CD pipelines?

---

# Azure CLI Use Cases and Multiple References

## Definition

- Azure CLI is widely used by Cloud Engineers, Azure Administrators, DevOps Engineers, and SREs to automate infrastructure and manage Azure resources efficiently.

---

## Common Use Cases

### Infrastructure Deployment

- Create Resource Groups.
- Deploy Virtual Machines.
- Configure Networking.
- Create Storage Accounts.

---

### Infrastructure as Code

- Automate deployments using Bash scripts.
- Reuse deployment scripts across environments.

---

### DevOps Pipelines

- Deploy infrastructure during CI/CD.
- Integrate with Azure DevOps and GitHub Actions.
- Automate application deployments.

---

### Resource Monitoring

- Check VM status.
- List resources.
- Monitor deployments.
- Retrieve resource information.

---

### Security Management

- Assign Azure RBAC roles.
- Manage Managed Identities.
- Configure Key Vault.
- Update NSG rules.

---

### Storage Management

- Upload files.
- Download blobs.
- Create storage containers.
- Generate SAS tokens.

---

### Networking

- Create VNets.
- Configure NSGs.
- Create Public IPs.
- Create Load Balancers.
- Configure VPN Gateways.

---

## Azure CLI vs Azure PowerShell

| Feature | Azure CLI | Azure PowerShell |
|----------|-----------|------------------|
| Command Style | az | Az Module |
| Best For | Cross-platform automation | Windows & PowerShell automation |
| Operating Systems | Windows, Linux, macOS | Windows, Linux, macOS |
| Language | Bash-friendly | PowerShell |
| Popular Among | DevOps Engineers | Windows Administrators |

---

## Azure CLI vs Azure Portal

| Azure Portal | Azure CLI |
|---------------|-----------|
| GUI based | Command line |
| Good for beginners | Good for automation |
| Manual operations | Script-based operations |
| Slower for repetitive work | Fast and repeatable |
| Limited automation | Excellent automation |

---

## Frequently Used Azure CLI Commands

| Command | Purpose |
|----------|----------|
| az login | Login to Azure |
| az logout | Logout |
| az account list | List subscriptions |
| az group create | Create Resource Group |
| az vm create | Create Virtual Machine |
| az vm list | List VMs |
| az storage account create | Create Storage Account |
| az network vnet create | Create VNet |
| az resource list | List resources |
| az group delete | Delete Resource Group |

---

## Real-world Example

A CI/CD pipeline automatically runs Azure CLI commands to create infrastructure, deploy applications, configure networking, and clean up unused resources after testing.

---

## Interview Tip

"In enterprise environments, Azure CLI is heavily used for automation, Infrastructure as Code, CI/CD pipelines, and large-scale Azure administration."

---

## Quick Revision

- Azure CLI starts with `az`.
- Cross-platform tool.
- Supports automation and scripting.
- Used in Azure DevOps and GitHub Actions.
- Can create, update, monitor, and delete Azure resources.
- Faster than manual Portal operations.
- Ideal for Infrastructure as Code.

---

## Important Interview Questions

1. Why is Azure CLI widely used in DevOps?
2. What is the difference between Azure CLI and Azure PowerShell?
3. How does Azure CLI support Infrastructure as Code?
4. How is Azure CLI used in CI/CD pipelines?
5. What are the advantages of Azure CLI over the Azure Portal?
