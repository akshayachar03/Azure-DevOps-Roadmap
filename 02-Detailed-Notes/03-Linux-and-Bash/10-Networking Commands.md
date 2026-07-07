# Networking Commands

## Overview

Linux Networking Commands are essential tools used to:

- Configure network interfaces
- Test network connectivity
- Download files
- Access remote servers
- Transfer files securely
- Monitor network connections
- Troubleshoot networking issues

These commands are used daily by:

- DevOps Engineers
- Cloud Engineers
- Site Reliability Engineers (SREs)
- Linux Administrators
- Platform Engineers

> **Interview Point**
>
> Modern Linux systems primarily use the **`ip`** command instead of older tools such as `ifconfig` and `route`.

---

## Why It Is Used

Networking commands help to:

- Verify network connectivity
- Configure interfaces
- Test DNS resolution
- Download deployment packages
- Access cloud servers
- Troubleshoot application connectivity
- Monitor active network connections

---

## Architecture / Working

```mermaid
flowchart LR

Application

Application --> NetworkInterface

NetworkInterface --> Router

Router --> Internet

Internet --> RemoteServer
```

---

## Key Components

| Component | Purpose |
|------------|----------|
| IP Address | Identifies a device |
| Network Interface | Physical/Virtual network adapter |
| DNS | Resolves domain names |
| Gateway | Routes traffic outside the local network |
| SSH | Secure remote access |
| TCP/UDP | Transport protocols |

---

## Types

### Network Configuration

- ip
- hostname

### Connectivity Testing

- ping

### HTTP Communication

- curl
- wget

### Remote Access

- ssh
- scp

### Network Monitoring

- ss
- netstat

---

## Lifecycle / Workflow

```mermaid
flowchart LR

CheckIP

CheckIP --> TestConnectivity

TestConnectivity --> AccessRemoteHost

AccessRemoteHost --> TransferFiles

TransferFiles --> MonitorConnections
```

---

## Configuration / Syntax

Common workflow

```bash
ip

ping

curl

ssh

scp

ss
```

---

## Important Commands

```bash
ip

ping

curl

wget

ssh

scp

ss

netstat

hostname
```

---

## Important Files

| File | Purpose |
|------|---------|
| /etc/hosts | Local hostname resolution |
| /etc/resolv.conf | DNS configuration |
| /etc/hostname | System hostname |
| /etc/ssh/sshd_config | SSH server configuration |
| /etc/ssh/ssh_config | SSH client configuration |

---

## Real-World Use Cases

- Connect to Azure/Linux VMs
- Test API endpoints
- Download deployment artifacts
- Transfer configuration files
- Troubleshoot production connectivity
- Verify listening services

---

## Advantages

- Lightweight
- Fast troubleshooting
- Essential for automation
- Available on most Linux distributions

---

## Limitations

- Some commands require elevated privileges
- Firewall rules may affect command output

---

## Common Interview Questions (Concept Only)

- Difference between `curl` and `wget`?
- Difference between `netstat` and `ss`?
- Difference between `scp` and `ssh`?
- What is the purpose of the `ip` command?
- Why is `ss` preferred over `netstat`?

---

## Common Mistakes

- Confusing hostname with IP address
- Using `wget` for API testing instead of `curl`
- Forgetting SSH key permissions
- Using deprecated commands when modern alternatives exist

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Cannot reach server | Verify IP, routing, firewall, and DNS |
| SSH connection refused | Verify SSH service and firewall |
| Download failed | Check URL and internet connectivity |
| DNS issues | Verify `/etc/resolv.conf` and test name resolution |

---

## Summary

Linux Networking Commands are fundamental tools for configuring networks, testing connectivity, accessing remote systems, and troubleshooting production environments.

---

# ip

## Overview

`ip` is the modern Linux networking utility used to manage:

- IP addresses
- Network interfaces
- Routes
- Neighbor tables

It replaces older commands such as:

- ifconfig
- route
- arp

> **Interview Point**
>
> The `ip` command is part of the **iproute2** package and is the standard networking utility on modern Linux systems.

---

## Why It Is Used

- View IP addresses
- Configure interfaces
- Display routing tables
- Troubleshoot networking

---

## Architecture / Working

```mermaid
flowchart LR

Kernel --> ip --> NetworkInterfaces
```

---

## Key Components

| Command | Purpose |
|----------|----------|
| ip addr | Display IP addresses |
| ip link | Display interfaces |
| ip route | Display routing table |
| ip neigh | Display ARP/neighbor table |

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Interface --> AssignIP --> ConfigureRoute --> Communicate
```

---

## Configuration / Syntax

Show interfaces

```bash
ip addr
```

Show routes

```bash
ip route
```

Show interfaces only

```bash
ip link
```

---

## Important Commands

```bash
ip addr

ip route

ip link

ip neigh
```

---

## Important Files

| File | Purpose |
|------|---------|
| /etc/network/interfaces (Debian, if used) | Interface configuration (legacy) |
| NetworkManager configuration (distribution-dependent) | Interface management |

---

## Real-World Use Cases

- Check VM IP
- Verify routes
- Troubleshoot cloud networking

---

## Advantages

- Comprehensive
- Modern
- Replaces multiple legacy commands

---

## Limitations

- Syntax is more extensive than older utilities

---

## Common Interview Questions (Concept Only)

- What replaced `ifconfig`?
- Difference between `ip addr` and `ip route`?

---

## Common Mistakes

- Confusing interface status with routing information

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Missing IP | Verify interface configuration |
| Incorrect route | Review routing table with `ip route` |

---

## Summary

`ip` is the standard Linux networking utility used for interface, address, and route management.

---

# ping

## Overview

`ping` tests connectivity between two network devices using **ICMP Echo Request** and **Echo Reply** messages.

It measures:

- Reachability
- Packet loss
- Round-trip time (RTT)

> **Interview Point**
>
> A failed `ping` does **not always** indicate the host is down. ICMP traffic may be blocked by firewalls or security policies.

---

## Why It Is Used

- Verify connectivity
- Troubleshoot networking
- Measure latency

---

## Architecture / Working

```mermaid
flowchart LR

Client --> ICMPRequest --> Server

Server --> ICMPReply --> Client
```

---

## Configuration / Syntax

```bash
ping google.com

ping 8.8.8.8

ping -c 4 google.com
```

---

## Important Commands

```bash
ping

ping -c
```

---

## Real-World Use Cases

- Verify internet access
- Test cloud VM connectivity
- Troubleshoot DNS

---

## Advantages

- Simple
- Fast
- Universal

---

## Limitations

- Depends on ICMP availability
- Cannot diagnose application-layer issues

---

## Common Interview Questions (Concept Only)

- What protocol does `ping` use?
- What does latency represent?
- Why can `ping` fail even when a service is available?

---

## Common Mistakes

- Assuming a failed `ping` always means the server is offline

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| No response | Check firewall, routing, or ICMP filtering |
| High latency | Investigate network congestion or routing |

---

## Summary

`ping` verifies network connectivity and measures latency using ICMP.

---

# curl

## Overview

`curl` is a command-line tool used to transfer data using protocols such as:

- HTTP
- HTTPS
- FTP
- SFTP

It is widely used for:

- REST APIs
- Health checks
- Downloading data
- Debugging web services

> **Interview Point**
>
> `curl` is primarily used for **sending HTTP requests and testing APIs**, not just downloading files.

---

## Why It Is Used

- Test REST APIs
- Check application health
- Download files
- Debug HTTP requests

---

## Architecture / Working

```mermaid
flowchart LR

Client --> HTTPRequest --> Server

Server --> HTTPResponse --> Client
```

---

## Configuration / Syntax

```bash
curl https://example.com

curl -I https://example.com

curl -X POST URL
```

---

## Important Commands

```bash
curl

curl -I

curl -O

curl -X
```

---

## Real-World Use Cases

- Kubernetes API testing
- Azure REST API
- Health checks
- CI/CD validation

---

## Advantages

- Supports many protocols
- API testing
- Script-friendly

---

## Limitations

- Steeper learning curve for complex requests

---

## Common Interview Questions (Concept Only)

- Difference between `curl` and `wget`?
- What does `curl -I` do?

---

## Common Mistakes

- Using `curl` without quoting complex URLs containing special characters

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Connection failed | Verify URL, DNS, and firewall |
| SSL error | Verify certificates or use appropriate options for testing |

---

## Summary

`curl` is a versatile networking tool for interacting with web services, APIs, and remote servers.

---

# wget

## Overview

`wget` downloads files from remote servers using protocols such as HTTP, HTTPS, and FTP.

It is optimized for file retrieval and supports resuming interrupted downloads.

> **Interview Point**
>
> Unlike `curl`, `wget` is primarily designed for downloading files.

---

## Why It Is Used

- Download software
- Retrieve backups
- Download deployment artifacts

---

## Architecture / Working

```mermaid
flowchart LR

RemoteServer --> wget --> LocalFile
```

---

## Configuration / Syntax

```bash
wget URL

wget -c URL

wget -O file URL
```

---

## Important Commands

```bash
wget

wget -c

wget -O
```

---

## Real-World Use Cases

- Download installers
- Retrieve application packages
- Download Kubernetes binaries

---

## Advantages

- Reliable downloads
- Resume support

---

## Limitations

- Less flexible than `curl` for API interactions

---

## Common Interview Questions (Concept Only)

- Difference between `wget` and `curl`?
- What does `wget -c` do?

---

## Common Mistakes

- Using `wget` for interactive API testing

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Download interrupted | Resume with `wget -c` |
| SSL issues | Verify certificates |

---

## Summary

`wget` is a reliable file download utility commonly used for retrieving software packages and deployment artifacts.

---

# ssh

## Overview

`ssh` (Secure Shell) provides encrypted remote access to Linux servers.

It is the standard protocol for remote Linux administration.

> **Interview Point**
>
> SSH uses **TCP port 22** by default and supports both password-based and key-based authentication.

---

## Why It Is Used

- Remote administration
- Cloud server access
- Secure command execution

---

## Architecture / Working

```mermaid
flowchart LR

Client --> SSH --> RemoteServer
```

---

## Key Components

| Component | Purpose |
|------------|----------|
| SSH Client | Initiates connection |
| SSH Server | Accepts connections |
| Public Key | Shared with the server |
| Private Key | Kept secure by the client |

---

## Configuration / Syntax

Password authentication

```bash
ssh user@host
```

Private key authentication

```bash
ssh -i key.pem azureuser@IP
```

---

## Important Commands

```bash
ssh

ssh -i

ssh -p
```

---

## Important Files

| File | Purpose |
|------|---------|
| ~/.ssh/id_rsa | Private key (RSA) |
| ~/.ssh/id_ed25519 | Private key (Ed25519) |
| ~/.ssh/authorized_keys | Authorized public keys |
| /etc/ssh/sshd_config | SSH server configuration |

---

## Real-World Use Cases

- Azure VM access
- AWS EC2 access
- Production server administration

---

## Advantages

- Secure
- Encrypted
- Widely supported

---

## Limitations

- Firewall rules can block access
- Private key management is critical

---

## Common Interview Questions (Concept Only)

- What is SSH?
- Why is key-based authentication preferred?
- What port does SSH use?

---

## Common Mistakes

- Incorrect private key permissions
- Using the wrong username
- Exposing private keys

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Connection refused | Verify SSH service and firewall |
| Permission denied | Check username, key permissions, and authorized keys |

---

## Summary

`ssh` provides secure remote administration and is one of the most essential tools for Linux, DevOps, and Cloud engineers.

---

# scp

## Overview

`scp` (Secure Copy) securely transfers files between systems using the SSH protocol.

> **Interview Point**
>
> `scp` uses **SSH for encryption**, making it secure for transferring files over untrusted networks.

---

## Why It Is Used

- Upload deployment files
- Download logs
- Copy configuration files
- Backup servers

---

## Architecture / Working

```mermaid
flowchart LR

LocalMachine --> SSH --> RemoteMachine
```

---

## Configuration / Syntax

Copy file to remote server

```bash
scp file.txt user@host:/home/user/
```

Copy file from remote server

```bash
scp user@host:/home/user/file.txt .
```

Copy a directory recursively

```bash
scp -r project/ user@host:/home/user/
```

---

## Important Commands

```bash
scp

scp -r

scp -i
```

---

## Real-World Use Cases

- Deploy application artifacts
- Copy backups
- Retrieve log files

---

## Advantages

- Secure
- Simple
- Uses SSH authentication

---

## Limitations

- Less efficient for synchronizing large directory trees than specialized tools like `rsync`

---

## Common Interview Questions (Concept Only)

- Difference between `scp` and `ssh`?
- What does `scp -r` do?

---

## Common Mistakes

- Forgetting recursive copy for directories
- Using incorrect destination paths

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Permission denied | Verify SSH credentials and permissions |
| Transfer failed | Check connectivity and available disk space |

---

## Summary

`scp` securely transfers files between systems using SSH and is commonly used for deployments and backups.

---

# netstat / ss

## Overview

`netstat` and `ss` display network connections, listening ports, routing information, and socket statistics.

`ss` is the modern replacement for `netstat`.

> **Interview Point**
>
> `ss` is faster and more efficient than `netstat` because it communicates directly with the Linux kernel.

---

## Why It Is Used

- Verify listening services
- Troubleshoot ports
- Investigate active connections
- Debug networking issues

---

## Architecture / Working

```mermaid
flowchart LR

Kernel --> ss --> NetworkConnections
```

---

## Key Components

| Information | Description |
|-------------|-------------|
| Listening Port | Service accepting connections |
| Established | Active connection |
| TCP | Connection-oriented protocol |
| UDP | Connectionless protocol |

---

## Configuration / Syntax

Using `ss`

```bash
ss -tuln
```

Using `netstat`

```bash
netstat -tuln
```

Show process information

```bash
ss -tulpn
```

---

## Important Commands

```bash
ss -tuln

ss -tulpn

netstat -tuln
```

---

## Real-World Use Cases

- Verify web servers
- Check Kubernetes services
- Troubleshoot application ports

---

## Advantages

- Fast
- Detailed
- Excellent for troubleshooting

---

## Limitations

- Process information may require elevated privileges

---

## Common Interview Questions (Concept Only)

- Difference between `ss` and `netstat`?
- How do you check which ports are listening?
- What do `-t`, `-u`, `-l`, and `-n` represent?

---

## Common Mistakes

- Forgetting elevated privileges when viewing process ownership
- Misinterpreting listening versus established connections

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Port not listening | Verify the application is running |
| Port conflict | Identify the process using the port and resolve the conflict |

---

## Summary

`ss` (and the legacy `netstat`) provide detailed information about network sockets and are essential tools for diagnosing connectivity and service issues.

---

# hostname

## Overview

`hostname` displays or configures the system's hostname.

The hostname is the human-readable name used to identify a system on a network.

> **Interview Point**
>
> The hostname identifies the **system**, not the network interface or IP address.

---

## Why It Is Used

- Identify servers
- Configure cloud VMs
- Troubleshoot DNS
- Manage infrastructure

---

## Architecture / Working

```mermaid
flowchart LR

System --> Hostname --> NetworkIdentity
```

---

## Configuration / Syntax

Display hostname

```bash
hostname
```

Display fully qualified domain name (FQDN)

```bash
hostname -f
```

Set hostname temporarily

```bash
sudo hostname new-server
```

Persistent hostname (systemd-based systems)

```bash
sudo hostnamectl set-hostname new-server
```

---

## Important Commands

```bash
hostname

hostname -f

hostnamectl
```

---

## Important Files

| File | Purpose |
|------|---------|
| /etc/hostname | Stores the persistent hostname |
| /etc/hosts | Local hostname-to-IP mappings |

---

## Real-World Use Cases

- Configure cloud VM names
- Server identification
- DNS troubleshooting
- Cluster management

---

## Advantages

- Easy server identification
- Simplifies administration
- Supports automation and monitoring

---

## Limitations

- Changing the hostname alone does not update DNS records automatically

---

## Common Interview Questions (Concept Only)

- What is a hostname?
- Difference between a hostname and an IP address?
- How do you change the hostname permanently?
- What is an FQDN?

---

## Common Mistakes

- Assuming hostname changes automatically update DNS
- Forgetting to update `/etc/hosts` where appropriate

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Incorrect hostname | Verify `/etc/hostname` and use `hostnamectl` |
| Hostname resolution issues | Check `/etc/hosts` and DNS configuration |

---

## Summary

`hostname` identifies a Linux system on a network and is an essential command for server administration, cloud deployments, and troubleshooting.
