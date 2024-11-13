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


### Organizing Cloud Usage with Tags on Azure

As cloud usage grows, staying organized is essential for understanding and managing resources and costs. For example, as Tailwind Traders experiments with Azure deployments, tagging enables quick identification and cleanup of test environments.

#### Organizational Strategies
1. **Subscriptions**: Group related resources by placing them in separate subscriptions.
2. **Resource Groups**: Use resource groups to manage sets of related resources.
3. **Tags**: Tags add metadata to resources, aiding in organization and resource management.

#### Benefits of Tagging

- **Resource Management**: Tags enable you to locate and manage resources associated with specific workloads, environments, business units, and owners.
- **Cost Management & Optimization**: Tags facilitate cost reporting, budgeting, and cost forecasting.
- **Operations Management**: Tags help define service-level agreements (SLAs) by grouping resources by criticality.
- **Security**: Classify resources based on data sensitivity, such as public or confidential.
- **Governance & Compliance**: Tags help enforce regulatory compliance (e.g., ISO 27001) and internal standards.
- **Workload Optimization & Automation**: Tags allow visualization of all resources in complex deployments. They can also integrate with tools like Azure DevOps for automated tasks.

#### Managing Tags
Tags can be managed through the Azure Portal, PowerShell, Azure CLI, REST API, and Resource Manager templates. You can use Azure Policy to enforce tagging rules, ensuring resource tags align with organizational standards.

#### Example Tagging Strategy for Tailwind Traders
Tailwind Traders uses the following tags:
- **appname**: Name of the application the resource belongs to.
- **cost center**: Internal cost center code.
- **owner**: Business owner responsible for the resource.
- **environment**: Environment name, e.g., Prod, Dev, or Test.
- **impact**: Importance to business operations (e.g., mission-critical, high-impact, low-impact).

This tagging setup allows Tailwind Traders to query resources by tags (using PowerShell or Azure CLI) and manage resources based on business requirements, such as identifying all mission-critical resources.

> Note: Not all resources need every tag; for example, only mission-critical resources might have an **impact** tag.




### Ensuring Compliance with Azure Policy

To keep resources compliant with governance and business requirements, Azure Policy provides a way to enforce, audit, and manage resource configurations in Azure. Azure Policy helps organizations stay compliant by defining rules and effects to maintain configurations that align with corporate standards.

#### Key Features of Azure Policy
- **Policy Definition & Assignment**: Define rules (policy definitions) and assign them to resources within a specific scope, like a management group, subscription, or resource group. Each resource is then evaluated as compliant or non-compliant based on these policies.
- **Initiatives**: Group related policies into initiatives to track compliance with broader goals, such as enabling monitoring or adhering to regulatory standards like HIPAA or ISO 27001.

#### Azure Policy Capabilities

1. **Control & Audit**: Enforce rules like restricting certain VM sizes or requiring certain tags (e.g., “appname”) on resources.
2. **Built-In & Custom Policies**: Use built-in policies across categories (e.g., storage, compute, security) or create custom policies to fit specific requirements.
3. **Automatic Remediation**: In some cases, Azure Policy can auto-correct configurations, such as reapplying tags if removed.
4. **Integration with Azure DevOps**: Apply policies within CI/CD pipelines to ensure compliance before and after deployments.
5. **Scope & Inheritance**: Policy assignments inherit across child resources within the specified scope, ensuring uniform compliance.

#### Example Policies in Azure Policy
- **Location Restriction**: Restrict deployments to specific geographic regions to meet compliance requirements.
- **Multi-Factor Authentication (MFA)**: Enforce MFA for all privileged accounts.
- **Cross-Origin Resource Sharing (CORS)**: Control which domains can interact with your web apps for added security.
- **Azure Security Center**: Enforce monitoring and security recommendations, such as checking for unencrypted databases or missing endpoint protection.

#### Implementing Azure Policies: Steps
1. **Define**: Create policy definitions (e.g., restrict VM sizes or enforce tagging).
2. **Assign**: Assign these definitions to resources within a specific scope.
3. **Evaluate & Review**: Azure evaluates resources against the policy every hour, marking them as compliant or non-compliant.

#### Initiatives & Assignments
Azure Policy’s **Initiatives** allow grouping multiple policies under a single goal, simplifying compliance tracking for broader objectives. Built-in initiatives include examples like “Enable Monitoring in Azure Security Center,” with policies to monitor encryption, OS vulnerabilities, and endpoint protection across resources.

Azure policies and initiatives can be defined and assigned through the Azure portal, CLI, or custom scripts. Initiatives allow flexibility, as you can add or remove policies over time without needing to re-assign them to resources.

> **Example**: Tailwind Traders could use an initiative for **Security Compliance**, covering all resources with policies related to encryption, authentication, and security baselines.






### Scaling Governance Across Subscriptions with Azure Blueprints

As cloud environments expand beyond a single Azure subscription, configuring policies and managing compliance consistently can become complex. **Azure Blueprints** offers a solution by allowing you to create and deploy repeatable governance configurations and resources across multiple subscriptions. This enables development teams to build compliant environments rapidly while ensuring adherence to organizational standards.

#### Key Features of Azure Blueprints

1. **Standardized Deployments**: Define a set of governance and resource configurations that can be consistently deployed across new and existing subscriptions.
2. **Blueprint Artifacts**: Each blueprint consists of various artifacts, such as policy assignments, role assignments, Azure Resource Manager (ARM) templates, and resource groups, allowing a comprehensive deployment of resources and policies.
3. **Versioning and Tracking**: Blueprint versions allow administrators to track changes, helping audit deployments and adjust configurations as standards evolve.
4. **Parameter Flexibility**: Blueprint artifacts can include parameters, like allowed locations, that can be set when creating or assigning blueprints. This enables you to maintain a single blueprint while customizing it for different deployment scopes.

#### Steps to Implement an Azure Blueprint

1. **Create the Blueprint Definition**: Define the blueprint, including all necessary artifacts (policies, role assignments, ARM templates, etc.).
2. **Assign the Blueprint**: Assign the blueprint to a specific scope, such as a management group or subscription, to automatically deploy resources.
3. **Track and Manage Assignments**: Azure tracks the relationship between the blueprint definition and the resources deployed, preserving an audit trail.

#### Example Use Case: ISO 27001 Compliance with Azure Blueprints

Suppose **Tailwind Traders** wants to comply with the ISO 27001 standard, which provides guidelines for IT system security. Azure Blueprints includes several pre-built blueprint templates for ISO 27001. By following these steps, Tailwind Traders can apply an ISO 27001-compliant blueprint across its subscriptions:

1. **Create a Management Group**: Establish a management group, such as `prod MG`, to manage compliance for multiple subscriptions.
2. **Define the Blueprint**: Use the ISO 27001 shared services blueprint template, customizing it as needed, and publish the blueprint.
3. **Assign to Management Group**: Assign the blueprint to `prod MG`, ensuring that all subscriptions under this group inherit the compliance settings.

When new subscriptions are added to `prod MG`, the ISO 27001 blueprint will automatically deploy its configurations, keeping new resources compliant. This approach simplifies governance, reduces the need for manual configurations, and ensures compliance standards are met consistently.

#### Benefits of Using Azure Blueprints

- **Consistency Across Subscriptions**: Blueprints enforce standardized configurations across all subscriptions in a management group.
- **Efficient Scaling**: Automatically apply compliance settings to new subscriptions.
- **Audit and Compliance Tracking**: With versioning and assignment tracking, administrators can audit deployments and make informed adjustments over time.

By implementing Azure Blueprints, Tailwind Traders can ensure governance and compliance on a larger scale, making it an effective tool for organizations expanding their Azure environment across multiple subscriptions.







