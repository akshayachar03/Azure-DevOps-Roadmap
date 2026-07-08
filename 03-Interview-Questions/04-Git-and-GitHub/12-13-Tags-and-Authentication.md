# Git Tags & Authentication Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are Git Tags, and why are they used?

**Answer**

Git Tags are references that point to specific commits, typically used to mark important milestones such as releases or version numbers.

Examples:

- v1.0.0
- v2.1.5
- release-2025

Unlike branches, tags do not move when new commits are added.

**Explanation**

Tags provide a permanent reference to a particular commit, making it easy to identify stable releases.

**Used in Production**

- Software releases
- Version management
- Rollbacks
- CI/CD release pipelines

**Common Mistake**

Many candidates think tags behave like branches. Tags are fixed references and do not move automatically.

---

### Question 2

**Question**

What is the difference between Lightweight Tags and Annotated Tags?

**Answer**

| Lightweight Tag | Annotated Tag |
|-----------------|---------------|
| Simple pointer to a commit | Full Git object |
| No metadata | Stores author, date, message |
| Suitable for temporary tags | Suitable for releases |

Lightweight Tag:

```bash
git tag v1.0
```

Annotated Tag:

```bash
git tag -a v1.0 -m "First stable release"
```

**Explanation**

Annotated tags contain additional metadata and are preferred for production releases.

**Used in Production**

Most organizations use annotated tags for official software versions.

---

### Question 3

**Question**

How do you create a Git Tag?

**Answer**

Create a lightweight tag:

```bash
git tag v1.0
```

Create an annotated tag:

```bash
git tag -a v1.0 -m "Release Version 1.0"
```

View tags:

```bash
git tag
```

**Explanation**

Tags are usually created after successful testing and before deployment.

**Used in Production**

Created before releasing applications.

---

### Question 4

**Question**

How do you push tags to a remote repository?

**Answer**

Push one tag:

```bash
git push origin v1.0
```

Push all tags:

```bash
git push origin --tags
```

**Explanation**

Tags remain local until explicitly pushed to the remote repository.

**Used in Production**

Required so CI/CD pipelines and teammates can access release tags.

**Common Mistake**

Candidates often assume `git push` automatically pushes tags.

---

### Question 5

**Question**

What is the difference between HTTPS and SSH authentication in Git?

**Answer**

| HTTPS | SSH |
|--------|-----|
| Uses username and PAT | Uses SSH key pair |
| Easier initial setup | More secure and convenient |
| May require PAT | Passwordless after setup |

**Explanation**

Both methods securely authenticate users with remote repositories.

**Used in Production**

SSH is generally preferred for frequent development.

---

### Question 6

**Question**

What are SSH Keys?

**Answer**

SSH Keys are a pair of cryptographic keys used for secure authentication.

They consist of:

- Private Key (kept secret)
- Public Key (uploaded to GitHub, GitLab, Azure DevOps, etc.)

Generate keys:

```bash
ssh-keygen -t ed25519
```

**Explanation**

SSH authentication removes the need to repeatedly enter credentials.

**Used in Production**

Widely used by DevOps engineers for Git operations and server access.

---

### Question 7

**Question**

What is the purpose of a Personal Access Token (PAT)?

**Answer**

A Personal Access Token is a secure token used instead of a password for HTTPS authentication.

It supports:

- Git operations
- API access
- Automation
- CI/CD pipelines

**Explanation**

Modern Git platforms have deprecated password-based authentication in favor of PATs.

**Used in Production**

Used for automation, scripts, and CI/CD pipelines.

---

### Question 8

**Question**

When should you use SSH authentication instead of HTTPS?

**Answer**

SSH is preferred when:

- You work with repositories frequently.
- Passwordless authentication is desired.
- Security is a priority.
- Automation is required.

HTTPS is suitable for occasional repository access.

**Explanation**

SSH offers greater convenience for daily development after the initial setup.

**Used in Production**

Most enterprise developers configure SSH for regular Git usage.

---

### Question 9

**Question**

How do you verify whether SSH authentication is working?

**Answer**

Run:

```bash
ssh -T git@github.com
```

If successful, GitHub confirms authentication.

**Explanation**

This command tests the SSH connection without performing Git operations.

**Used in Production**

Often used after configuring SSH keys.

---

### Question 10

**Question**

How do you view existing Git Tags?

**Answer**

List all tags:

```bash
git tag
```

Show detailed information for an annotated tag:

```bash
git show v1.0
```

**Explanation**

Git provides commands to list and inspect tag information.

**Used in Production**

Developers verify release versions and associated commits.

---

### Question 11

**Question**

What authentication method is commonly used in CI/CD pipelines?

**Answer**

Most CI/CD pipelines use:

- Personal Access Tokens (PAT)
- Service Accounts
- SSH Keys (in some environments)

Authentication credentials are stored securely using:

- Secret Managers
- Environment Variables
- CI/CD Secret Stores

**Explanation**

Automation requires non-interactive authentication.

**Used in Production**

Azure DevOps, GitHub Actions, Jenkins, GitLab CI, and other CI/CD tools rely on secure credentials.

**Common Mistake**

Hardcoding PATs or SSH private keys directly into scripts or repositories.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your team is releasing version 2.0 of an application. How would you permanently mark this release in Git?

**Answer**

Create an annotated tag:

```bash
git tag -a v2.0 -m "Release Version 2.0"
```

Push it:

```bash
git push origin v2.0
```

**Explanation**

Annotated tags are the standard way to mark production releases.

---

### Scenario 2

**Question**

You created a Git tag locally, but your teammates cannot see it. Why?

**Answer**

Tags are not automatically pushed.

Run:

```bash
git push origin --tags
```

or

```bash
git push origin v2.0
```

**Explanation**

Git requires tags to be pushed separately.

---

### Scenario 3

**Question**

Your company disables password authentication for GitHub. Which authentication methods can you use?

**Answer**

Use:

- Personal Access Token (HTTPS)
- SSH Keys

**Explanation**

Modern Git hosting platforms no longer support password authentication for Git operations.

---

### Scenario 4

**Question**

You work on GitHub every day and are tired of entering credentials repeatedly. What authentication method would you recommend?

**Answer**

Configure SSH authentication using an SSH key pair.

**Explanation**

SSH enables secure, passwordless authentication after setup.

---

### Scenario 5

**Question**

A CI/CD pipeline needs to clone a private repository automatically. What authentication method should it use?

**Answer**

Use:

- Personal Access Token (PAT)
- Service Account credentials
- SSH Keys (depending on the environment)

Store the credentials securely in the CI/CD platform's secret store.

**Explanation**

Automation requires secure, non-interactive authentication.

---

### Scenario 6

**Question**

You generate an SSH key pair but GitHub still asks for credentials. What troubleshooting steps would you perform?

**Answer**

- Verify the public key is added to GitHub.
- Check that the SSH agent is running.
- Ensure the private key is loaded.
- Test using:

```bash
ssh -T git@github.com
```

- Verify the repository uses the SSH URL instead of HTTPS.

**Explanation**

Authentication issues usually result from configuration errors rather than Git itself.

---

### Scenario 7

**Question**

A teammate accidentally committed a Personal Access Token into a Git repository. What should be done immediately?

**Answer**

- Revoke the compromised PAT.
- Generate a new PAT.
- Remove the token from the repository history if required.
- Rotate any affected credentials.
- Review repository access logs.

**Explanation**

A leaked PAT can grant unauthorized access and should be treated as a security incident.

---

### Scenario 8

**Question**

Your organization requires every production deployment to reference an exact version of the application. How can Git help?

**Answer**

Create annotated release tags for every production deployment.

Example:

```bash
git tag -a v3.2.0 -m "Production Release"
```

**Explanation**

Tags provide immutable references to released versions, making rollbacks and auditing easier.

---

### Scenario 9

**Question**

A release pipeline is configured to deploy only tagged commits, but the deployment never starts after creating a tag. What is the most likely reason?

**Answer**

The tag was created locally but not pushed.

Run:

```bash
git push origin --tags
```

**Explanation**

CI/CD systems monitor the remote repository, not your local repository.

---

### Scenario 10

**Question**

Your team wants detailed information about every software release, including the author, creation date, and release notes. Which type of tag should you use?

**Answer**

Use an annotated tag.

Example:

```bash
git tag -a v2.5 -m "Quarterly Production Release"
```

**Explanation**

Annotated tags store metadata and are designed for official releases.

---

### Scenario 11

**Question**

You are preparing a production release for an enterprise application. Your responsibilities include creating an official release tag, publishing it to the remote repository, configuring secure authentication for developers, and ensuring the CI/CD pipeline can access the private repository without exposing credentials. Describe the complete workflow.

**Answer**

A typical workflow is:

1. Ensure all changes are merged into the release branch.
2. Create an annotated release tag:

```bash
git tag -a v2.0.0 -m "Production Release v2.0.0"
```

3. Push the tag to the remote repository:

```bash
git push origin v2.0.0
```

4. Configure developers to use SSH authentication for secure, passwordless access.
5. Upload each developer's public SSH key to the Git hosting platform.
6. Configure CI/CD pipelines to authenticate using securely stored PATs or service account credentials.
7. Store all secrets in the platform's secure secret management system rather than hardcoding them.
8. Verify authentication using:

```bash
ssh -T git@github.com
```

9. Confirm the release pipeline detects the new tag and deploys the tagged version.

**Explanation**

This workflow demonstrates production-ready Git practices, including versioning with annotated tags, secure authentication using SSH and PATs, and proper secret management for automated deployments. These are common topics in DevOps, Cloud Engineer, Platform Engineer, and SRE interviews.
