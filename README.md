# The Permission Sprawl | IAM Access Governance at Northwind Health

*A fictional healthcare SaaS scenario focused on Role-Based Access Control (RBAC), least privilege, segregation of duties (SoD), and Privileged Identity Management (PIM).*

---

## 1. Overview

Northwind Health is a fictional healthcare SaaS company with approximately 120 employees, supporting 400 clinics and handling electronic protected health information (ePHI).

The Billing department has accumulated individual permission grants over time. As a result, employees performing similar jobs have inconsistent access, and several users hold permissions beyond their business responsibilities.

**My assignment:** Review the current access, design appropriate roles, identify incompatible permissions, recommend access removals, and propose a safe transition to a more manageable access model.

**Objective:** Reduce excessive permissions, improve access governance and maintain business operations throughout the transition.

## 2. Scope

The review covers:

- Six employees across four job roles.
- Seven application permissions.
- Role-Based Access Control (RBAC) and security-group design.
- Least privilege and segregation of duties.
- Individual access findings and remediation priorities.
- A three-step rollout plan.
- Temporary privileged access using PIM and Just-in-Time (JIT) controls.

**Scope limitation:** This is a design and access-review exercise. No live application permissions were changed.

## 3. Current Access Matrix

The following table shows the permissions currently assigned to each employee.

**Legend:** ✓ Granted | — Not granted

| Employee | Create invoices | Approve refunds | Edit patient billing details | Create new payee | Approve payments | Export all billing data | System admin |
| -------- | --------------- | --------------- | ---------------------------- | ---------------- | ---------------- | ----------------------- | ------------ |
| Ana      | ✓               | —               | ✓                            | —                | —                | ✓                       | —            |
| Ben      | ✓               | ✓               | ✓                            | ✓                | —                | —                       | —            |
| Chloe    | ✓               | —               | ✓                            | —                | —                | —                       | —            |
| Dev      | ✓               | ✓               | ✓                            | ✓                | ✓                | ✓                       | —            |
| Erin     | —               | ✓               | —                            | —                | ✓                | ✓                       | —            |
| Fraser   | ✓               | ✓               | ✓                            | ✓                | ✓                | ✓                       | ✓            |

### Initial observations

- **Ana** has unnecessary access to export all billing data.
- **Ben** can approve refunds and create payees despite being a Billing Clerk.
- **Chloe** has access consistent with the Billing Clerk role.
- **Dev** has payment approval, payee creation and bulk data export permissions beyond the Billing Supervisor role.
- **Erin** can approve refunds even though that permission is not part of the stated Finance Manager responsibilities.
- **Fraser** has all seven permissions, including financial transaction functions and system administration.

**Highest-risk finding:** Fraser's excessive access creates multiple opportunities for misuse or account compromise.

## 4. Proposed RBAC and Security-Group Design

I recommend replacing individual permission assignments with **Role-Based Access Control (RBAC)**, implemented through security groups aligned with job responsibilities.

Instead of granting permissions separately to each employee, permissions would be assigned to the appropriate role group. Users would receive access through their approved group membership.

### Proposed role matrix

| Role / Security Group | Create invoices | Approve refunds | Edit patient billing details | Create new payee | Approve payments | Export all billing data | System admin |
| --------------------- | --------------- | --------------- | ---------------------------- | ---------------- | ---------------- | ----------------------- | ------------ |
| Billing Clerk         | ✓               | —               | ✓                            | —                | —                | —                       | —            |
| Billing Supervisor    | ✓               | ✓               | ✓                            | —                | —                | —                       | —            |
| Finance Manager       | —               | —               | —                            | —                | ✓                | ✓                       | —            |
| IT Support            | —               | —               | —                            | —                | —                | —                       | Restricted\* |

*System administration must be limited to appropriate technical functions. Whether Northwind's application supports that separation needs to be verified.*

### Proposed group membership

| Security Group     | Members         |
| ------------------ | --------------- |
| Billing Clerk      | Ana, Ben, Chloe |
| Billing Supervisor | Dev             |
| Finance Manager    | Erin            |
| IT Support         | Fraser          |

### Unassigned permission: Create new payee

None of the supplied job descriptions identifies responsibility for creating new payees.

Rather than assigning this permission by assumption, I would remove existing unauthorised grants and confirm the appropriate payee-management process with the Finance owner.

The final design should separate payee creation from payment approval.

### Benefits of the proposed design

- More consistent permissions for employees performing the same role.
- Easier onboarding, role changes and offboarding.
- Reduced reliance on individual permission grants.
- Clearer access ownership and easier periodic reviews.
- Better enforcement of least privilege.

## 5. Segregation of Duties (SoD)

Segregation of duties helps prevent one person from controlling incompatible stages of a sensitive business process.

| Permission combination                          | Potential risk                                                                                       | Recommended control                                               |
| ----------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| Create new payee + approve payments             | An employee could create a fraudulent recipient and authorise a payment                              | Separate payee management and payment approval                    |
| System administration + financial approvals     | A privileged user could potentially modify access or system settings and authorise financial actions | Separate technical administration from financial responsibilities |
| Edit billing details + approve a related refund | A user could change a billing record and approve a refund involving that change                      | Require independent review for relevant transactions              |

**Important distinction:** The Billing Supervisor legitimately needs both billing-detail editing and refund approval. The proposed safeguard is independent review of relevant transactions, not removal of permissions required by the role.

The precise refund workflow would need to be confirmed before implementing transaction-level restrictions.

## 6. Excessive Access Findings

The following removals would bring each employee's permissions into alignment with the proposed role design.

| Employee | Role               | Permissions to remove                                                                                                       | Priority  |
| -------- | ------------------ | --------------------------------------------------------------------------------------------------------------------------- | --------- |
| Ana      | Billing Clerk      | Export all billing data                                                                                                     | Medium    |
| Ben      | Billing Clerk      | Approve refunds; create new payee                                                                                           | High      |
| Chloe    | Billing Clerk      | None                                                                                                                        | No change |
| Dev      | Billing Supervisor | Create new payee; approve payments; export all billing data                                                                 | High      |
| Erin     | Finance Manager    | Approve refunds                                                                                                             | Medium    |
| Fraser   | IT Support         | Create invoices; approve refunds; edit patient billing details; create new payee; approve payments; export all billing data | Critical  |

*Priorities are proposed qualitative assessments based on the scenario, not scores from a validated organisational risk methodology.*

### Highest-priority finding: Fraser

Fraser is assigned to IT Support, but currently holds all seven permissions.

This includes the ability to create payees, approve payments, approve refunds, export sensitive billing information and administer the system.

The combination creates significant risk because technical administration and financial responsibilities are not separated.

**Recommended action:** Remove all six billing and financial permissions, review the scope of system administration, and provide controlled temporary elevation for legitimate technical support tasks.

## 7. Three-Step Remediation and Rollout Plan

### Step 1: Validate and approve

- Confirm job responsibilities with Billing, Finance and IT managers.
- Review the proposed permission matrix against company policy.
- Identify the authorised owner of payee creation.
- Verify what the existing System Admin permission actually allows.
- Record current access and prepare a rollback plan.

### Step 2: Test and migrate

- Configure the proposed security groups and role permissions.
- Test that users can complete their required business tasks.
- Verify that unnecessary or conflicting access is blocked.
- Pilot the changes before wider deployment.
- Remove legacy individual permission grants during migration.

**Important:** Assigning a user to a new security group does not automatically remove permissions they still hold through direct grants or other group memberships.

### Step 3: Verify and monitor

- Confirm effective permissions after migration.
- Check that Billing and Finance operations continue normally.
- Review relevant logs and access-related issues.
- Correct role-design problems through approved changes.
- Schedule periodic access reviews to prevent permission sprawl from returning.

Urgent high-risk access should be prioritised while maintaining appropriate change control.

## 8. Privileged Access: PIM and JIT

IT Support needs to maintain the application and troubleshoot faults, but this does not justify permanent financial transaction permissions.

I propose using **Privileged Identity Management (PIM)** with **Just-in-Time (JIT) access** where supported.

### Proposed process

1. Fraser uses a standard account for everyday work.
2. A support issue identifies the technical access required.
3. An authorised approver reviews the request.
4. Temporary administrative privileges are activated for the approved task and duration.
5. Access expires automatically, and the activity is logged for review.

This would allow Fraser to perform legitimate support work without retaining permanent financial permissions.

**Implementation consideration:** Northwind's technical capabilities are not specified. If the application cannot separate administration from financial functions, this would require further investigation and compensating controls rather than assuming PIM alone resolves the conflict.

## 9. Expected Security Improvements

If the recommendations are approved and implemented, the expected outcomes would include:

| Area                   | Expected improvement                                                |
| ---------------------- | ------------------------------------------------------------------- |
| Least privilege        | Employees retain only permissions needed for their responsibilities |
| Access consistency     | Users in equivalent roles receive consistent access                 |
| Administration         | Security groups simplify permission management                      |
| Segregation of duties  | Incompatible financial responsibilities are separated               |
| Privileged access      | Technical elevation is controlled and time-limited                  |
| Audit readiness        | Role ownership, permissions and changes are easier to review        |
| Operational continuity | Testing and phased migration reduce disruption risk                 |

These are **expected outcomes**, not measured results from a live deployment.

## 10. Project Documentation

The supporting case-study documents will provide the detailed analysis behind this overview.

| Document                               | Focus                                                           |
| -------------------------------------- | --------------------------------------------------------------- |
| 01 — Scenario and Scope                | Business context, responsibilities, assumptions and constraints |
| 02 — Current Access and RBAC Design    | Existing permissions, proposed roles and security groups        |
| 03 — Segregation of Duties             | Incompatible permissions and proposed safeguards                |
| 04 — Access Findings and Risk Register | Individual findings, risk ratings and remediation priorities    |
| 05 — Remediation and Rollout           | Testing, migration, legacy grant removal and verification       |
| 06 — PIM and JIT Access                | Temporary privileged access and technical limitations           |
| 07 — Executive Summary                 | Management-level summary of risks and recommendations           |

Additional CSV evidence will include the current access matrix, proposed role matrix and individual remediation actions.

## 11. What I Learned

The most challenging part was understanding what IT Support genuinely needs.

I initially thought Fraser might need billing permissions to troubleshoot problems, but I realised there is a difference between supporting a system and performing its business tasks.

This exercise also helped me connect RBAC with security groups, understand why legacy permission grants must be removed during migration, and explore how PIM and JIT can reduce permanent privileged access.

---

**Related IAM case study:** [User Access Review | Northwind Health](https://github.com/itsanitarose/IAM-Access-Review)
