
# Permission Sprawl & RBAC

## 🎫 The Ticket

It's 12 October 2026, my second week on the security team at Northwind Health, and a new ticket has landed on my desk.

The IT Manager writes:

> Everyone in Billing has been given access one request at a time, and it's a mess. Can you design proper roles, and flag anything that shouldn't be allowed in the first place?

<BR>

## What's the Risk?

After reading the ticket, I looked through the access records to understand how permissions had been assigned. I noticed that some employees had access beyond what their roles required. This looked like classic permission sprawl.

It raised two concerns: internal and external risks.

On the inside, a Billing employee who can both set up and approve payments could misuse that access. They could also make an honest mistake that goes unnoticed if there is no second check.

From the outside, if an attacker compromises that account, they inherit the same permissions.

So the question wasn't just who had too much access, but **what those permissions could allow someone to do together.**

<BR>

## The Investigation

### 1. Who has access they don't actually need?

I compared each account's permissions against the person's job responsibilities. Where the two didn't match, I treated the extra access as a finding.

### 2. What could someone do with those permissions combined?

A single permission can look harmless. Together, they can let one person start and approve the same transaction, so I checked combinations for segregation of duties (SoD) conflicts.

### 3. How can I fix the risks without disrupting Billing?

Removing access is only half the job. Some permissions are genuinely needed, so I designed an RBAC model around job roles and planned the changes in stages.

### 4. What needs attention first?

I ranked the accounts by risk and built a three-step rollout plan that deals with critical access first. Not every account needs the same response.

<BR>

## What I Found

I reviewed six accounts in the Billing system. Five needed permission changes.

| Severity | Accounts | Finding |
|---|---:|---|
| 🔴 Critical | 1 | IT Support account with all seven Billing system permissions, including System Admin |
| 🟠 High | 2 | Excessive financial permissions, including conflicting transaction and approval rights |
| 🟡 Medium | 2 | Access beyond what the employees' roles required |
| 🟢 No change | 1 | Permissions matched the employee's responsibilities |
| **Total** | **6** | |

**Fraser's account stood out.** He worked in IT Support but held every Billing permission, including the ability to create payees and approve payments.

<BR>

## Decisions & Recommendations


This raised a question I couldn't ignore: **Why can the person who fixes the system also move the money?**

His combination of permissions created two serious risks:

- **Insider fraud:** Someone misusing Fraser's account could potentially create a fraudulent payee and approve payments without independent oversight. If his System Admin access also allows changes to audit settings or logs, they might be able to interfere with the records used to detect that activity. I would need to verify those administrative capabilities.

- **Account compromise:** If an attacker gained access to Fraser's account, they could inherit both his financial permissions and administrative access. One compromised account could therefore expose several sensitive functions at once.

I couldn't tell from the permission records how Fraser ended up with all seven permissions. Were they granted for an earlier support task and never removed, or did he inherit them through an overly broad role?

**My recommendation** was to remove his six unnecessary financial and Billing permissions, while checking which administrative access he genuinely needed for IT Support. For tasks requiring elevated privileges, I recommended temporary, just-in-time (JIT) access instead of permanent access.

<BR>

## What Will I Do Differently Next Time?

This time, I started with individual accounts and worked towards designing an RBAC model. Next time, I'd reverse that approach.

I'd start by understanding what each role needs to do, then design what the access should look like. That would give me a clearer baseline to compare against the existing permissions, rather than working out what to remove one account at a time.

I'd still address urgent risks like Fraser's immediately, but I'd approach the wider review with a clearer picture of the access model I was trying to achieve.

I'd also bring relevant security guidance into the investigation earlier, using it to shape the controls I recommend and identify what needs testing.

<BR>


## Explore the Investigation

| Document                                                                                   | What's Inside                                       |
| ------------------------------------------------------------------------------------------ | --------------------------------------------------- |
| [01. Source Data](Document/01.%20Source%20Data.md)                                         | Original access and job requirements                |
| [02. RBAC Design](Document/02.%20RBAC%20Design.md)                                         | Proposed roles and security groups                  |
| [03. Segregation of Duties (SoD)](Document/03.%20Segregation%20of%20Duties%20%28SoD%29.md) | Conflicting permissions and recommended controls    |
| [04. Findings & Recommendations](Document/04.%20Findings%20%26%20Recommendations.md)       | Employee findings and risk priorities               |
| [05. Rollout Plan](Document/05.%20Rollout%20Plan.md)                                       | Three-step migration and privileged access approach |

<Bbr>
  
---

[← Week 1: Access Review](https://github.com/itsanitarose/IAM-Access-Review) · [All Case Studies](https://github.com/itsanitarose/IAM-Case-Studies) · [Week 3: Agent Security Review →](https://github.com/itsanitarose/IAM-AI-Agent-Security-Review)

*<sub>Northwind Health is fictional. This is independent work; no production systems were changed.</sub>*





