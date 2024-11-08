## Accelerate Your Cloud Adoption Journey by Using the Cloud Adoption Framework for Azure

### The Cloud Adoption Framework

**Purpose**: The framework offers guidance for cloud adoption and implementing business and technology strategies.

### Stages of the Cloud Adoption Framework

1. **Define Strategy**: 
   - Establish motivations, business outcomes, and develop a business case for cloud adoption.

2. **Build a Plan**: 
   - Map goals to specific actions, inventory digital assets, align teams, and create a skills readiness plan.

3. **Ready the Organization**: 
   - Create a landing zone, set up Azure subscriptions, and refine infrastructure, governance, and security.

4. **Adopt the Cloud**: 
   - Migrate applications, modernize solutions, follow best practices, and ensure business value.

5. **Govern and Manage**: 
   - Develop governance strategies, iteratively improve policies, establish management baselines, and review for resilience.

### Continuous Improvement and Adaptation

- Cloud governance evolves as the environment changes; ensure ongoing resilience and optimization across all cloud assets.

---

## Governance in Azure

Governance refers to the set of policies, processes, and tools that ensure an organization’s resources in the cloud are used responsibly, securely, and in a way that aligns with the organization’s goals, compliance standards, and operational requirements.

### Breakdown of Governance:

- **Access Control**: Defining who has permission to access specific resources, ensuring that only authorized users can manage or view critical data or applications.

- **Policy Enforcement**: Creating policies that define acceptable configurations or standards for resources. For instance, setting policies to require data encryption, specify which regions resources can be deployed in, or enforce tagging for cost management.

- **Cost Management**: Organizing resources to control and monitor costs, using tools like billing reports, chargebacks, and budget limits to manage expenditures.

- **Compliance and Security**: Ensuring cloud resources meet regulatory requirements (e.g., PCI DSS for payment data security) and follow best practices for security. Governance includes applying policies that enforce these requirements across all resources.

- **Resource Management**: Using organizational structures like resource groups, subscriptions, and management groups to control resource allocation, set limits, and organize assets according to the organization’s needs.

- **Operational Efficiency**: Ensuring resources are configured optimally for performance, scalability, and maintenance, which also includes managing limits and ensuring resources are deployed in the right environments (e.g., development, production).

In essence, governance in the cloud is about creating a framework that ensures resources are used in a way that is secure, cost-effective, compliant, and aligned with business objectives.

---

## Hierarchical Structure in Azure

- **Resources**: Instances of Azure services (e.g., VMs, databases).
- **Resource Groups**: Logical containers grouping related resources for easier deployment and management.
- **Subscriptions**: Group resources and user accounts, enforce quotas, and manage costs by department, team, or project.
- **Management Groups**: Enforce policies, access control, and compliance across multiple subscriptions; conditions apply to all nested subscriptions.

### Cloud Governance Setup:

- Form a Cloud Center of Excellence or Enablement Team to centralize governance practices across the organization.
- Start governance at the Subscription Level.

### Subscription Management:

- **Billing**: Each subscription has a billing report; use separate subscriptions for departments/projects to track costs, or apply resource tags.
- **Access Control**: Role-based access control via Azure AD, which allows administrators to assign roles and permissions within subscription boundaries.
- **Limits and Quotas**: Subscriptions have defined resource limits (e.g., 10 ExpressRoute circuits per subscription). Plan to create additional subscriptions if limits are reached.

### Using Management Groups:

- Simplify management of access, policies, and compliance across subscriptions through Management Groups.
- Subscriptions within a management group inherit policies automatically, supporting consistent governance across your Azure environment.

---

## Azure Role-Based Access Control (RBAC)

### Need for Access Control

In Azure, controlling access to resources is essential, especially in environments with multiple IT and engineering teams.

**Principle of Least Privilege**: Grant users only the access they need to perform their tasks.

### Azure Role-Based Access Control (RBAC):

Azure simplifies access control by assigning roles to users, groups, or applications at different scopes.

- **Roles**: Define what actions can be performed on Azure resources. Examples include:
  - **Reader**: View resources without making changes.
  - **Contributor**: Manage all resources without assigning roles.
  - **Owner**: Full access, including role assignment capabilities.

- **Scopes**: The level at which permissions apply, organized hierarchically:
  - Management Group (broadest level)
  - Subscription
  - Resource Group
  - Resource (most specific level)

- **Custom Roles**: Organizations can create custom roles if the built-in roles don’t meet specific needs.

### Role Assignments:

- Attach roles to Security Principals (users, groups, applications, or managed identities) at specific scopes.
- **Allow Model**: Roles are cumulative, meaning users inherit all permissions granted through multiple role assignments.

### Enforcing RBAC via Azure Resource Manager:

- RBAC permissions are enforced on actions going through the Azure Resource Manager, which secures and organizes Azure resources.
- Azure RBAC applies only at the resource level; applications still need to handle their own security for data-level access.

### RBAC Scenarios:

- Control resource access based on team functions. Examples include:
  - Allow one user to manage virtual machines and another to manage virtual networks within the same subscription.
  - Permit a Database Administrator group to manage SQL databases.
  - Allow an application to manage all resources within a specific resource group.

### Managing Access Permissions:

- The **Access Control (IAM)** Pane in the Azure portal shows who has access to a resource, their role, and their scope.
- Role assignments can be added or removed here to manage access efficiently.

By using Azure RBAC, organizations like Tailwind Traders can assign roles based on job functions for teams such as IT Administrators (full control), Backup and Disaster Recovery (backup operations), Cost and Billing (budget management), and Security Operations (monitoring and responding to incidents). This enables fine-grained control over access and helps protect Azure resources from unauthorized actions.

---

## Azure Resource Locking: An Added Layer of Access Control

### Purpose of Azure Resource Locking:

Resource Locks add an extra layer of security to prevent accidental deletion or modification of critical resources, even by users with necessary Azure RBAC permissions.

**Scenario Example**: At Tailwind Traders, an IT Administrator accidentally deleted critical resources during routine cleanup. A resource lock could prevent such accidents by warning that the resource should not be altered or removed.

### Applying Resource Locks:

- **Lock Levels**:
  - **Cannot Delete**: Users can modify and read the resource but cannot delete it without removing the lock.
  - **Read-Only**: Users can read the resource but cannot modify or delete it, similar to permissions in the **Reader** role.

- **Where to Apply Locks**:
  - Resource locks can be applied at various levels—subscriptions, resource groups, or individual resources.

- **Managing Locks**:
  - Locks can be added or removed through the Azure portal, PowerShell, Azure CLI, or Azure Resource Manager templates.

### Enforcement and Modification:

- **Protection Mechanism**: A locked resource requires the lock to be removed before any restricted actions (like delete) can be performed, providing a safety checkpoint.
- **Lock Removal Requirement**: Even resource owners must remove the lock to execute restricted actions, ensuring intentionality.

### Enhancing Protection with Azure Blueprints:

- **Azure Blueprints**: Define and enforce resource standards within an organization.
- **Blueprint-Defined Locks**: Azure blueprints can specify required locks for resources. If a lock is deleted, the blueprint can automatically reapply it, providing continuous protection.

Azure resource locking combined with Azure RBAC enables a secure, controlled environment where even administrative actions require intentional oversight, reducing the risk of accidental deletion or modification of essential resources.
