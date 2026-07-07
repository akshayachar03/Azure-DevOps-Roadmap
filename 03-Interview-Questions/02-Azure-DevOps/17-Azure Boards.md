# Azure DevOps Boards Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Azure Boards?

**Answer**

Azure Boards is the work management service in Azure DevOps used to plan, track, and manage software development work.

It provides features such as:

- Work Items
- Backlogs
- Boards (Kanban)
- Sprints
- Epics
- Features
- User Stories
- Tasks
- Dashboards
- Queries

**Explanation**

Azure Boards helps Agile teams organize and monitor work throughout the software development lifecycle.

**Used in Production**

Organizations use Azure Boards to manage product backlogs, sprint planning, bug tracking, and project progress.

**Common Mistake**

Many candidates think Azure Boards is only a ticketing system. It is a complete Agile project management solution.

---

### Question 2

**Question**

What are Work Items in Azure Boards?

**Answer**

A Work Item is a record used to track work throughout a project.

Common Work Item types include:

- Epic
- Feature
- User Story
- Task
- Bug
- Issue

Each Work Item contains:

- Title
- Description
- Assigned User
- Priority
- State
- Tags
- Comments
- History

**Explanation**

Every piece of work in Azure Boards is represented as a Work Item.

**Used in Production**

Development teams use Work Items to track features, bugs, technical tasks, and project activities.

---

### Question 3

**Question**

What is an Epic?

**Answer**

An Epic is a large business objective that requires multiple Features and User Stories to complete.

Example:

```text
Online Shopping Platform
```

Possible Features:

- User Authentication
- Product Catalog
- Shopping Cart
- Payment System

**Explanation**

Epics represent high-level business goals and are broken down into smaller deliverables.

**Used in Production**

Product Managers typically create Epics during release planning.

**Common Mistake**

Confusing an Epic with a User Story. An Epic is much larger and usually spans multiple sprints.

---

### Question 4

**Question**

What is a Feature?

**Answer**

A Feature is a significant functionality that delivers business value and belongs to an Epic.

Example:

Epic:

```text
Online Shopping Platform
```

Feature:

```text
Shopping Cart
```

User Stories:

- Add Item
- Remove Item
- Update Quantity

**Explanation**

Features organize related User Stories into functional areas.

**Used in Production**

Development teams often complete Features over one or more sprints.

---

### Question 5

**Question**

What is a User Story?

**Answer**

A User Story describes a user requirement from the customer's perspective.

Format:

> As a **user**, I want **to add products to my cart**, so that **I can purchase multiple items together.**

**Explanation**

User Stories define what the application should accomplish from the end user's perspective.

**Used in Production**

Most Agile development teams plan and estimate work using User Stories.

**Common Mistake**

Writing User Stories as technical implementation tasks instead of user-focused requirements.

---

### Question 6

**Question**

What is a Task in Azure Boards?

**Answer**

A Task represents a technical activity required to complete a User Story.

Example:

User Story:

```text
User Login
```

Tasks:

- Create Login API
- Design Login Page
- Validate Credentials
- Write Unit Tests

**Explanation**

Tasks help developers break User Stories into manageable implementation work.

**Used in Production**

Developers assign and track Tasks during sprint execution.

---

### Question 7

**Question**

What is a Backlog?

**Answer**

A Backlog is an ordered list of pending work items waiting to be completed.

It may contain:

- Epics
- Features
- User Stories
- Bugs

**Explanation**

The Product Owner prioritizes the Backlog so the team always works on the highest-value items first.

**Used in Production**

Backlogs are reviewed regularly during backlog refinement sessions.

---

### Question 8

**Question**

What are Boards in Azure DevOps?

**Answer**

Boards provide a Kanban-style visual representation of Work Items.

Typical columns include:

```text
New
↓

Active
↓

Resolved
↓

Closed
```

**Explanation**

Boards allow teams to visualize work progress and identify bottlenecks.

**Used in Production**

Kanban Boards are commonly used for Agile and DevOps workflows.

---

### Question 9

**Question**

What are Sprints?

**Answer**

A Sprint is a fixed time period during which a team completes a selected set of work items.

Typical Sprint duration:

- 1 week
- 2 weeks
- 3 weeks
- 4 weeks

Activities include:

- Sprint Planning
- Daily Stand-up
- Development
- Testing
- Sprint Review
- Sprint Retrospective

**Explanation**

Sprints help teams deliver software in small, predictable increments.

**Used in Production**

Most Scrum teams use two-week sprints.

---

### Question 10

**Question**

What is the relationship between Epics, Features, User Stories, and Tasks?

**Answer**

Hierarchy:

```text
Epic
   │
   ▼
Feature
   │
   ▼
User Story
   │
   ▼
Task
```

Example:

```text
Epic
Online Banking

    │

Feature
Fund Transfer

    │

User Story
Transfer Money

    │

Tasks
Create API
Validate Account
Write Tests
Deploy
```

**Explanation**

Breaking work into smaller levels improves planning, estimation, and tracking.

**Used in Production**

Most Agile organizations organize work using this hierarchy.

---

### Question 11

**Question**

What are some best practices for managing Azure Boards?

**Answer**

Best practices include:

- Create meaningful User Stories.
- Break large Epics into Features.
- Keep Tasks small and manageable.
- Prioritize the Product Backlog regularly.
- Update Work Item status daily.
- Use Sprint Planning effectively.
- Link related Work Items.
- Monitor progress using Boards and Dashboards.

**Explanation**

Following these practices improves visibility, collaboration, and delivery predictability.

**Used in Production**

Agile teams routinely refine their backlog and update Boards throughout each sprint.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your Product Owner asks the team to implement an entire e-commerce website as one User Story. Would you recommend this?

**Answer**

No.

Create:

- One Epic
- Multiple Features
- Multiple User Stories
- Individual Tasks

**Explanation**

Large requirements should be decomposed into manageable work items that can be estimated, developed, and tested effectively.

---

### Scenario 2

**Question**

Your Sprint contains 40 User Stories, but the team consistently completes only 20. What would you recommend?

**Answer**

- Improve Sprint Planning.
- Estimate work more accurately.
- Reduce Sprint scope.
- Review team velocity.
- Prioritize high-value work.

**Explanation**

Sprint commitments should align with the team's historical delivery capacity.

---

### Scenario 3

**Question**

Several developers are working on the same Feature. How would you organize the work?

**Answer**

Create:

- One Feature.
- Multiple User Stories.
- Separate Tasks for each developer.

**Explanation**

Breaking work into smaller units enables parallel development and easier progress tracking.

---

### Scenario 4

**Question**

Your Board shows many Work Items stuck in the "Active" column for several days. What would you investigate?

**Answer**

Check:

- Workload distribution.
- Blocking issues.
- Code review delays.
- Testing bottlenecks.
- Resource availability.
- Priority changes.

**Explanation**

Items remaining in one stage for extended periods often indicate workflow bottlenecks.

---

### Scenario 5

**Question**

A developer closes a User Story even though testing has not started. Is this a good practice?

**Answer**

No.

A User Story should only be completed after development, testing, and acceptance criteria have been successfully satisfied according to the team's Definition of Done.

**Explanation**

Closing work prematurely reduces visibility and may result in incomplete features reaching production.

---

### Scenario 6

**Question**

Your manager wants to know which Features belong to a specific Epic. How would Azure Boards help?

**Answer**

Use parent-child relationships between:

- Epic
- Feature
- User Story
- Task

Azure Boards automatically displays the work item hierarchy.

**Explanation**

Hierarchical work item relationships improve traceability and reporting.

---

### Scenario 7

**Question**

A critical production bug is reported during an active Sprint. How would you handle it?

**Answer**

- Create a Bug Work Item.
- Assess its priority.
- If critical, reprioritize the Sprint with approval from the Product Owner.
- Assign the bug to the appropriate developer.
- Track it through the Board until resolved.

**Explanation**

Critical production issues may require Sprint adjustments to protect business operations.

---

### Scenario 8

**Question**

Your Product Backlog contains hundreds of outdated User Stories. What would you recommend?

**Answer**

Conduct regular backlog refinement to:

- Remove obsolete items.
- Merge duplicates.
- Reprioritize work.
- Clarify requirements.
- Split oversized stories.

**Explanation**

A well-maintained backlog improves planning and ensures the team focuses on valuable work.

---

### Scenario 9

**Question**

The team wants to know what work will be completed during the next two weeks. Which Azure Boards feature would you use?

**Answer**

Use **Sprint Planning** to assign prioritized User Stories and Tasks to the upcoming Sprint.

**Explanation**

Sprint Planning defines the work the team commits to delivering during the Sprint.

---

### Scenario 10

**Question**

Several User Stories depend on another team's work. How would you track this?

**Answer**

- Link related Work Items.
- Add dependency relationships.
- Track blockers using Boards.
- Monitor progress during Daily Stand-ups.
- Coordinate with the dependent team.

**Explanation**

Tracking dependencies improves visibility and helps identify delivery risks early.

---

### Scenario 11

**Question**

At the end of a Sprint, several Tasks are complete, but the User Story is still not fully tested. Should the User Story be marked as Done?

**Answer**

No.

The User Story should remain incomplete until all associated Tasks are finished, testing is complete, acceptance criteria are met, and the team's Definition of Done has been satisfied.

**Explanation**

In Agile, completing individual Tasks does not mean the User Story is complete. The entire feature must meet business and quality expectations before it is considered done.
