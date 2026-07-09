# Ansible Galaxy

## Overview

Ansible Galaxy is the official repository for sharing and downloading Ansible Roles and Collections.

It allows DevOps engineers to reuse automation created by the Ansible community instead of writing everything from scratch.

Ansible Galaxy provides:

- Reusable Roles
- Collections
- Documentation
- Version management
- Community-contributed automation

> **Interview Tip**
>
> Think of **Ansible Galaxy** as the **GitHub of Ansible Roles and Collections**.

---

## Why It Is Used

Ansible Galaxy helps to:

- Reuse existing automation
- Reduce development time
- Standardize deployments
- Share automation across teams
- Simplify dependency management

---

## Architecture / Working

```mermaid
flowchart LR
    DevOpsEngineer --> AnsibleGalaxy
    AnsibleGalaxy --> DownloadRole
    DownloadRole --> LocalRolesDirectory
    LocalRolesDirectory --> Playbook
    Playbook --> ManagedNodes
```

---

## Key Components

| Component | Purpose |
|-----------|---------|
| Galaxy Server | Repository of Roles and Collections |
| Roles | Reusable automation modules |
| Collections | Bundles of Roles, Modules, and Plugins |
| ansible-galaxy | CLI tool for interacting with Galaxy |

---

## Types (if applicable)

### Roles

Reusable automation for common tasks.

Examples:

- Nginx
- Apache
- Docker
- MySQL

---

### Collections

A package containing:

- Roles
- Modules
- Plugins
- Documentation

Collections are the preferred packaging method in modern Ansible.

---

## Lifecycle / Workflow

```mermaid
flowchart LR
    SearchGalaxy --> InstallRole
    InstallRole --> AddToPlaybook
    AddToPlaybook --> ExecutePlaybook
```

---

## Configuration / Syntax (if applicable)

Search Galaxy

```bash
ansible-galaxy search nginx
```

Install Role

```bash
ansible-galaxy role install geerlingguy.nginx
```

Install Collection

```bash
ansible-galaxy collection install community.general
```

List Installed Roles

```bash
ansible-galaxy role list
```

List Installed Collections

```bash
ansible-galaxy collection list
```

---

## Important Commands (if applicable)

Initialize a Role

```bash
ansible-galaxy init myrole
```

Search Roles

```bash
ansible-galaxy search docker
```

Install Role

```bash
ansible-galaxy role install geerlingguy.mysql
```

Install Collection

```bash
ansible-galaxy collection install ansible.posix
```

Remove Role

```bash
ansible-galaxy role remove geerlingguy.mysql
```

---

## Important Files (if applicable)

| File | Purpose |
|------|---------|
| requirements.yml | Defines Galaxy Roles or Collections to install |
| roles/ | Stores installed Roles |
| collections/ | Stores installed Collections |
| ansible.cfg | Galaxy installation paths |

---

## Real-World Use Cases

- Install Docker using community Roles
- Configure Nginx
- Deploy Kubernetes components
- Configure MySQL
- Standardize server configurations
- Share automation across development teams

---

## Advantages

- Saves development time
- Community-tested automation
- Easy installation
- Version management
- Reusable components

---

## Limitations

- Community Roles may vary in quality
- Third-party Roles require validation before production use
- Version incompatibilities may occur
- Some Roles may become unmaintained

---

## Common Interview Questions (Concept Only)

- What is Ansible Galaxy?
- What is the difference between a Role and a Collection?
- Why is Ansible Galaxy used?
- Which command searches Galaxy?
- Which command initializes a new Role?

---

## Common Mistakes

- Installing untrusted community Roles without review
- Not specifying Role versions
- Mixing incompatible Role versions
- Forgetting required dependencies

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Role not found | Incorrect name | Verify Galaxy Role name |
| Version conflict | Incompatible versions | Install a compatible version |
| Permission denied | Insufficient privileges | Check installation directory permissions |
| Role unavailable | Network or repository issue | Verify internet connectivity and Role name |

Useful Commands

```bash
ansible-galaxy role list

ansible-galaxy collection list

ansible-galaxy search nginx
```

---

## Summary

Ansible Galaxy is the official repository for sharing and downloading reusable Roles and Collections. It accelerates automation development by allowing engineers to reuse well-tested community and organization-maintained automation components.

---

# Install Roles

## Overview

Roles can be installed directly from Ansible Galaxy using the `ansible-galaxy` command.

Installed Roles are stored locally and can be reused in multiple Playbooks.

> **Interview Tip**
>
> Installing Roles from Galaxy is much faster than manually creating common automation such as Docker, Nginx, or MySQL installation tasks.

---

## Why It Is Used

Installing Roles helps to:

- Reuse community automation
- Reduce development effort
- Improve consistency
- Accelerate infrastructure deployment

---

## Architecture / Working

```mermaid
flowchart LR
    GalaxyRepository --> DownloadRole
    DownloadRole --> LocalRolesDirectory
    LocalRolesDirectory --> Playbook
```

---

## Key Components

| Component | Purpose |
|-----------|---------|
| ansible-galaxy | CLI installation tool |
| Role Repository | Source of Roles |
| Local Roles Directory | Stores downloaded Roles |

---

## Types (if applicable)

Installation Methods

- Install a single Role
- Install multiple Roles using `requirements.yml`

---

## Lifecycle / Workflow

```mermaid
flowchart LR
    SearchRole --> InstallRole
    InstallRole --> StoreLocally
    StoreLocally --> UseRole
```

---

## Configuration / Syntax (if applicable)

Install a Role

```bash
ansible-galaxy role install geerlingguy.nginx
```

Install a Specific Version

```bash
ansible-galaxy role install geerlingguy.nginx,3.1.0
```

Install Multiple Roles

Create `requirements.yml`

```yaml
roles:
  - name: geerlingguy.nginx
  - name: geerlingguy.mysql
```

Install All Roles

```bash
ansible-galaxy role install -r requirements.yml
```

---

## Important Commands (if applicable)

Install Role

```bash
ansible-galaxy role install geerlingguy.nginx
```

List Roles

```bash
ansible-galaxy role list
```

Remove Role

```bash
ansible-galaxy role remove geerlingguy.nginx
```

---

## Important Files (if applicable)

| File | Purpose |
|------|---------|
| requirements.yml | Install multiple Roles |
| roles/ | Installed Roles |

---

## Real-World Use Cases

- Install Docker Role
- Install Kubernetes Role
- Configure Nginx
- Configure Apache
- Install MySQL

---

## Advantages

- Quick installation
- Version control
- Easy maintenance
- Reusable automation

---

## Limitations

- Depends on Role quality
- External dependencies may exist
- Internet access required for initial download

---

## Common Interview Questions (Concept Only)

- How do you install a Role?
- What is `requirements.yml`?
- How do you install multiple Roles at once?
- Where are installed Roles stored?

---

## Common Mistakes

- Incorrect Role name
- Ignoring Role documentation
- Forgetting dependencies
- Installing incompatible versions

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Role installation failed | Incorrect name | Verify Galaxy Role name |
| Version conflict | Wrong version | Specify compatible version |
| Download failed | Network issue | Check internet connectivity |

Useful Commands

```bash
ansible-galaxy role install -r requirements.yml

ansible-galaxy role list
```

---

## Summary

Roles are installed using the `ansible-galaxy role install` command. Multiple Roles can be managed efficiently using a `requirements.yml` file, making deployments consistent and repeatable.

---

# Use Galaxy Roles

## Overview

Once a Role is installed from Ansible Galaxy, it can be used in any Playbook through the `roles` keyword.

Ansible automatically loads the Role's:

- Tasks
- Variables
- Templates
- Files
- Handlers

during Playbook execution.

---

## Why It Is Used

Using Galaxy Roles enables:

- Reuse of community automation
- Modular Playbooks
- Standardized deployments
- Faster infrastructure provisioning

---

## Architecture / Working

```mermaid
flowchart LR
    InstalledRole --> Playbook
    Playbook --> ExecuteTasks
    ExecuteTasks --> ManagedNodes
```

---

## Key Components

| Component | Purpose |
|-----------|---------|
| Installed Role | Downloaded automation |
| Playbook | Uses the Role |
| Managed Nodes | Target systems |

---

## Types (if applicable)

Role Usage

- Single Role
- Multiple Roles

---

## Lifecycle / Workflow

```mermaid
flowchart LR
    InstallRole --> AddRoleToPlaybook
    AddRoleToPlaybook --> ExecutePlaybook
```

---

## Configuration / Syntax (if applicable)

Use a Single Role

```yaml
- hosts: web

  roles:
    - geerlingguy.nginx
```

Use Multiple Roles

```yaml
- hosts: web

  roles:
    - geerlingguy.mysql
    - geerlingguy.nginx
```

Pass Variables to a Role

```yaml
- hosts: web

  roles:
    - role: geerlingguy.nginx
      vars:
        nginx_listen_port: 8080
```

---

## Important Commands (if applicable)

Execute Playbook

```bash
ansible-playbook site.yml
```

List Installed Roles

```bash
ansible-galaxy role list
```

---

## Important Files (if applicable)

| File | Purpose |
|------|---------|
| playbook.yml | Includes Galaxy Roles |
| roles/ | Installed Roles |
| requirements.yml | Role dependency list |

---

## Real-World Use Cases

- Deploy Nginx
- Configure Docker
- Install MySQL
- Deploy Kubernetes worker nodes
- Configure monitoring agents
- Provision application servers

---

## Advantages

- Reduces development time
- Standardized deployments
- Easy integration
- Modular Playbooks
- Reusable automation

---

## Limitations

- Community Roles may not match organizational standards
- Customization may require variable overrides
- Updates may introduce breaking changes

---

## Common Interview Questions (Concept Only)

- How do you use an installed Galaxy Role?
- Can multiple Galaxy Roles be used in one Playbook?
- How are variables passed to a Galaxy Role?
- Where does Ansible search for installed Roles?

---

## Common Mistakes

- Incorrect Role name in the Playbook
- Not installing the Role before use
- Ignoring required Role variables
- Forgetting Role dependencies

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Role not found | Role not installed | Install using `ansible-galaxy role install` |
| Variable error | Required variable missing | Define required variables |
| Task failure | Unsupported platform | Verify Role documentation and supported operating systems |

Useful Commands

```bash
ansible-galaxy role list

ansible-playbook site.yml

ansible-playbook site.yml --check
```

---

## Summary

Galaxy Roles allow engineers to reuse community-maintained automation with minimal effort. After installation, they are included in Playbooks using the `roles` keyword, enabling faster, standardized, and more maintainable infrastructure automation.
