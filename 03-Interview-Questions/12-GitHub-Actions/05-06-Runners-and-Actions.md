# Runners & Actions Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are Runners in GitHub Actions?

**Answer**

Runners are machines that execute GitHub Actions workflows.

GitHub supports two types of runners:

- GitHub-hosted runners
- Self-hosted runners

**Explanation**

Whenever a workflow is triggered, GitHub assigns a runner to execute the jobs defined in the workflow. Every job runs on a runner specified using the `runs-on` keyword.

**Where it is used in Production**

Every GitHub Actions workflow uses a runner to execute builds, tests, deployments, and automation tasks.

**Common Mistake**

Many candidates think a runner executes the entire workflow. In reality, each **job** runs on a runner.

---

### Question 2

**Question**

What is the difference between GitHub-hosted runners and Self-hosted runners?

**Answer**

| GitHub-Hosted Runner | Self-Hosted Runner |
|----------------------|--------------------|
| Managed by GitHub | Managed by the organization |
| Automatically provisioned | Requires installation and maintenance |
| Ready to use | Customizable |
| Internet accessible | Can access private infrastructure |

**Explanation**

GitHub-hosted runners are ideal for general CI/CD tasks, while self-hosted runners provide greater control and access to internal resources.

**Where it is used in Production**

- GitHub-hosted runners for standard CI pipelines.
- Self-hosted runners for deployments to private networks and enterprise environments.

---

### Question 3

**Question**

When should you use a Self-hosted Runner instead of a GitHub-hosted Runner?

**Answer**

Use a Self-hosted Runner when:

- Access to private servers is required.
- Internal databases must be accessed.
- Custom software or tools are needed.
- Company security policies require on-premises execution.
- Specialized hardware is required.

**Explanation**

Self-hosted runners provide complete control over the execution environment.

**Where it is used in Production**

Enterprise deployments to private data centers, Kubernetes clusters, or internal networks.

---

### Question 4

**Question**

What are Runner Labels in GitHub Actions?

**Answer**

Runner Labels identify runners with specific capabilities.

Examples:

- ubuntu-latest
- windows-latest
- self-hosted
- linux
- production

**Explanation**

Labels help GitHub select the appropriate runner for a job.

Example:

```yaml
runs-on: ubuntu-latest
```

**Where it is used in Production**

Running workloads on operating system-specific or environment-specific runners.

---

### Question 5

**Question**

What are Actions in GitHub Actions?

**Answer**

Actions are reusable units of automation that perform specific tasks within a workflow.

Examples include:

- Checking out source code
- Setting up programming languages
- Building applications
- Deploying applications

**Explanation**

Actions eliminate the need to write repetitive automation code.

**Where it is used in Production**

Every GitHub Actions workflow uses one or more actions.

---

### Question 6

**Question**

What are Marketplace Actions?

**Answer**

Marketplace Actions are pre-built actions published in the GitHub Marketplace that can be reused in workflows.

Popular examples include:

- actions/checkout
- actions/setup-java
- actions/setup-node
- docker/login-action

**Explanation**

Marketplace Actions simplify workflow development by providing tested and reusable automation components.

**Where it is used in Production**

CI/CD pipelines across nearly every GitHub-based project.

---

### Question 7

**Question**

What are Reusable Actions?

**Answer**

Reusable Actions are custom actions created by organizations or developers that can be reused across multiple workflows and repositories.

**Explanation**

Instead of duplicating workflow logic, reusable actions encapsulate common tasks into a single reusable component.

**Where it is used in Production**

Large organizations standardize CI/CD processes using reusable actions.

---

### Question 8

**Question**

What are Third-Party Actions?

**Answer**

Third-Party Actions are actions created by community members or external organizations and published on GitHub Marketplace.

**Explanation**

They provide integrations for cloud providers, deployment tools, testing frameworks, and many other services.

**Where it is used in Production**

- AWS deployments
- Azure deployments
- Kubernetes deployments
- Docker builds

**Common Mistake**

Many candidates assume all Marketplace Actions are officially maintained by GitHub. Many are maintained by third parties.

---

### Question 9

**Question**

Why should you use specific Action Versions instead of the latest version?

**Answer**

Using a specific version ensures workflow stability and reproducibility.

Example:

```yaml
uses: actions/checkout@v4
```

instead of

```yaml
uses: actions/checkout@main
```

**Explanation**

Pinned versions prevent unexpected failures caused by future updates.

**Where it is used in Production**

All enterprise CI/CD pipelines.

---

### Question 10

**Question**

How do you use an Action in a workflow?

**Answer**

Actions are referenced using the `uses` keyword.

Example:

```yaml
steps:
  - uses: actions/checkout@v4
```

**Explanation**

GitHub downloads the action and executes it as part of the workflow.

**Where it is used in Production**

Every GitHub Actions workflow.

---

### Question 11

**Question**

What are the advantages of using Marketplace Actions?

**Answer**

Benefits include:

- Faster workflow development
- Reduced scripting
- Reusable automation
- Community-tested solutions
- Easier maintenance

**Explanation**

Marketplace Actions help teams build reliable pipelines with minimal custom code.

**Where it is used in Production**

CI/CD, testing, deployments, security scanning, and infrastructure automation.

---

### Question 12

**Question**

What security precautions should you follow when using Third-Party Actions?

**Answer**

Best practices include:

- Use trusted publishers.
- Pin actions to specific versions.
- Review the source code when possible.
- Grant minimum required permissions.
- Regularly update actions.

**Explanation**

Third-party actions execute code in your workflow, so they should be treated as part of your software supply chain.

**Where it is used in Production**

Enterprise CI/CD environments with strict security requirements.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Your GitHub-hosted runner cannot access an internal production server. How would you solve this?

**Answer**

I would configure a **Self-hosted Runner** inside the organization's private network.

**Explanation**

Self-hosted runners can access internal infrastructure that GitHub-hosted runners cannot reach.

---

### Scenario 2

**Question**

Your workflow must run only on Windows machines. How would you configure it?

**Answer**

I would specify:

```yaml
runs-on: windows-latest
```

**Explanation**

Runner labels determine which operating system executes the workflow.

---

### Scenario 3

**Question**

A workflow remains in the "Waiting for Runner" state. What would you investigate?

**Answer**

I would verify:

- Runner availability
- Runner online status
- Runner labels
- Job configuration
- GitHub Actions service status

**Explanation**

Jobs remain queued until a compatible runner becomes available.

---

### Scenario 4

**Question**

Your organization has multiple self-hosted runners for Development, QA, and Production. How would you ensure production deployments only run on production runners?

**Answer**

I would assign a label such as:

```yaml
runs-on:
  - self-hosted
  - production
```

**Explanation**

Runner labels ensure workflows execute on the correct infrastructure.

---

### Scenario 5

**Question**

A Marketplace Action suddenly causes your workflow to fail after an update. How would you prevent this in the future?

**Answer**

I would pin the action to a specific stable version instead of using a moving reference like `main` or `latest`.

**Explanation**

Version pinning ensures consistent workflow behavior.

---

### Scenario 6

**Question**

Your team repeatedly copies the same deployment steps into multiple repositories. How would you improve this?

**Answer**

I would create a **Reusable Action** that encapsulates the deployment logic and reference it from all repositories.

**Explanation**

Reusable actions reduce duplication and simplify maintenance.

---

### Scenario 7

**Question**

Your security team asks whether it is safe to use Third-Party Actions. What would you tell them?

**Answer**

I would explain that Third-Party Actions are useful but should be used carefully by:

- Choosing trusted publishers
- Pinning versions
- Reviewing permissions
- Auditing the source code when possible

**Explanation**

These practices reduce supply chain security risks.

---

### Scenario 8

**Question**

A deployment requires software that is unavailable on GitHub-hosted runners. What would you do?

**Answer**

I would use a **Self-hosted Runner** with the required software pre-installed.

**Explanation**

Self-hosted runners allow complete customization of the execution environment.

---

### Scenario 9

**Question**

A workflow fails because it cannot find the required Java version. How would you resolve this?

**Answer**

I would use a Marketplace Action such as:

```yaml
uses: actions/setup-java@v4
```

to install and configure the required Java version before running the build.

**Explanation**

Setup actions prepare the runner with the required runtime or tools.

---

### Scenario 10

**Question**

Your manager wants to standardize CI/CD pipelines across dozens of repositories while minimizing maintenance. What approach would you recommend?

**Answer**

I would:

- Create reusable custom actions for common tasks.
- Use trusted Marketplace Actions where appropriate.
- Pin action versions.
- Use runner labels to target the correct execution environment.

**Explanation**

This approach reduces duplication, improves consistency, simplifies updates, and creates maintainable enterprise-grade GitHub Actions workflows.
