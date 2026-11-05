# IAM: The Permission Sprawl

## The Scenario

It's my second week on the security team at Northwind Health, and a new ticket has landed on my desk.

The problem? **Permission sprawl in Billing.**

Access has been granted one request at a time, leaving employees with permissions that don't always match their jobs.
<br><br>

### 🎫 The Ticket

**IT Manager's Request:**

> "Everyone in Billing has been given access one request at a time, and it's a mess. Can you design proper roles, and flag anything that shouldn't be allowed in the first place?"

*Audit date: 12 October 2026*

## My Investigation

I reviewed six employee accounts against their job responsibilities, looking for excessive access and permissions that could become dangerous when combined.

Three questions guided my investigation:

- **Who has access they don't actually need?**
- **What could someone do with those permissions combined?**
- **How can I fix the risks without disrupting Billing?**

I used the findings to design an RBAC model, identify access changes and propose a three-step rollout plan.

## What I Found

| Risk | Accounts |
|:-----|:--------:|
| 🔴 Critical | 1 |
| 🟠 High | 2 |
| 🟡 Low/Medium | 2 |
| 🟢 No change | 1 |

**Five of the six accounts require permission changes.**

## Top Priority: Fraser

The most serious finding was **Fraser, an IT Support employee with all seven Billing system permissions**, including financial actions and system administration.

It raised a question I kept coming back to:

**Why should someone who fixes the system also be able to carry out financial transactions?**

I recommended urgently removing Fraser's unnecessary financial permissions and using temporary, approved privileged access when technical support requires it.

These were potential access risks, not evidence of wrongdoing.

## Case Study Outcome

The assessment produced:

- A proposed RBAC design based on job responsibilities.
- Findings by employee and access removal recommendations.
- An investigation of segregation-of-duties (SoD) risks.
- A three-step rollout plan that prioritises critical access without disrupting Billing.

## What I Learned

When I started this investigation, my focus was on identifying excessive permissions, designing roles and recommending what needed to be removed.

But the further I went, the more questions I had about my own recommendations.

One example was the Billing Supervisor role. At first, removing conflicting permissions seemed straightforward. Then I realised that some permissions are genuinely needed for the job, even when they create risks. That made me think about **additional controls instead of simply removing access**.

I also reconsidered my rollout plan. Initially, Fraser's access was part of the wider migration. But why should a critical risk wait while everyone else's roles are being tested? I moved his access restrictions to the first step and connected that decision to a practical JIT solution for IT Support.

I found myself going back to earlier sections, questioning assumptions and improving the recommendations as the investigation developed.

**My biggest lesson here was that security analysis isn't always a straight line.** Sometimes looking more closely at a problem makes you rethink an earlier decision. What matters is being willing to question it, understand the consequences and make the recommendation stronger.

## Explore the Investigation

| Document | What's Inside |
|:---------|:--------------|
| **[01. Source Data](01.%20Document/01.%20Source%20Data.md)** | Original access and job requirements |
| **[02. RBAC Design](01.%20Document/02.%20RBAC%20Design.md)** | Proposed roles and security groups |
| **[03. Segregation of Duties (SoD)](01.%20Document/03.%20Segregation%20of%20Duties%20(SoD).md)** | Conflicting permissions and recommended controls |
| **[04. Findings & Recommendations](01.%20Document/04.%20Findings%20%26%20Recommendations.md)** | Employee findings and risk priorities |
| **[05. Rollout Plan](01.%20Document/05.%20Rollout%20Plan.md)** | Three-step migration and privileged access approach |

<br>

---

[← Week 1: Access Review](https://github.com/itsanitarose/IAM-Access-Review) · [All Case Studies](https://github.com/itsanitarose/IAM-Case-Studies) · [Week 3: Agent Security Review →](https://github.com/itsanitarose/IAM-AI-Agent-Security-Review)

<sub>Northwind Health is fictional. This is independent work. No production systems were changed.</sub>





