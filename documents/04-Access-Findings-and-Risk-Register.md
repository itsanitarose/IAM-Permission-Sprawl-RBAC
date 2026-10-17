# 04 — Access Findings and Risk Register

**Project:** Northwind Health | IAM Permission Sprawl & RBAC Design

---

## 1. Findings Overview

The access review identified excessive permissions across five of the six employee accounts assessed.

The findings are prioritised according to the risk assessment methodology documented in [**Document 03 — Access Risk Assessment Methodology**](03-Access-Risk-Methodology.md).

| Severity | Accounts | Count |
|---|---|---|
| Critical | Fraser | 1 |
| High | Ben, Dev | 2 |
| Medium | Ana, Erin | 2 |
| No Change | Chloe | 1 |
| **Total** | **6 accounts reviewed** | **6** |

## 2. Access Risk Register

| ID | Employee / Role | Finding | Risk | Severity | Recommended Action |
|---|---|---|---|---|---|
| AR-01 | Fraser / IT Support | Holds all seven permissions, including System Admin and financial transaction access | Excessive privileged access could enable unauthorised financial actions, sensitive-data exposure and bypass of controls | **Critical** | Remove six billing and financial permissions; validate and restrict technical administration |
| AR-02 | Dev / Billing Supervisor | Can create payees, approve payments and export all billing data beyond supervisor duties | Payee creation combined with payment approval creates a significant segregation-of-duties conflict | **High** | Remove payee creation, payment approval and bulk export; retain supervisor permissions |
| AR-03 | Ben / Billing Clerk | Can approve refunds and create new payees outside clerk duties | Unnecessary financial capabilities increase the risk of unauthorised changes and transactions | **High** | Remove refund approval and payee creation; retain clerk permissions |
| AR-04 | Ana / Billing Clerk | Can export all billing data despite having no reporting responsibility | Unnecessary bulk export capability increases the risk of sensitive billing-data exposure | **Medium** | Remove billing-data export; retain clerk permissions |
| AR-05 | Erin / Finance Manager | Can approve refunds outside finance manager duties | Unnecessary refund approval expands financial transaction authority beyond the defined role | **Medium** | Remove refund approval; retain payment approval and reporting export |
| AR-06 | Chloe / Billing Clerk | Permissions match the documented Billing Clerk role | No excessive permissions identified | **No Change** | Retain current permissions and include in periodic access reviews |

## 3. Priority Findings

### Critical — Fraser: Excessive Privileged Access

Fraser's IT Support account has all seven permissions, including System Admin, payee creation, payment approval, refund approval and billing-data export.

These permissions combine technical administration with financial functions that are not required for IT Support.

**Recommended action:** Remove all six billing and financial permissions. Review the scope of System Admin access and replace standing broad privileges with restricted technical administration where feasible.

The technical controls for privileged access are addressed in [**Document 05 — Remediation and Preventive Controls**](05-Remediation-and-Preventive-Controls.md).

### High — Dev: Segregation-of-Duties Conflict

Dev is a Billing Supervisor and legitimately requires invoice creation, billing-detail editing and refund approval.

However, Dev can also create payees and approve payments. This allows one account to perform two sensitive stages of a payment process.

**Recommended action:** Remove payee creation, payment approval and bulk billing-data export. Retain the permissions required for the Billing Supervisor role.

### High — Ben: Unnecessary Financial Permissions

Ben is a Billing Clerk but can approve refunds and create new payees.

Neither permission is required for the Billing Clerk role.

**Recommended action:** Remove both permissions and retain invoice creation and billing-detail editing.

## 4. Additional Findings

Ana's bulk billing-data export permission should be removed because her Billing Clerk role does not require it.

Erin's refund approval permission should be removed because her Finance Manager role is responsible for payment approval and monthly reporting, not refund approval.

Chloe requires no immediate changes because her existing permissions align with the Billing Clerk role.

## 5. Recommended Remediation Order

| Priority | Account | Action |
|---|---|---|
| 1 | Fraser | Remove unnecessary financial and billing access; validate and restrict System Admin |
| 2 | Dev | Resolve payee creation and payment approval conflict; remove excess export |
| 3 | Ben | Remove unauthorised refund approval and payee creation |
| 4 | Ana, Erin | Remove remaining permissions outside job responsibilities |
| Routine | Chloe | Retain access and review periodically |

Remediation should be approved by the relevant business and system owners, tested for operational impact and followed by verification of each employee's effective access.

The implementation approach and preventive controls are detailed in [**Document 05 — Remediation and Preventive Controls**](05-Remediation-and-Preventive-Controls.md).
