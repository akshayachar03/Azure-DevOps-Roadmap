# Essential Linux Interview Commands Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

Which Linux commands are considered essential for DevOps, Cloud, SRE, and Infrastructure Engineer interviews?

**Answer**

The most frequently used Linux commands include:

| Category | Commands |
|----------|----------|
| File Permissions | `chmod`, `chown` |
| File Search | `find`, `grep` |
| Process Management | `ps`, `top`, `kill` |
| File Archiving | `tar` |
| Networking | `curl`, `wget`, `ssh`, `scp`, `ip` |
| Service Management | `systemctl`, `journalctl` |
| Storage | `df`, `du`, `lsblk` |
| Scheduling | `cron` |
| Scripting | `bash` |

**Explanation**

These commands cover daily Linux administration tasks and form the foundation of DevOps and Cloud operations.

**Used in Production**

Engineers use these commands daily for troubleshooting, deployments, monitoring, automation, and server management.

---

### Question 2

**Question**

What is the difference between `chmod` and `chown`?

**Answer**

`chmod`

Changes file permissions.

Example:

```bash
chmod 755 script.sh
```

`chown`

Changes file ownership.

Example:

```bash
sudo chown ubuntu:developers script.sh
```

**Explanation**

Permissions determine **what** users can do, while ownership determines **who** controls the file.

**Used in Production**

Frequently used during deployments and application setup.

---

### Question 3

**Question**

When would you use `find` instead of `grep`?

**Answer**

Use `find` to locate files.

Example:

```bash
find /var/log -name "*.log"
```

Use `grep` to search inside files.

Example:

```bash
grep ERROR application.log
```

**Explanation**

`find` searches the filesystem, while `grep` searches file contents.

**Used in Production**

Administrators often combine both commands to locate and inspect files.

---

### Question 4

**Question**

What is the difference between `ps`, `top`, and `kill`?

**Answer**

| Command | Purpose |
|----------|---------|
| `ps` | Displays running processes |
| `top` | Monitors processes in real time |
| `kill` | Terminates a process |

Examples:

```bash
ps -ef
```

```bash
top
```

```bash
kill PID
```

**Explanation**

These commands work together for process management and troubleshooting.

**Used in Production**

Used to identify resource-intensive or unresponsive applications.

---

### Question 5

**Question**

Why is the `tar` command important?

**Answer**

`tar` creates or extracts archive files.

Create archive:

```bash
tar -cvf backup.tar folder/
```

Extract archive:

```bash
tar -xvf backup.tar
```

**Explanation**

`tar` simplifies backup, transfer, and deployment of files.

**Used in Production**

Commonly used for backups, application packaging, and log archiving.

---

### Question 6

**Question**

What is the difference between `curl` and `wget`?

**Answer**

| `curl` | `wget` |
|---------|--------|
| Tests APIs | Downloads files |
| Supports many protocols | Primarily HTTP/HTTPS/FTP |
| Frequently used in automation | Frequently used for downloads |

Examples:

```bash
curl https://example.com
```

```bash
wget https://example.com/file.zip
```

**Explanation**

`curl` is more flexible for API interaction, while `wget` excels at downloading files.

**Used in Production**

Both are widely used in automation and deployment scripts.

---

### Question 7

**Question**

What are `ssh` and `scp` used for?

**Answer**

SSH:

```bash
ssh user@server
```

Securely connects to a remote Linux server.

SCP:

```bash
scp file.txt user@server:/tmp/
```

Securely copies files between systems.

**Explanation**

Both use the SSH protocol to provide encrypted communication.

**Used in Production**

Remote administration and file transfers rely heavily on SSH and SCP.

---

### Question 8

**Question**

How are `systemctl` and `journalctl` related?

**Answer**

`systemctl`

Manages services.

Example:

```bash
systemctl restart nginx
```

`journalctl`

Displays service logs.

Example:

```bash
journalctl -u nginx
```

**Explanation**

`systemctl` controls services, while `journalctl` helps troubleshoot them.

**Used in Production**

Frequently used together during service failures.

---

### Question 9

**Question**

What is the difference between `df`, `du`, and `lsblk`?

**Answer**

| Command | Purpose |
|----------|---------|
| `df` | Shows filesystem usage |
| `du` | Shows directory size |
| `lsblk` | Displays storage devices |

Examples:

```bash
df -h
```

```bash
du -sh /var/log
```

```bash
lsblk
```

**Explanation**

Each command provides a different view of storage usage.

**Used in Production**

Administrators use these commands to troubleshoot disk space issues.

---

### Question 10

**Question**

What are the purposes of the `ip`, `cron`, and `bash` commands?

**Answer**

`ip`

Displays or configures networking.

```bash
ip addr
```

`cron`

Schedules recurring tasks.

```bash
crontab -e
```

`bash`

Runs Bash scripts.

```bash
bash script.sh
```

**Explanation**

These commands support networking, automation, and scripting.

**Used in Production**

Essential for Linux administration and DevOps automation.

---

### Question 11

**Question**

What are some best practices when using Linux commands in production?

**Answer**

Best practices include:

- Verify commands before executing them.
- Test destructive commands in non-production environments.
- Use `grep` to filter logs efficiently.
- Monitor processes before terminating them.
- Verify permissions before changing ownership.
- Use SSH keys instead of passwords.
- Review logs before restarting services.
- Automate repetitive tasks using Bash and cron.
- Document administrative procedures.

**Explanation**

Careful command usage reduces operational risk and improves reliability.

**Used in Production**

Following best practices minimizes downtime and human error.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A deployment fails because the application cannot execute a startup script. Which Linux command would you use first?

**Answer**

Check and update file permissions:

```bash
chmod +x startup.sh
```

**Explanation**

Missing execute permission is a common cause of deployment failures.

---

### Scenario 2

**Question**

An application cannot access a configuration file due to ownership issues. Which command would you use?

**Answer**

Use:

```bash
chown application:application config.yml
```

**Explanation**

Correct ownership ensures the application has the required access.

---

### Scenario 3

**Question**

A production log contains millions of lines. You need to locate all entries containing "ERROR". Which command would you use?

**Answer**

Run:

```bash
grep ERROR application.log
```

**Explanation**

`grep` quickly filters relevant log entries.

---

### Scenario 4

**Question**

A server becomes slow because one process is consuming excessive CPU. Which commands would you use?

**Answer**

Identify the process:

```bash
top
```

or

```bash
ps -ef
```

Terminate it if necessary:

```bash
kill PID
```

**Explanation**

Monitoring precedes termination to avoid stopping the wrong process.

---

### Scenario 5

**Question**

Your manager requests a compressed backup of the application directory before deployment. Which command would you use?

**Answer**

Run:

```bash
tar -czvf backup.tar.gz application/
```

**Explanation**

`tar` packages and compresses files for backup.

---

### Scenario 6

**Question**

A deployment script needs to download an installation package from the internet. Which command would you choose?

**Answer**

Use:

```bash
wget URL
```

or

```bash
curl -O URL
```

**Explanation**

Both commands download remote resources, with `curl` offering greater flexibility for HTTP interactions.

---

### Scenario 7

**Question**

You need to copy a deployment package securely to a remote Linux server. Which command would you use?

**Answer**

Run:

```bash
scp package.tar.gz user@server:/opt/
```

**Explanation**

`scp` securely transfers files using SSH.

---

### Scenario 8

**Question**

A service fails immediately after deployment. Which commands would you use to investigate?

**Answer**

Check service status:

```bash
systemctl status service-name
```

Review logs:

```bash
journalctl -u service-name
```

**Explanation**

Service status and logs provide the most relevant troubleshooting information.

---

### Scenario 9

**Question**

A server reports that the disk is full. Which Linux commands would you use to identify the problem?

**Answer**

Check filesystem usage:

```bash
df -h
```

Identify large directories:

```bash
du -sh /*
```

View storage devices:

```bash
lsblk
```

**Explanation**

These commands provide complementary information for diagnosing storage issues.

---

### Scenario 10

**Question**

A nightly backup script is not running automatically. Which Linux feature would you investigate?

**Answer**

Check scheduled jobs:

```bash
crontab -l
```

Edit if necessary:

```bash
crontab -e
```

Review cron logs to confirm execution.

**Explanation**

Cron is responsible for scheduling recurring tasks.

---

### Scenario 11

**Question**

A production deployment fails after new code is released. The application cannot start, users report downtime, disk space is nearly exhausted, and administrators need to verify network connectivity while collecting logs for troubleshooting. Which essential Linux commands would you use and why?

**Answer**

A structured investigation would include:

- Check service status:

```bash
systemctl status application
```

- Review service logs:

```bash
journalctl -u application
```

- Search for errors:

```bash
grep ERROR application.log
```

- Monitor running processes:

```bash
top
```

or

```bash
ps -ef
```

- Check disk usage:

```bash
df -h
```

- Locate large directories:

```bash
du -sh /*
```

- Verify storage devices:

```bash
lsblk
```

- Confirm network configuration:

```bash
ip addr
```

- Test remote connectivity:

```bash
ssh user@server
```

- Archive logs before making changes:

```bash
tar -czvf logs.tar.gz /var/log/
```

**Explanation**

Real production incidents often require multiple Linux commands working together rather than a single command. A systematic approach that combines service management, log analysis, process monitoring, storage investigation, networking, and secure remote access is a core expectation for DevOps, SRE, Cloud, and Infrastructure Engineer interviews. Mastering these essential commands enables efficient troubleshooting and faster incident resolution.
