# 01 — Scenario and Scope

**Project:** Northwind Health | IAM Permission Sprawl & RBAC Design  
**Assessment Area:** Identity and Access Management (IAM)

---

## 1. Business Context

Northwind Health is a fictional US-based healthcare SaaS provider supporting approximately 400 clinics with a workforce of 120 employees. The organisation handles electronic protected health information (ePHI), making appropriate access controls essential for protecting sensitive information and supporting business operations.

The Billing department has accumulated permissions through individual access requests rather than a consistent role-based model.

This has resulted in employees performing similar duties holding different permissions. Some employees also have access to financial functions or sensitive data beyond their stated responsibilities.

The assessment focuses on improving access governance through Role-Based Access Control (RBAC), least privilege and segregation of duties (SoD).

## 2. Assessment Objectives

The assessment aims to:

- Review existing permissions against defined job responsibilities.
- Identify excessive access and incompatible permission combinations.
- Design appropriate job-based roles and security groups.
- Recommend removal of unnecessary individual permission grants.
- Prioritise findings according to potential security and business impact.
- Propose a controlled migration to the new access model.
- Evaluate how temporary privileged access could support IT troubleshooting.

## 3. Scope of Review

The assessment covers six employees across four job roles within Northwind Health's billing application.

### Job Responsibilities and Required Access

| Job Role | Required Access Based on Job Description |
|---|---|
| Billing Clerk | Create invoices and edit patient billing details |
| Billing Supervisor | All Billing Clerk permissions, plus approve refunds |
| Finance Manager | Approve payments and export billing data for monthly reporting |
| IT Support | Maintain and troubleshoot the system without performing financial transactions |

These job descriptions establish the baseline for assessing whether existing permissions are appropriate.

The current permission assignments and proposed RBAC model are documented in [**Document 02 — Current Access and RBAC Design**](02-Current-Access-and-RBAC-Design.md).
## 4. Assessment Approach

| Stage | Activity |
|---|---|
| Review | Examine current permissions and stated job responsibilities |
| Compare | Identify differences between assigned access and required access |
| Design | Define job-based RBAC roles and proposed security-group membership |
| Assess | Evaluate excessive permissions, SoD conflicts and potential impact |
| Prioritise | Assign qualitative risk levels to the identified findings |
| Recommend | Document access removals, preventive controls and privileged-access safeguards |
| Plan | Propose testing, phased migration and post-change verification |

The assessment applies the principle of least privilege: employees should receive only the permissions necessary to perform their authorised responsibilities.


