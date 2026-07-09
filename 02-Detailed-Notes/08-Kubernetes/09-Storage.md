# Storage

## Overview

Kubernetes Storage provides persistent and temporary storage for containers running inside Pods.

By default, containers have **ephemeral storage**, meaning all data is lost when the container is deleted or recreated. Kubernetes solves this problem using **Volumes**, **Persistent Volumes (PV)**, **Persistent Volume Claims (PVC)**, and **Storage Classes**.

Storage resources allow applications such as databases, web servers, and logging systems to retain data across Pod restarts, rescheduling, and upgrades.

> **Interview Tip**
>
> Kubernetes separates **compute (Pods)** from **storage (PV/PVC)**.
>
> Pods consume **PVCs**, not Persistent Volumes directly.

---

## Why It Is Used

Storage is used to:

- Persist application data
- Share data between containers
- Store databases
- Store logs
- Retain user uploads
- Separate storage from Pods
- Support dynamic storage provisioning

---

## Architecture / Working

```mermaid
flowchart LR

Application

↓

Pod

↓

PersistentVolumeClaim

↓

PersistentVolume

↓

StorageClass

↓

Storage Backend

(Storage Account / Azure Disk / AWS EBS / NFS)
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Volume | Temporary Pod storage |
| Persistent Volume (PV) | Cluster storage resource |
| Persistent Volume Claim (PVC) | Request for storage |
| StorageClass | Dynamic storage provisioning |
| Storage Backend | Physical cloud or on-premises storage |

---

## Types (if applicable)

### Storage Types

- EmptyDir
- HostPath
- Persistent Volume
- Network Storage
- Cloud Storage

### Persistent Storage

- Persistent Volume (PV)
- Persistent Volume Claim (PVC)
- StorageClass

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Create StorageClass

↓

PVC Created

↓

Storage Automatically Provisioned

↓

Persistent Volume Created

↓

Pod Uses PVC

↓

Application Stores Data
```

Static Provisioning

```mermaid
flowchart LR

Administrator

↓

Create PV

↓

User Creates PVC

↓

Binding

↓

Pod Uses PVC
```

---

## Configuration / Syntax (if applicable)

Example Pod

```yaml
volumes:
- name: app-storage
```

Example PVC

```yaml
persistentVolumeClaim:
  claimName: app-pvc
```

---

## Important Commands (if applicable)

View Volumes

```bash
kubectl get pv
```

View PVC

```bash
kubectl get pvc
```

View Storage Classes

```bash
kubectl get storageclass
```

Describe PV

```bash
kubectl describe pv
```

Describe PVC

```bash
kubectl describe pvc
```

Delete PVC

```bash
kubectl delete pvc app-pvc
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| pv.yaml | Persistent Volume |
| pvc.yaml | Persistent Volume Claim |
| storageclass.yaml | Storage Class |
| deployment.yaml | Uses PVC |

---

## Real-World Use Cases

- MySQL databases
- PostgreSQL databases
- MongoDB
- Jenkins Home Directory
- Elasticsearch
- User uploads
- Shared application storage
- Log persistence

---

## Advantages

- Persistent storage
- Dynamic provisioning
- Storage abstraction
- Cloud integration
- Portable applications
- Decouples storage from Pods

---

## Limitations

- Storage depends on backend availability
- Incorrect reclaim policies may delete data
- Some volume types are cloud-specific
- Performance depends on storage backend

---

## Common Interview Questions (Concept Only)

- Why is persistent storage required?
- What is the difference between Volume and PV?
- What is PVC?
- Why do Pods use PVC instead of PV?
- What is StorageClass?
- Explain dynamic provisioning.
- What happens when a Pod is deleted?
- What happens if a PVC is deleted?

---

## Common Mistakes

- Using EmptyDir for databases
- Mounting incorrect PVC
- Forgetting StorageClass
- Assuming PV is created automatically without a StorageClass
- Deleting PVC without understanding reclaim policies

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| PVC Pending | No matching PV or StorageClass | Verify storage resources |
| Pod Pending | PVC not bound | Check PVC status |
| Volume Mount Failed | Incorrect mount path | Verify volume configuration |
| Data lost | Ephemeral storage used | Use PV/PVC |
| Provisioning failed | StorageClass issue | Check StorageClass configuration |

Useful Commands

```bash
kubectl get pv

kubectl get pvc

kubectl get storageclass

kubectl describe pvc

kubectl describe pv
```

---

## Summary

Kubernetes Storage enables applications to persist data beyond the lifecycle of individual Pods. Volumes provide temporary storage, while Persistent Volumes, Persistent Volume Claims, and Storage Classes provide scalable, reusable, and dynamically provisioned persistent storage for production workloads.

---

# Volumes

## Overview

A **Volume** is storage attached to a Pod.

Unlike the container filesystem, a Volume survives container restarts within the same Pod.

However, most volumes tied directly to a Pod are deleted when the Pod is deleted.

> **Interview Tip**
>
> A Volume belongs to a **Pod**, not to an individual container.

---

## Why It Is Used

Volumes are used to:

- Share files between containers
- Store temporary data
- Store logs
- Mount configuration files
- Mount Secrets and ConfigMaps

---

## Architecture / Working

```mermaid
flowchart LR

Pod

↓

Volume

↓

Container 1

Container 2
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Volume | Shared storage |
| Mount Path | Directory inside container |
| Pod | Uses the volume |

---

## Types (if applicable)

| Volume Type | Purpose |
|-------------|----------|
| emptyDir | Temporary storage |
| hostPath | Host filesystem |
| configMap | Configuration files |
| secret | Sensitive data |
| persistentVolumeClaim | Persistent storage |

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Create Pod

↓

Attach Volume

↓

Containers Use Volume

↓

Delete Pod

↓

Volume Removed (Except Persistent Storage)
```

---

## Configuration / Syntax (if applicable)

```yaml
volumes:
- name: app-volume
  emptyDir: {}
```

Mount

```yaml
volumeMounts:
- name: app-volume
  mountPath: /data
```

---

## Important Commands (if applicable)

```bash
kubectl describe pod <pod-name>

kubectl exec -it <pod-name> -- df -h
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| pod.yaml | Volume definition |
| deployment.yaml | Volume mounts |

---

## Real-World Use Cases

- Shared logs
- Temporary files
- ConfigMap mounting
- Secret mounting

---

## Advantages

- Easy sharing
- Supports multiple storage types
- Works with ConfigMaps and Secrets

---

## Limitations

- Most Pod volumes are temporary
- Data is lost after Pod deletion unless using persistent storage

---

## Common Interview Questions (Concept Only)

- What is a Volume?
- Difference between Volume and Persistent Volume?
- Can multiple containers share a Volume?

---

## Common Mistakes

- Using EmptyDir for persistent data
- Incorrect mount paths

---

## Troubleshooting

```bash
kubectl describe pod <pod-name>

kubectl exec -it <pod-name> -- ls /data
```

---

## Summary

Volumes provide storage shared by containers within a Pod and are commonly used for temporary data, configuration, and shared files.

---

# Persistent Volumes (PV)

## Overview

A **Persistent Volume (PV)** is a cluster-wide storage resource that exists independently of Pods.

It represents physical storage such as:

- Azure Disk
- Azure Files
- AWS EBS
- NFS
- SAN

PVs are managed by the cluster rather than individual Pods.

> **Interview Tip**
>
> A PV is the **actual storage resource**, while a PVC is the **request** for that storage.

---

## Why It Is Used

Persistent Volumes are used to:

- Retain data after Pod deletion
- Share storage
- Separate storage from compute
- Provide reusable storage

---

## Architecture / Working

```mermaid
flowchart LR

Persistent Volume

↓

Persistent Volume Claim

↓

Pod
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Capacity | Storage size |
| Access Mode | Read/Write policy |
| Storage Backend | Physical storage |
| Reclaim Policy | Data retention behavior |

---

## Types (if applicable)

Access Modes

- ReadWriteOnce (RWO)
- ReadOnlyMany (ROX)
- ReadWriteMany (RWX)

Reclaim Policies

- Retain
- Delete
- Recycle (Deprecated)

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Create PV

↓

PVC Created

↓

Binding

↓

Pod Uses Storage
```

---

## Configuration / Syntax (if applicable)

```yaml
kind: PersistentVolume
```

---

## Important Commands (if applicable)

```bash
kubectl get pv

kubectl describe pv
```

---

## Important Files (if applicable)

pv.yaml

---

## Real-World Use Cases

- Databases
- File storage
- Jenkins
- Elasticsearch

---

## Advantages

- Persistent
- Independent of Pods
- Reusable

---

## Limitations

- Requires backend storage
- Manual management if static provisioning is used

---

## Common Interview Questions (Concept Only)

- What is a Persistent Volume?
- Explain reclaim policies.
- Explain access modes.

---

## Common Mistakes

- Assuming Pods directly use PVs
- Incorrect access mode selection

---

## Troubleshooting

```bash
kubectl describe pv
```

---

## Summary

Persistent Volumes represent the actual storage resources available in a Kubernetes cluster and provide durable storage independent of Pod lifecycles.

---

# Persistent Volume Claims (PVC)

## Overview

A **Persistent Volume Claim (PVC)** is a request for storage made by a user or application.

Pods request storage through PVCs instead of directly using Persistent Volumes.

The Kubernetes control plane automatically binds a matching PV to the PVC.

> **Interview Tip**
>
> **Pods → PVC → PV**
>
> This abstraction allows storage to be managed independently of applications.

---

## Why It Is Used

PVCs are used to:

- Request storage
- Abstract physical storage
- Enable dynamic provisioning
- Simplify application deployment

---

## Architecture / Working

```mermaid
flowchart LR

Pod

↓

PVC

↓

PV

↓

Storage
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Storage Request | Requested capacity |
| Access Mode | Read/Write policy |
| StorageClass | Dynamic provisioning |

---

## Types (if applicable)

- Static Binding
- Dynamic Binding

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Create PVC

↓

Find Matching PV

↓

Bind

↓

Pod Uses Storage
```

---

## Configuration / Syntax (if applicable)

```yaml
kind: PersistentVolumeClaim
```

---

## Important Commands (if applicable)

```bash
kubectl get pvc

kubectl describe pvc
```

---

## Important Files (if applicable)

pvc.yaml

---

## Real-World Use Cases

- Database storage
- Application uploads
- Shared application data

---

## Advantages

- Storage abstraction
- Easy to use
- Dynamic provisioning

---

## Limitations

- Depends on available storage
- Incorrect StorageClass prevents binding

---

## Common Interview Questions (Concept Only)

- What is PVC?
- Why do Pods use PVC?
- Difference between PV and PVC?

---

## Common Mistakes

- Using incorrect storage size
- Wrong access mode

---

## Troubleshooting

```bash
kubectl describe pvc
```

---

## Summary

Persistent Volume Claims allow applications to request storage without needing to know implementation details about the underlying storage infrastructure.

---

# Storage Classes

## Overview

A **StorageClass** defines how Kubernetes dynamically provisions storage.

Instead of administrators creating Persistent Volumes manually, StorageClasses automatically provision storage whenever a PVC requests it.

This is the standard approach in modern Kubernetes clusters.

> **Interview Tip**
>
> Most cloud-managed Kubernetes services (AKS, EKS, GKE) rely on **dynamic provisioning using StorageClasses**.

---

## Why It Is Used

StorageClasses are used to:

- Enable dynamic provisioning
- Automate storage creation
- Support multiple storage types
- Define storage performance characteristics

---

## Architecture / Working

```mermaid
flowchart LR

StorageClass

↓

PVC

↓

Dynamic PV

↓

Pod
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Provisioner | Creates storage |
| Parameters | Storage settings |
| Reclaim Policy | Cleanup behavior |
| Volume Binding Mode | Binding timing |

---

## Types (if applicable)

Examples

- Azure Disk
- Azure Files
- AWS EBS
- NFS
- Local Storage

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Create StorageClass

↓

Create PVC

↓

Provision Storage

↓

Create PV

↓

Bind PVC

↓

Pod Uses Storage
```

---

## Configuration / Syntax (if applicable)

```yaml
kind: StorageClass
```

---

## Important Commands (if applicable)

List Storage Classes

```bash
kubectl get storageclass
```

Describe Storage Class

```bash
kubectl describe storageclass
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| storageclass.yaml | StorageClass definition |

---

## Real-World Use Cases

- Azure AKS
- AWS EKS
- Google GKE
- Production databases
- Enterprise applications

---

## Advantages

- Automatic provisioning
- Simplifies storage management
- Cloud-native integration
- Supports multiple storage backends

---

## Limitations

- Requires supported storage provisioner
- Misconfigured StorageClasses can prevent PVC binding

---

## Common Interview Questions (Concept Only)

- What is a StorageClass?
- What is dynamic provisioning?
- Difference between static and dynamic provisioning?
- How does a StorageClass work with a PVC?
- Can multiple StorageClasses exist in one cluster?

---

## Common Mistakes

- Forgetting to specify the correct StorageClass
- Assuming every cluster has a default StorageClass
- Using an unsupported provisioner

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| PVC Pending | Missing or incorrect StorageClass | Verify `storageClassName` |
| No PV created | Provisioner unavailable | Check StorageClass and CSI driver |
| Provisioning failed | Invalid parameters | Review StorageClass configuration |
| Wrong storage type | Incorrect StorageClass selected | Use the appropriate StorageClass |

Useful Commands

```bash
kubectl get storageclass

kubectl describe storageclass

kubectl get pvc

kubectl describe pvc
```

---

## Summary

StorageClasses automate the creation of Persistent Volumes through dynamic provisioning. They define how storage is allocated and are the preferred method for managing persistent storage in modern Kubernetes environments, especially on cloud platforms like AKS, EKS, and GKE.
