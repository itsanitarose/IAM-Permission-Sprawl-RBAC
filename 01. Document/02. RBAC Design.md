# 02 — Current Access and RBAC Design

**Project:** Northwind Health | IAM Permission Sprawl & RBAC Design

---

## 1. Access Review Overview

The assessment compares the permissions currently assigned to six Northwind Health employees against their documented job responsibilities.

The objective is to identify inconsistent and excessive access, then design a Role-Based Access Control (RBAC) model that assigns permissions according to business need rather than individual access requests.

## 2. Current Access Matrix

The existing permissions are shown below.

**Legend:** ✓ = Access granted | — = Access not granted

| Employee | Job Role           | Create invoices | Approve refunds | Edit patient billing details | Create new payee | Approve payments | Export all billing data | System admin |
| -------- | ------------------ | --------------- | --------------- | ---------------------------- | ---------------- | ---------------- | ----------------------- | ------------ |
| Ana      | Billing Clerk      | ✓               | —               | ✓                            | —                | —                | ✓                       | —            |
| Ben      | Billing Clerk      | ✓               | ✓               | ✓                            | ✓                | —                | —                       | —            |
| Chloe    | Billing Clerk      | ✓               | —               | ✓                            | —                | —                | —                       | —            |
| Dev      | Billing Supervisor | ✓               | ✓               | ✓                            | ✓                | ✓                | ✓                       | —            |
| Erin     | Finance Manager    | —               | ✓               | —                            | —                | ✓                | ✓                       | —            |
| Fraser   | IT Support         | ✓               | ✓               | ✓                            | ✓                | ✓                | ✓                       | ✓            |

The matrix shows that employees in the same job role do not always have consistent permissions.

For example, Ana, Ben and Chloe are all Billing Clerks, but Ana can export billing data, Ben can approve refunds and create payees, and Chloe holds only the permissions required for her role.

Fraser has the broadest access, with all seven permissions assigned despite having no financial responsibilities.

## 3. Proposed RBAC Model

I recommend replacing individual permission assignments with security groups based on approved job responsibilities.

Under the proposed model, permissions would be assigned to security groups, and employees would receive access through membership of the appropriate group.

### Proposed Role-Permission Matrix

**Legend:** ✓ = Proposed access | — = No proposed access | \* = Requires technical validation

| Security Group     | Create invoices | Approve refunds | Edit patient billing details | Create new payee | Approve payments | Export all billing data | System admin |
| ------------------ | --------------- | --------------- | ---------------------------- | ---------------- | ---------------- | ----------------------- | ------------ |
| Billing Clerk      | ✓               | —               | ✓                            | —                | —                | —                       | —            |
| Billing Supervisor | ✓               | ✓               | ✓                            | —                | —                | —                       | —            |
| Finance Manager    | —               | —               | —                            | —                | ✓                | ✓                       | —            |
| IT Support         | —               | —               | —                            | —                | —                | —                       | \*           |

**IT Support:** Technical administration should be restricted to the capabilities necessary for system maintenance and troubleshooting. The existing System Admin permission must be reviewed before deciding whether it can be safely assigned or requires a more limited administrative role.

### Proposed Security-Group Membership

| Security Group     | Employees       |
| ------------------ | --------------- |
| Billing Clerk      | Ana, Ben, Chloe |
| Billing Supervisor | Dev             |
| Finance Manager    | Erin            |
| IT Support         | Fraser          |

The Billing Supervisor group includes the permissions required by a Billing Clerk, plus refund approval.

This role-based approach would make access more consistent and easier to manage when employees join, change roles or leave the organisation.

## 4. Permission Gap Analysis

Comparing current permissions against the proposed roles identifies the following differences.

| Employee | Permissions outside stated job responsibilities                                                                             |
| -------- | --------------------------------------------------------------------------------------------------------------------------- |
| Ana      | Export all billing data                                                                                                     |
| Ben      | Approve refunds; create new payee                                                                                           |
| Chloe    | None identified                                                                                                             |
| Dev      | Create new payee; approve payments; export all billing data                                                                 |
| Erin     | Approve refunds                                                                                                             |
| Fraser   | Create invoices; approve refunds; edit patient billing details; create new payee; approve payments; export all billing data |

Fraser's System Admin access is not included in the removal list because technical administration may be necessary for his role. However, its scope and whether it should be permanently assigned require further review.

These differences form the basis of the risk assessment and individual findings documented in [**Document 04 — Access Findings and Risk Register**](04-Access-Findings-and-Risk-Register.md).

## 5. Unassigned Permission: Create New Payee

The permission to create new payees is not included in any of the supplied job descriptions.

Ben, Dev and Fraser currently hold this permission, but their stated responsibilities do not justify it.

I would recommend removing these grants after confirming the appropriate payee-management process with Finance.

Before assigning the permission to an authorised role, the organisation should establish clear ownership and ensure that payee creation is separated from payment approval.

## 6. RBAC Implementation Considerations

Introducing security groups alone would not guarantee that excessive access had been removed.

The transition would also need to address:

- **Direct permission grants:** Remove legacy permissions assigned individually to users.
- **Inherited access:** Check whether other group memberships continue to grant unnecessary permissions.
- **Role validation:** Test that each group can perform its authorised tasks and cannot perform restricted actions.
- **Business approval:** Confirm the proposed roles and permissions with the relevant managers.
- **Effective access:** Verify each employee's final permissions after migration.




