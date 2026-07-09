# Vault, Tags & Facts Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Ansible Vault, and why is it used?

**Answer**

Ansible Vault is a built-in feature that encrypts sensitive data such as passwords, API keys, SSH private keys, certificates, and secret variables.

**Explanation**

Storing secrets in plain text is a major security risk. Ansible Vault encrypts sensitive information using AES-256 encryption, ensuring that only authorized users with the Vault password can access the data.

**Used in Production**

- Database passwords
- Cloud credentials
- SSH private keys
- API tokens
- SSL certificates

**Common Mistake**

Storing passwords directly in playbooks or inventory files instead of using Vault.

---

### Question 2

**Question**

How do you create an encrypted file using Ansible Vault?

**Answer**

Use the command:

```bash
ansible-vault create secrets.yml
```

**Explanation**

This command prompts for a Vault password and opens an editor. The contents are encrypted before being saved.

**Used in Production**

Creating encrypted variable files containing application credentials or infrastructure secrets.

---

### Question 3

**Question**

How do you encrypt an existing file with Ansible Vault?

**Answer**

Use:

```bash
ansible-vault encrypt secrets.yml
```

**Explanation**

The existing file is encrypted without changing its contents.

**Used in Production**

Encrypting existing configuration or variable files before committing them to version control.

---

### Question 4

**Question**

How do you decrypt an encrypted Vault file?

**Answer**

Use:

```bash
ansible-vault decrypt secrets.yml
```

**Explanation**

After entering the Vault password, the file becomes plain text.

**Used in Production**

Editing encrypted files when permanent decryption is required.

**Common Mistake**

Decrypting files and accidentally committing them to Git.

---

### Question 5

**Question**

How do you use encrypted variables in a playbook?

**Answer**

Include the encrypted file using `vars_files`.

Example:

```yaml
vars_files:
  - secrets.yml
```

**Explanation**

During execution, Ansible decrypts the file using the Vault password and loads the variables automatically.

**Used in Production**

Database credentials, cloud secrets, and application passwords.

---

### Question 6

**Question**

What is the purpose of the Vault password?

**Answer**

The Vault password is used to encrypt and decrypt Vault-protected files during playbook execution.

**Explanation**

Without the correct password (or password file), encrypted content cannot be accessed.

**Used in Production**

Protecting confidential infrastructure and application credentials.

---

### Question 7

**Question**

What are Tags in Ansible?

**Answer**

Tags allow you to execute or skip specific tasks in a playbook instead of running every task.

Example:

```yaml
tasks:
  - name: Install Nginx
    apt:
      name: nginx
      state: present
    tags:
      - install
```

**Explanation**

Tags improve execution speed and flexibility by allowing selective task execution.

**Used in Production**

Running only deployment, configuration, backup, or restart tasks as needed.

---

### Question 8

**Question**

How do you run only tagged tasks?

**Answer**

Use:

```bash
ansible-playbook site.yml --tags install
```

**Explanation**

Only tasks tagged with `install` are executed.

**Used in Production**

Deploying application updates without rerunning server provisioning tasks.

---

### Question 9

**Question**

How do you skip specific tagged tasks?

**Answer**

Use:

```bash
ansible-playbook site.yml --skip-tags backup
```

**Explanation**

All tasks except those tagged with `backup` are executed.

**Used in Production**

Skipping long-running backup or maintenance tasks during urgent deployments.

---

### Question 10

**Question**

What are Ansible Facts?

**Answer**

Facts are automatically collected system information about managed hosts.

Examples include:

- Operating system
- IP address
- CPU
- Memory
- Hostname
- Disk information

**Explanation**

Facts allow playbooks to make decisions based on the target system.

**Used in Production**

OS-specific package installation, configuration management, and conditional execution.

---

### Question 11

**Question**

What is the purpose of `ansible_facts`?

**Answer**

`ansible_facts` is a dictionary that stores all gathered information about a managed host.

Example:

```yaml
{{ ansible_facts.hostname }}
```

**Explanation**

Playbooks can reference these facts to customize automation dynamically.

**Used in Production**

Generating configuration files, selecting packages, and environment-specific deployments.

---

### Question 12

**Question**

What is the `setup` module?

**Answer**

The `setup` module gathers system facts from managed hosts.

Example:

```bash
ansible all -m setup
```

**Explanation**

The module collects detailed information about the target systems, which becomes available as Ansible Facts.

**Used in Production**

Inventory validation, troubleshooting, dynamic configuration, and conditional task execution.

**Common Mistake**

Disabling fact gathering without understanding that many playbooks rely on `ansible_facts`.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Your playbook contains database passwords in plain text. How would you secure them?

**Answer**

Move the passwords to an encrypted Vault file and load them using `vars_files`.

**Explanation**

Vault encrypts sensitive information, preventing accidental exposure in source code repositories.

---

### Scenario 2

**Question**

A deployment playbook has 200 tasks, but you only need to restart services. How would you avoid running the entire playbook?

**Answer**

Assign tags to restart tasks and execute the playbook using:

```bash
ansible-playbook site.yml --tags restart
```

**Explanation**

Tags enable selective execution, reducing deployment time and minimizing unnecessary changes.

---

### Scenario 3

**Question**

You need to skip backup tasks during an emergency production deployment. What would you do?

**Answer**

Run the playbook using:

```bash
ansible-playbook site.yml --skip-tags backup
```

**Explanation**

Skipping nonessential tasks speeds up deployments while preserving the playbook structure.

---

### Scenario 4

**Question**

Your playbook should install Apache on Debian systems and HTTPD on Red Hat systems. How would you determine the operating system?

**Answer**

Use `ansible_facts` such as:

```yaml
ansible_os_family
```

or

```yaml
ansible_distribution
```

**Explanation**

Facts allow playbooks to adapt automatically to different operating systems.

---

### Scenario 5

**Question**

A teammate accidentally committed an unencrypted password file to Git. What would you recommend?

**Answer**

Remove the exposed credentials, rotate the affected passwords, encrypt the file with Ansible Vault, and recommit the encrypted version.

**Explanation**

Secrets committed in plain text should always be treated as compromised.

---

### Scenario 6

**Question**

Your playbook fails because `ansible_distribution` is undefined. What is the most likely cause?

**Answer**

Fact gathering is disabled, or the `setup` module has not been executed.

**Explanation**

Ansible Facts are unavailable unless they are gathered during playbook execution.

---

### Scenario 7

**Question**

You need to generate an Nginx configuration file containing the server hostname automatically. Which feature would you use?

**Answer**

Use `ansible_facts.hostname` inside a Jinja2 template.

**Explanation**

Facts provide dynamic host information that can be inserted into configuration files during deployment.

---

### Scenario 8

**Question**

Your security team requires that cloud API keys never appear in playbooks or inventory files. How would you implement this?

**Answer**

Store the API keys in an encrypted Vault file and reference them as variables during playbook execution.

**Explanation**

This ensures sensitive information remains encrypted both at rest and in version control.

---

### Scenario 9

**Question**

You only want to execute configuration tasks during a maintenance window while skipping installation tasks. How would you achieve this?

**Answer**

Assign separate tags such as `configure` and `install`, then run:

```bash
ansible-playbook site.yml --tags configure
```

**Explanation**

Tags allow different stages of automation to be executed independently.

---

### Scenario 10

**Question**

Before deploying an application, you want to verify the hostname, operating system, memory, and IP address of all managed servers. Which Ansible feature would you use?

**Answer**

Gather Ansible Facts using the `setup` module or the default fact-gathering process.

**Explanation**

Facts provide detailed system information that helps validate infrastructure before deployment and supports dynamic automation.
