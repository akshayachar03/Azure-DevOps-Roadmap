# Azure DevOps Security & Access Control Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Security & Access Control in Azure DevOps?

**Answer**

Security & Access Control in Azure DevOps is the process of controlling who can access, modify, and manage Azure DevOps resources.

It includes permissions for:

- Organizations
- Projects
- Azure Repos
- Pipelines
- Service Connections
- Environments
- Agent Pools
- Artifacts
- Azure Boards

**Explanation**

Azure DevOps uses Role-Based Access Control (RBAC) and permissions to ensure that users only have access to the resources required for their job.

**Used in Production**

Organizations use access control to protect source code, production pipelines, deployment environments, and cloud resources.

**Common Mistake**

Many candidates think Azure DevOps security applies only to Git repositories. It applies to nearly every Azure DevOps resource.

---

### Question 2

**Question**

How are users managed in Azure DevOps?

**Answer**

Users are added to an Azure DevOps Organization and assigned access to one or more Projects.

Users can be assigned through:

- Microsoft Entra ID
- Microsoft Account
- Azure DevOps invitation

Users are then assigned permissions based on groups and roles.

**Explanation**

User management allows organizations to control who can access projects and what actions they can perform.

**Used in Production**

Organizations onboard new employees by adding them to Microsoft Entra ID groups that synchronize with Azure DevOps.

---

### Question 3

**Question**

Why should Groups be used instead of assigning permissions directly to users?

**Answer**

Using Groups provides:

- Easier administration
- Consistent permissions
- Faster onboarding
- Simplified offboarding
- Reduced permission errors
- Better scalability

Example groups:

- Project Administrators
- Contributors
- Readers
- Build Administrators

**Explanation**

Permissions are managed centrally, reducing administrative effort and improving consistency.

**Used in Production**

Most organizations manage access through security groups rather than individual user permissions.

**Common Mistake**

Assigning permissions individually to every developer, which becomes difficult to maintain.

---

### Question 4

**Question**

What are the common roles in Azure DevOps?

**Answer**

Common project roles include:

| Role | Responsibilities |
|------|------------------|
| Project Administrator | Full project management |
| Contributor | Create and modify code, pipelines, and work items |
| Reader | Read-only access |
| Build Administrator | Manage build pipelines |
| Release Administrator | Manage release pipelines |

**Explanation**

Roles define the default permissions assigned to users and groups.

**Used in Production**

Organizations assign users to roles based on their responsibilities.

---

### Question 5

**Question**

What are Repository Permissions in Azure DevOps?

**Answer**

Repository Permissions control access to Azure Repos.

Common permissions include:

- Read
- Contribute
- Create Branch
- Force Push
- Delete Repository
- Create Tag
- Manage Permissions

**Explanation**

Repository permissions protect source code from unauthorized changes.

**Used in Production**

Most organizations restrict force pushes and repository deletion to administrators.

**Common Mistake**

Granting all developers unrestricted repository permissions.

---

### Question 6

**Question**

What are Branch Policies, and how do they improve repository security?

**Answer**

Branch Policies protect important branches such as `main` or `master`.

Common policies include:

- Pull Request required
- Minimum reviewers
- Build validation
- Comment resolution
- Linked work items
- Prevent direct pushes

**Explanation**

Branch Policies ensure code is reviewed and validated before being merged.

**Used in Production**

Most organizations protect production branches with mandatory Pull Request reviews and successful build validation.

---

### Question 7

**Question**

What are Pipeline Permissions?

**Answer**

Pipeline Permissions determine who can:

- View pipelines
- Edit pipelines
- Run pipelines
- Delete pipelines
- Manage pipeline security
- Access pipeline resources

**Explanation**

Restricting pipeline permissions prevents unauthorized users from modifying or executing CI/CD workflows.

**Used in Production**

Production deployment pipelines are typically editable only by DevOps engineers or release administrators.

---

### Question 8

**Question**

What are Service Connection Permissions?

**Answer**

Service Connection Permissions control who can:

- Use a Service Connection
- Modify a Service Connection
- Delete a Service Connection
- Grant access to pipelines
- Manage credentials

**Explanation**

Service Connections provide access to external resources such as Azure subscriptions, so they require strict security controls.

**Used in Production**

Organizations limit production Service Connections to approved pipelines and authorized administrators.

**Common Mistake**

Allowing every pipeline or developer to use the Production Service Connection.

---

### Question 9

**Question**

Why is the Principle of Least Privilege important in Azure DevOps?

**Answer**

The Principle of Least Privilege means users receive only the permissions required to perform their job.

Benefits include:

- Improved security
- Reduced accidental changes
- Lower attack surface
- Better compliance
- Easier auditing

**Explanation**

Restricting permissions minimizes the impact of compromised accounts and operational mistakes.

**Used in Production**

Most enterprise DevOps teams assign Contributor access by default and reserve administrative permissions for a small number of users.

---

### Question 10

**Question**

How does Azure DevOps integrate with Microsoft Entra ID for security?

**Answer**

Azure DevOps integrates with Microsoft Entra ID to provide:

- User authentication
- Group synchronization
- Single Sign-On (SSO)
- Multi-Factor Authentication (MFA)
- Centralized identity management

**Explanation**

Organizations can manage identities centrally using Microsoft Entra ID instead of maintaining separate Azure DevOps accounts.

**Used in Production**

Enterprise organizations commonly use Microsoft Entra ID to enforce security policies across Azure DevOps.

---

### Question 11

**Question**

What are some best practices for securing Azure DevOps?

**Answer**

Best practices include:

- Apply the Principle of Least Privilege.
- Use Groups instead of assigning permissions directly to users.
- Protect important branches with Branch Policies.
- Restrict Production pipeline access.
- Limit Service Connection usage.
- Enable Multi-Factor Authentication (MFA).
- Review permissions regularly.
- Audit security changes and access logs.
- Remove inactive users promptly.

**Explanation**

Following these practices improves security, governance, and compliance while reducing operational risk.

**Used in Production**

Enterprise organizations routinely perform access reviews and permission audits.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A new developer joins your team. How would you provide the required Azure DevOps access?

**Answer**

- Add the developer to the appropriate Microsoft Entra ID or Azure DevOps security group.
- Assign the appropriate project role (for example, Contributor).
- Verify repository and pipeline access based on team requirements.

**Explanation**

Using groups ensures consistent permissions and simplifies future permission changes.

---

### Scenario 2

**Question**

A developer accidentally deletes an important branch. How could this have been prevented?

**Answer**

Implement:

- Branch Policies.
- Restrict branch deletion permissions.
- Require Pull Requests.
- Limit administrative access.
- Protect critical branches such as `main`.

**Explanation**

Repository permissions and protected branches reduce the risk of accidental code loss.

---

### Scenario 3

**Question**

A developer requests Project Administrator access because they need to create a pipeline. Would you grant it?

**Answer**

No.

Grant only the specific permissions required to create or manage pipelines, or assign an appropriate role such as Build Administrator if it aligns with organizational policy.

**Explanation**

Administrative access should not be granted when a lower-privilege role satisfies the requirement.

---

### Scenario 4

**Question**

Your Production pipeline is editable by every developer. What changes would you recommend?

**Answer**

- Restrict pipeline edit permissions.
- Allow only DevOps engineers or release administrators to modify Production pipelines.
- Enable branch protection and approval workflows.
- Audit pipeline permissions.

**Explanation**

Production deployment pipelines should be tightly controlled to reduce operational risk.

---

### Scenario 5

**Question**

A deployment to Production occurs without approval because anyone can use the Production Service Connection. How would you fix this?

**Answer**

- Restrict Service Connection permissions.
- Authorize only approved pipelines.
- Require Environment approvals.
- Limit access to deployment administrators.

**Explanation**

Production credentials should not be accessible to all users or pipelines.

---

### Scenario 6

**Question**

Your manager wants all developers to have access to every repository in the organization. Would you recommend this?

**Answer**

Generally, no.

Grant repository access based on business needs and the Principle of Least Privilege.

**Explanation**

Unrestricted repository access increases the risk of accidental or unauthorized changes and unnecessary exposure of sensitive code.

---

### Scenario 7

**Question**

An employee leaves the organization. What security actions should be taken in Azure DevOps?

**Answer**

- Remove the user from Microsoft Entra ID or Azure DevOps.
- Remove group memberships.
- Revoke pipeline permissions.
- Revoke Service Connection access.
- Review assigned work items if necessary.
- Audit recent activity.

**Explanation**

Promptly removing access reduces the risk of unauthorized use of organizational resources.

---

### Scenario 8

**Question**

Your organization wants every code change reviewed before it reaches the `main` branch. How would you implement this?

**Answer**

Configure Branch Policies that require:

- Pull Requests.
- Minimum reviewers.
- Successful build validation.
- Resolution of review comments before merge.

**Explanation**

Branch Policies improve code quality and reduce the likelihood of defective code reaching production.

---

### Scenario 9

**Question**

A developer reports "Permission Denied" when attempting to push code. How would you troubleshoot?

**Answer**

Check:

- Repository permissions.
- Group membership.
- Branch Policies.
- Repository selection.
- Project access.
- Authentication status.

**Explanation**

Permission issues often result from missing repository rights or branch restrictions.

---

### Scenario 10

**Question**

Your organization wants stronger security for Production deployments. What recommendations would you provide?

**Answer**

Recommend:

- Restrict Production pipeline permissions.
- Protect production branches.
- Limit Service Connection access.
- Require Environment approvals.
- Enable Multi-Factor Authentication (MFA).
- Apply least-privilege access.
- Perform regular permission reviews.

**Explanation**

Layered security controls reduce the risk of unauthorized production changes and improve governance.

---

### Scenario 11

**Question**

During a security audit, you discover that several users have accumulated permissions from multiple groups, giving them more access than they need. How would you address this?

**Answer**

- Review each user's effective permissions.
- Remove unnecessary group memberships.
- Consolidate permissions into role-based groups.
- Apply the Principle of Least Privilege.
- Document the changes and schedule regular access reviews.
- Verify that users retain only the permissions required for their current responsibilities.

**Explanation**

Permission accumulation (also called permission creep) is common in long-running projects. Regular audits and role-based access control help maintain a secure and manageable Azure DevOps environment while reducing the risk of excessive privileges.
