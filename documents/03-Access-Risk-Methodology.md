# 03 — Access Risk Assessment Methodology

**Project:** Northwind Health | IAM Permission Sprawl & RBAC Design


---

## 1. Risk Assessment Approach

The assessment uses a qualitative, risk-based approach to evaluate permissions assigned to employees within Northwind Health's billing application.

Existing access is compared against documented job responsibilities and the proposed RBAC model to identify excessive privileges, inconsistent access and segregation-of-duties (SoD) conflicts.

Risk severity is assessed by considering the sensitivity of the permissions, the potential impact of misuse and whether an employee can perform incompatible actions without independent oversight.

## 2. Risk Assessment Criteria

| Assessment Factor      | Evaluation Criteria                                                                             |
| ---------------------- | ----------------------------------------------------------------------------------------------- |
| Business Justification | Whether assigned permissions are necessary for the employee's documented responsibilities       |
| Privilege Level        | Whether access includes sensitive financial actions, bulk data exports or system administration |
| Segregation of Duties  | Whether an employee can perform incompatible steps within a financial process                   |
| Data Sensitivity       | Whether permissions could expose or modify sensitive patient billing information                |
| Potential Impact       | Possible consequences for financial integrity, patient information and business operations      |


## 3. Segregation-of-Duties Assessment

Segregation of duties reduces the risk of one employee controlling multiple sensitive stages of a business process.

The following permission combinations require particular attention:

| Permission Combination                         | Potential Risk                                                                             | Assessment Consideration                                                              |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------- |
| Create new payee + approve payments            | A user could create a fraudulent payment recipient and approve a payment to that recipient | These responsibilities should be assigned to different authorised users               |
| System admin + financial permissions           | A privileged account could potentially combine technical control with financial actions    | Technical administration should be separated from business transaction permissions    |
| Edit patient billing details + approve refunds | A user could potentially modify billing information and approve a related refund           | Confirm whether the application supports independent review or prevents self-approval |

The final combination requires workflow validation. Billing Supervisors are expected to edit billing details and approve refunds, so the proposed control would be independent review of relevant transactions rather than removing a legitimate role permission.

Creating a new payee and approving refunds may also present a conflict **if refunds can be directed to newly created payees**. That relationship would need to be confirmed through the billing workflow.

## 4. Risk Severity Classification

| Severity | Criteria |
|---|---|
| Critical | Extensive privileged access combining system administration and sensitive financial functions |
| High | Excessive financial permissions or significant segregation-of-duties conflicts |
| Medium | Unnecessary access to sensitive data or individual functions outside job responsibilities |
| Low | Minor access discrepancies with limited potential impact |
| No Change | Permissions align with documented job responsibilities |

Severity is based on the nature of the permissions, segregation-of-duties conflicts and potential business impact.

## 5. Risk Prioritisation

The assessment prioritises findings according to the potential consequences of unnecessary access.

Fraser's account receives the highest priority because it combines all seven permissions, including System Admin, financial approvals, payee creation and bulk billing-data export.

Ben and Dev require prompt attention because they hold financial permissions beyond their documented responsibilities. Dev's combination of payee creation and payment approval presents a particularly important SoD conflict.

Ana and Erin also require access corrections, while Chloe's permissions align with the stated Billing Clerk responsibilities.

The individual findings, severity ratings and recommended actions are recorded in [**Document 04 — Access Findings and Risk Register**](04-Access-Findings-and-Risk-Register.md).
