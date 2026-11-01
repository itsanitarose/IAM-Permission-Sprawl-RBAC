# 05 — Remediation and Preventive Controls

**Project:** Northwind Health | IAM Permission Sprawl & RBAC Design

---

## 1. Remediation Objectives

The remediation plan aims to remove excessive permissions, resolve segregation-of-duties conflicts and transition employees to the proposed Role-Based Access Control (RBAC) model.

The approach prioritises high-risk access while maintaining the billing and finance functions employees need to perform their jobs.

The findings and recommended access changes are documented in [**Document 04 — Access Findings and Risk Register**](04-Access-Findings-and-Risk-Register.md).


## 2. RBAC Implementation Plan

### Phase 1 — Validate and Prepare

Confirm the proposed job roles, required permissions and security-group memberships with the relevant managers.

Review the scope of System Admin access, identify the appropriate owner for payee creation and document any dependencies that could affect business operations.

Establish an approved change plan, including a rollback procedure.

### Phase 2 — Configure and Migrate

Create the proposed RBAC security groups and assign permissions according to the approved role-permission matrix.

Test each group to confirm that authorised tasks work and restricted actions are blocked.

Pilot the changes with selected users before migrating the remaining employees.

Remove legacy direct permission grants and unnecessary inherited access to prevent users from retaining privileges outside their assigned roles.

### Phase 3 — Verify and Monitor

Verify each employee's effective permissions after migration.

Confirm that billing, refund and payment workflows continue to function as intended.

Review relevant access and administrative activity logs, investigate unexpected access and arrange periodic access recertification.

## 3. Segregation-of-Duties Controls

| Control | Recommended Implementation |
|---|---|
| Payee Creation and Payment Approval | Assign these functions to separate authorised roles and prevent the same user from completing both stages |
| Refund Approval | Require appropriate supervisory approval and independent review where the same employee has modified related billing information |
| Technical Administration | Separate system maintenance privileges from billing and financial transaction permissions |
| Bulk Data Export | Restrict export permissions to approved reporting responsibilities and monitor their use |

The payee-creation permission should remain unassigned in the proposed RBAC model until Finance confirms the responsible role and approval process.

## 4. Privileged Access Management — PIM/JIT

Fraser's account presents the highest-priority finding because it combines System Admin access with all six billing and financial permissions.

I recommend a Privileged Identity Management (PIM) or Just-in-Time (JIT) access model for technical administration, where supported by the application and identity platform.

Under this approach:

- Fraser would use a standard account for routine work.
- Administrative privileges would be activated only when required for an approved technical task.
- Elevation would be limited to the necessary permissions and duration.
- Privileged access would expire automatically after the approved period.
- Multifactor authentication, approval requirements and audit logging would protect privileged activation where supported.

**PIM/JIT does not replace permission separation.** Fraser's financial permissions must still be removed, and the scope of administrative access must be validated to ensure it cannot bypass financial controls.

## 5. Preventive IAM Controls

| Control | Purpose |
|---|---|
| Role-Based Provisioning | Assign permissions through approved security groups rather than individual requests |
| Joiner, Mover and Leaver Process | Grant appropriate access when employees join, update it when roles change and remove it when they leave |
| Periodic Access Reviews | Confirm that permissions remain necessary and appropriate for each role |
| Segregation-of-Duties Checks | Detect and prevent incompatible financial permission combinations |
| Privileged Access Reviews | Review administrative eligibility, activation and continued business need |
| Access Change Logging | Maintain records of permission changes, approvals and privileged activity |

## 6. Success Criteria

The remediation would be considered successful when:

- All six accounts have been reviewed against approved role requirements.
- Excessive direct and inherited permissions have been removed.
- Each employee's effective access matches the approved RBAC model.
- Payee creation and payment approval are appropriately separated.
- Technical administration is restricted and subject to suitable privileged-access controls.
- Authorised billing and finance workflows continue to operate.
- Access reviews and monitoring are established to detect future permission sprawl.
