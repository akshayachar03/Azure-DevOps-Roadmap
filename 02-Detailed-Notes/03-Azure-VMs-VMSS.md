# Azure Virtual Machines (Azure VM)

## Definition

- Azure Virtual Machine (VM) is an Infrastructure as a Service (IaaS) offering.
- It allows you to create and run Windows or Linux virtual servers in Azure.
- You have full control over the operating system, applications, storage, and networking.

---

## Why is it used?

- Host web applications.
- Run enterprise applications.
- Lift and shift on-premises workloads to Azure.
- Run development and testing environments.
- Host databases and application servers.
- Support custom software that requires OS-level control.

---

## Key Features

- Supports Windows and Linux operating systems.
- Multiple VM sizes based on CPU, RAM, and storage.
- Connect using RDP (Windows) or SSH (Linux).
- Supports Managed Disks.
- Can be attached to Virtual Networks (VNet).
- Supports Availability Sets and Availability Zones.
- Can be backed up using Azure Backup.
- Supports auto-shutdown and monitoring.

---

## Advantages

- Full control over the operating system.
- Easy to scale vertically by changing VM size.
- Supports custom applications.
- Highly available using Availability Zones.
- Pay only for the resources you use.
- Easy integration with other Azure services.

---

## Disadvantages

- Requires OS maintenance and patching.
- User is responsible for security updates.
- Scaling multiple VMs manually can be difficult.
- Higher management overhead compared to PaaS.

---

## Components

### Virtual Machine

- The compute resource.

### VM Size

- Determines CPU, RAM, and storage performance.

### Operating System

- Windows Server or Linux distributions.

### Managed Disk

- Stores OS and application data.

### Network Interface (NIC)

- Connects VM to the virtual network.

### Virtual Network (VNet)

- Private network for Azure resources.

### Public IP (Optional)

- Allows internet access.

### Network Security Group (NSG)

- Controls inbound and outbound traffic.

---

## Workflow

```text
Create Resource Group
        ↓
Create Virtual Network
        ↓
Choose VM Image
        ↓
Select VM Size
        ↓
Configure Storage & Networking
        ↓
Deploy VM
        ↓
Connect using RDP/SSH
```

---

## Real-world Example

A company migrates its on-premises payroll application to Azure by creating a Windows VM and installing the existing application without changing its architecture.

---

## Interview Tip

"Azure VM is an IaaS service where Azure manages the physical infrastructure while I manage the operating system, applications, networking, and security."

---

## Quick Revision

- Azure VM is an IaaS service.
- Supports Windows and Linux.
- Connect using RDP or SSH.
- Uses Managed Disks.
- Can be placed in VNets.
- Supports Availability Sets and Zones.
- User manages the OS.
- Suitable for custom applications.

---

## Important Interview Questions

1. What is Azure Virtual Machine?
2. When should you choose Azure VM instead of App Service?
3. What is the difference between Availability Set and Availability Zone?
4. How do you connect to a Windows and Linux VM?
5. What responsibilities does Azure have and what responsibilities does the customer have for Azure VMs?

---

# Azure Virtual Machine Scale Sets (VMSS)

## Definition

- Azure Virtual Machine Scale Sets (VMSS) allow you to deploy and manage multiple identical virtual machines.
- VMSS automatically increases or decreases the number of VMs based on demand.
- It helps build highly available and scalable applications.

---

## Why is it used?

- Automatically handle increasing user traffic.
- Reduce infrastructure management.
- Improve application availability.
- Support load-balanced applications.
- Optimize cost using auto-scaling.

---

## Key Features

- Automatic scaling based on CPU, memory, or custom metrics.
- Supports thousands of VM instances.
- Integrates with Azure Load Balancer.
- Supports Availability Zones.
- Uniform VM configuration.
- Automatic OS image upgrades.
- Supports rolling upgrades.
- Health monitoring of VM instances.

---

## Advantages

- Automatic scaling.
- High availability.
- Reduced manual management.
- Cost optimization.
- Easy deployment of identical VMs.
- Supports rolling updates with minimal downtime.

---

## Disadvantages

- All VMs should have similar configuration.
- Less suitable for workloads requiring unique server configurations.
- Requires proper scaling policies.

---

## Components

### Scale Set

- Group of identical virtual machines.

### VM Instances

- Individual virtual machines inside the scale set.

### Autoscale Rules

- Define when to add or remove VM instances.

### Load Balancer

- Distributes traffic among VM instances.

### Health Probe

- Detects unhealthy VM instances.

### Availability Zones

- Improve fault tolerance.

---

## Workflow

```text
Create VM Scale Set
          ↓
Deploy Multiple VM Instances
          ↓
Attach Load Balancer
          ↓
Configure Autoscale Rules
          ↓
Traffic Increases
          ↓
New VM Instances Created Automatically
          ↓
Traffic Decreases
          ↓
Extra VM Instances Removed
```

---

## Real-world Example

An e-commerce website normally runs on 2 virtual machines. During a festive sale, CPU usage exceeds 70%, so VM Scale Sets automatically increase the number of VMs to 10. After the sale, unused VMs are removed automatically to reduce cost.

---

## Interview Tip

"VM Scale Sets are used when an application needs automatic scaling and high availability. Instead of manually creating VMs, Azure automatically adds or removes VM instances based on demand."

---

## Quick Revision

- VMSS manages multiple identical VMs.
- Supports automatic scaling.
- Integrates with Azure Load Balancer.
- Uses autoscale rules.
- Supports rolling upgrades.
- Improves high availability.
- Reduces operational effort.
- Helps optimize cost.

---

## Important Interview Questions

1. What is Azure Virtual Machine Scale Set?
2. How does VM Scale Set perform auto-scaling?
3. Why is Azure Load Balancer used with VM Scale Sets?
4. What are rolling upgrades in VM Scale Sets?
5. When would you choose VM Scale Sets instead of a single Azure VM?

---

# Azure VM vs Azure VM Scale Sets

| Feature | Azure VM | Azure VM Scale Sets |
|---------|-----------|---------------------|
| Number of VMs | Single VM | Multiple identical VMs |
| Scaling | Manual | Automatic |
| High Availability | Possible with Availability Set/Zone | Built-in with multiple instances |
| Load Balancing | Configure separately | Integrated |
| Management | Individual VM | Centralized |
| Best For | Small applications, databases, testing | Web applications, APIs, large-scale workloads |
| Cost Optimization | Manual | Automatic through autoscaling |
| Maintenance | Individual | Centralized |
