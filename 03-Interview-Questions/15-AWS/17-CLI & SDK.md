# AWS CLI & SDK Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is the AWS CLI, and why is it used?

**Answer**

AWS Command Line Interface (AWS CLI) is a command-line tool used to interact with AWS services using commands instead of the AWS Management Console.

It allows users to:
- Create AWS resources
- Manage existing resources
- Automate AWS operations
- Integrate AWS tasks into shell scripts and CI/CD pipelines

**Explanation**

AWS CLI communicates with AWS APIs using configured credentials. It enables administrators and DevOps engineers to automate repetitive cloud management tasks.

**Where it is used in Production**

- Infrastructure automation
- CI/CD pipelines
- Server provisioning
- Resource management
- DevOps scripting

**Common Mistake**

Many candidates think AWS CLI is only for Linux. It is supported on Windows, Linux, and macOS.

---

### Question 2

**Question**

How do you configure AWS CLI?

**Answer**

AWS CLI is configured using the following command:

```bash
aws configure
```

It prompts for:

- AWS Access Key ID
- AWS Secret Access Key
- Default Region
- Default Output Format (json, yaml, text, table)

**Explanation**

The credentials are stored locally and used to authenticate AWS CLI commands.

**Where it is used in Production**

Every AWS CLI installation must be configured before accessing AWS resources.

**Common Mistake**

Committing AWS credentials to Git repositories instead of using secure credential management.

---

### Question 3

**Question**

Where does AWS CLI store its configuration files?

**Answer**

AWS CLI stores configuration in two files:

**Credentials**

```
~/.aws/credentials
```

**Configuration**

```
~/.aws/config
```

**Explanation**

The credentials file stores access keys, while the config file stores regions, output formats, and profile settings.

**Where it is used in Production**

Used on developer laptops, build servers, and automation environments.

---

### Question 4

**Question**

What are AWS CLI Profiles?

**Answer**

AWS CLI Profiles allow multiple AWS accounts or credential sets to be configured on the same machine.

Example:

```bash
aws configure --profile production
aws configure --profile development
```

Use a profile:

```bash
aws s3 ls --profile production
```

**Explanation**

Profiles simplify switching between AWS accounts without changing credentials.

**Where it is used in Production**

- Development environments
- Multi-account organizations
- Dev/Test/Production accounts

**Common Mistake**

Overwriting the default profile instead of creating separate named profiles.

---

### Question 5

**Question**

What command is used to verify AWS CLI is installed?

**Answer**

```bash
aws --version
```

**Explanation**

This command displays the installed AWS CLI version.

**Where it is used in Production**

Used during installation verification and troubleshooting.

---

### Question 6

**Question**

How do you list all S3 buckets using AWS CLI?

**Answer**

```bash
aws s3 ls
```

**Explanation**

This command retrieves all S3 buckets accessible using the configured AWS credentials.

**Where it is used in Production**

- Storage administration
- Backup verification
- Automation scripts

---

### Question 7

**Question**

How do you list EC2 instances using AWS CLI?

**Answer**

```bash
aws ec2 describe-instances
```

**Explanation**

This command retrieves information about EC2 instances in the configured AWS Region.

**Where it is used in Production**

- Infrastructure auditing
- Automation
- Inventory reporting

**Common Mistake**

Forgetting to specify the correct Region, resulting in no resources being returned.

---

### Question 8

**Question**

What is the difference between AWS CLI and the AWS Management Console?

**Answer**

| AWS CLI | AWS Management Console |
|----------|------------------------|
| Command-line interface | Web-based interface |
| Supports automation | Manual operations |
| Scriptable | Not easily scriptable |
| Faster for repetitive tasks | Easier for beginners |

**Explanation**

The AWS CLI is preferred by DevOps engineers because it enables automation and integration into scripts.

**Where it is used in Production**

Infrastructure automation and CI/CD pipelines.

---

### Question 9

**Question**

What is an AWS SDK?

**Answer**

AWS Software Development Kits (SDKs) allow developers to interact with AWS services using programming languages.

Examples include:

- Python (Boto3)
- Java
- JavaScript
- Go
- .NET
- PHP

**Explanation**

SDKs simplify AWS API calls by providing language-specific libraries.

**Where it is used in Production**

- Application development
- Infrastructure automation
- Serverless applications

**Common Mistake**

Confusing AWS CLI with AWS SDK. CLI is command-line based, whereas SDKs are programming libraries.

---

### Question 10

**Question**

When should you use AWS CLI instead of an SDK?

**Answer**

Use AWS CLI for:

- Manual administration
- Automation scripts
- CI/CD pipelines
- Resource management

Use SDKs for:

- Application development
- Backend services
- Custom automation
- Programmatic AWS integration

**Explanation**

CLI is ideal for administrators, while SDKs are intended for software developers.

**Where it is used in Production**

Organizations commonly use both depending on the use case.

---

### Question 11

**Question**

What are some commonly used AWS CLI commands?

**Answer**

Examples include:

```bash
aws configure
aws --version
aws s3 ls
aws ec2 describe-instances
aws iam list-users
aws sts get-caller-identity
aws lambda list-functions
```

**Explanation**

These commands help administrators verify credentials, inspect infrastructure, and manage AWS resources.

**Where it is used in Production**

Daily cloud administration and automation.

---

### Question 12

**Question**

Why is AWS CLI important for DevOps engineers?

**Answer**

AWS CLI enables:

- Infrastructure automation
- Resource provisioning
- Script execution
- CI/CD integration
- Faster cloud administration
- Repeatable operations

**Explanation**

Most DevOps automation relies on command-line tools rather than manual console operations.

**Where it is used in Production**

- Jenkins pipelines
- GitHub Actions
- Terraform automation
- Shell scripts
- Infrastructure management

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A Jenkins pipeline fails with the error "Unable to locate credentials." How would you troubleshoot?

**Answer**

Check:

- AWS CLI configuration
- IAM credentials
- Environment variables
- AWS Profiles
- IAM permissions
- Credential expiration

**Explanation**

Most authentication failures occur because AWS CLI cannot locate valid credentials.

---

### Scenario 2

**Question**

Your AWS CLI command returns "Access Denied." What would you investigate?

**Answer**

Verify:

- IAM user permissions
- IAM role permissions
- Resource policies
- AWS Region
- Correct AWS Profile

**Explanation**

"Access Denied" typically indicates insufficient IAM permissions.

---

### Scenario 3

**Question**

You manage Development, Testing, and Production AWS accounts. How would you switch between them using AWS CLI?

**Answer**

Create separate AWS Profiles and specify the required profile using:

```bash
aws <service> <command> --profile production
```

**Explanation**

Profiles allow secure management of multiple AWS accounts from a single workstation.

---

### Scenario 4

**Question**

Your AWS CLI commands suddenly stop working after rotating IAM access keys. What should you do?

**Answer**

Update the AWS CLI configuration using:

```bash
aws configure
```

or update the appropriate AWS Profile with the new credentials.

**Explanation**

Old credentials become invalid after key rotation.

---

### Scenario 5

**Question**

You need a daily report of all EC2 instances. How would you automate it?

**Answer**

Create a shell or Python script using AWS CLI:

```bash
aws ec2 describe-instances
```

Schedule it using cron (Linux) or Task Scheduler (Windows).

**Explanation**

AWS CLI enables repeatable infrastructure reporting through automation.

---

### Scenario 6

**Question**

A developer accidentally performs operations in the wrong AWS account. How can this be prevented?

**Answer**

Use separate AWS Profiles and verify the active account using:

```bash
aws sts get-caller-identity
```

before executing commands.

**Explanation**

Profiles reduce the risk of managing resources in the wrong account.

---

### Scenario 7

**Question**

Your team wants to upload build artifacts to Amazon S3 after every successful deployment. How would you accomplish this?

**Answer**

Use AWS CLI within the CI/CD pipeline:

```bash
aws s3 cp build.zip s3://my-bucket/
```

**Explanation**

AWS CLI integrates easily with Jenkins, GitHub Actions, Azure DevOps, and other CI/CD tools.

---

### Scenario 8

**Question**

A deployment script works locally but fails on the production server with AWS authentication errors. What would you verify?

**Answer**

Check:

- AWS CLI installation
- IAM role or credentials
- AWS Profile
- Region configuration
- Environment variables

**Explanation**

Production servers often use IAM roles instead of access keys.

---

### Scenario 9

**Question**

Your application needs to automatically upload files to Amazon S3. Should you use AWS CLI or an AWS SDK?

**Answer**

Use an AWS SDK such as Boto3 (Python).

**Explanation**

SDKs are designed for application integration, whereas AWS CLI is intended for administration and scripting.

---

### Scenario 10

**Question**

A DevOps engineer needs to automate EC2 provisioning, S3 uploads, IAM user management, and Lambda deployments. Which tool would you recommend?

**Answer**

Use AWS CLI for scripting and automation or AWS SDKs for application-level automation, depending on the use case.

**Explanation**

AWS CLI is ideal for operational automation, while SDKs provide greater flexibility for application development and complex workflows.
