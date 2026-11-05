# IAM: The Permission Sprawl

## 🎫 The Ticket

It's 12 October 2026, my second week on the security team at Northwind Health, and a new ticket has landed on my desk.

The IT Manager writes:

> Everyone in Billing has been given access one request at a time, and it's a mess. **Can you design proper roles, and flag anything that shouldn't be allowed in the first place?**

Before designing anything, I need to understand how the access got this way.

<br>

## What I'm Working With

I have six employee accounts in Billing, along with their job responsibilities and the permissions each one holds. Access was granted one request at a time, so every permission made sense when it was approved, but nobody looked at the whole picture.

I'm checking for **permissions that don't fit the job**, and for combinations that become risky together.

<br>

## How I Worked Through It

**1. Who has access they don't actually need?**
I compared each account's permissions against the person's job responsibilities. Where the two didn't match, I treated the extra access as a finding.

**2. What could someone do with those permissions combined?**
A single permission can look harmless. Together they can let one person start and approve the same transaction, so I checked combinations for segregation of duties (SoD) conflicts.

**3. How can I fix the risks without disrupting Billing?**
Removing access is only half the job. Some permissions are genuinely needed, so I designed an RBAC model around job roles and planned the changes in stages.

**4. What needs attention first?**
I ranked the accounts by risk and built a 3 step rollout plan that deals with critical access first. Not every account needs the same response.

<br>

## What I Found

The review covered six accounts.

| Severity      | Accounts | Finding                                                |
| ------------- | -------: | ------------------------------------------------------ |
| 🔴 Critical   |        1 | IT Support employee with all seven Billing permissions |
| 🟠 High       |        2 | [Confirm findings from the assessment]                 |
| 🟡 Low/Medium |        2 | [Confirm findings from the assessment]                 |
| 🟢 No change  |        1 | Access matches job responsibilities                    |
| **Total**     |    **6** |                                                        |

Five of the six accounts require permission changes.

 <br>
 
## Why We Start With Fraser

The most serious finding was **Fraser, an IT Support employee with all seven Billing system permissions**, including financial actions and system administration.

That raised a simple question: why can the person who fixes the system also move the money?


My recommendation is to remove his financial permissions urgently and use temporary, approved access for the technical tasks that need it.
But this is about his access, not his character. Nothing in the supplied data shows that Fraser misused those permissions. The concern is that his account allows financial actions his job doesn’t require. I don’t need to assume bad intentions to flag that, the access itself is what needs fixing.

<br>

## Looking Back at the Review

When I started this case, initially my focus was on identifying excessive permissions, designing roles, and recommending what needed to be removed. But the further I went, the more questions I had about my own recommendations.

Take the Billing Supervisor role. At first, removing conflicting permissions seemed straightforward. Then I realised that some permissions are genuinely needed for the job, even when they create risks. That made me think about **additional controls instead of simply removing access.**

I also reconsidered my rollout plan. Fraser's access was originally part of the wider migration, but a critical risk shouldn't wait while everyone else's roles are being tested. I moved his restrictions to the first step and connected that decision to a practical just-in-time (JIT) solution for IT Support.

Basically, I kept going back to what I had written earlier. I questioned my own assumptions and improved my recommendations as the investigation developed, realising that security analysis isn't always a straight line. Looking closer at something can make you rethink an earlier choice, and being willing to do that leads to stronger, better recommendations.&#x20;

<br>

## What will I do differently next time?**

I'd stop treating a plausible reason as a justification. With Fraser, I first accepted that someone in IT Support could have a technical reason for that access. A reason that sounds plausible isn't the same as one that was approved, limited, and reviewed. Next time, I'd ask for the approval and the control rather than looking for a reasonable explanation. I will stand on this question

**Does this access still serve a real purpose, and what control protects against the risk when it does?**



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





