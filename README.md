# IAM Permission Sprawl & RBAC Design | Northwind Health

*A fictional Identity and Access Management (IAM) case study focused on excessive permissions, role-based access control, segregation of duties and privileged access management.*

---

## Overview

Northwind Health is a healthcare SaaS company with approximately 120 employees, supporting 400 clinics and handling sensitive patient information.

The Billing department has accumulated individually assigned permissions, resulting in inconsistent access between employees performing similar roles and excessive privileges across several accounts.

I reviewed the access assigned to six employees, compared their permissions against job responsibilities, identified security risks and designed a proposed Role-Based Access Control (RBAC) model.

**The objective:** Reduce unnecessary access, establish consistent job-based permissions and recommend a controlled transition without disrupting business operations.

## Key Findings

| Severity | Count | Findings |
|---|---:|---|
| 🔴 Critical | 1 | IT Support account with all seven permissions, including financial approvals and system administration |
| 🟠 High | 2 | Billing employees holding incompatible or unnecessary financial permissions |
| 🟡 Medium | 2 | Excessive data export and refund approval permissions |
| 🟢 No change | 1 | Billing Clerk access consistent with stated job responsibilities |
| **Total** | **6** | **Six employee accounts reviewed** |

*Severity classifications are proposed qualitative assessments based on the scenario.*

## Top Priority — Fraser

Fraser works in IT Support but has all seven application permissions, including the ability to create payees, approve payments, approve refunds, export billing data and administer the system.

This combination creates a significant least-privilege and segregation-of-duties concern.

I recommend removing the six billing and financial permissions, verifying the scope of system administration and introducing controlled temporary elevation through Privileged Identity Management (PIM) and Just-in-Time (JIT) access where supported.

## Project Structure

| Document | Purpose |
|---|---|
| [01 — Scenario and Scope](documents/01-Scenario-and-Scope.md) | Defines the business context, objectives and scope |
| [02 — Current Access and RBAC Design](documents/02-Current-Access-and-RBAC-Design.md) | Documents current permissions, proposed roles and security groups |
| [03 — Access Risk Methodology](documents/03-Access-Risk-Methodology.md) | Explains risk criteria, least privilege and segregation-of-duties assessment |
| [04 — Access Findings and Risk Register](documents/04-Access-Findings-and-Risk-Register.md) | Records excessive access, severity and remediation priorities |
| [05 — Remediation and Preventive Controls](documents/05-Remediation-and-Preventive-Controls.md) | Proposes the rollout plan, access validation and PIM/JIT controls |

## IAM Skills Demonstrated

- Role-Based Access Control (RBAC) design
- Security-group and permission mapping
- Least-privilege access assessment
- Segregation-of-duties conflict identification
- Qualitative access risk assessment and prioritisation
- Privileged Identity Management (PIM) and Just-in-Time (JIT) access concepts
- Access remediation planning and validation
- Security documentation and reporting

## What I Learned

This project strengthened my understanding of how individually assigned permissions can create inconsistent access and make governance more difficult.

A key lesson was recognising the difference between supporting an application and performing its business functions. IT Support may need administrative capabilities for troubleshooting, but that does not automatically justify access to financial transactions.

I also learned that designing RBAC involves more than assigning security groups. Existing direct permissions must be removed and effective access verified to ensure the new roles enforce least privilege.

## What I Would Improve

With access to additional system information, I would:

- Confirm the business owner and approval process for creating new payees.
- Review the application's actual System Admin capabilities.
- Test the proposed roles against real business workflows.
- Validate segregation-of-duties controls at the transaction level.
- Verify that legacy individual permissions were removed after migration.
- Review audit logs and access changes to assess whether the controls operate as intended.

These additional checks would provide stronger evidence that the proposed access model is appropriate and effective.

---


