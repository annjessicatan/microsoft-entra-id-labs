# 🚦 Lab 6: Conditional Access: Configuration, Testing & Troubleshooting

[⬅ Previous: Lab 5 – MFA](../05-mfa/README.md) &nbsp;|&nbsp; [Main README](../README.md)

![Microsoft Entra ID](https://img.shields.io/badge/Microsoft-Entra%20ID%20P2-0078D4?logo=microsoft&logoColor=white)
![Policy](https://img.shields.io/badge/Policy-Conditional%20Access-purple)
![Mode](https://img.shields.io/badge/Mode-Report--only-yellow)
![Status](https://img.shields.io/badge/Status-Completed-success)

> **Scenario:** Before rolling out any access policy at Contoso, an admin needs to know who it affects and what it will do. I built a Conditional Access policy, ran it in **Report-only mode** so no real users were disrupted, and used **sign-in logs** and the **What If tool** to verify its scope. Along the way I diagnosed licensing, resource, and logging issues, the kind of troubleshooting that comes up in real tenants.

---

## 📋 At a Glance

| | |
|---|---|
| **Platform** | Microsoft Entra admin center (Entra ID P2 trial) |
| **Policy** | `Office 365`: Require multifactor authentication |
| **Mode** | Report-only |
| **Target user** | Bhogeswar Kalita |
| **Target resource** | Office 365 |
| **Core skills** | Conditional Access design, Report-only evaluation, sign-in log analysis, What If simulation, troubleshooting |

### 🏆 Outcomes

- ✅ Created a Conditional Access policy **scoped to one user and one resource**, requiring MFA
- ✅ Deployed it in **Report-only mode** to evaluate impact without enforcing it
- ✅ **Verified the policy using real sign-in logs**: `Report-only: Success` on two Outlook sign-ins
- ✅ Ran **three What If simulations** to confirm which users and services the policy matches
- ✅ Diagnosed **five real issues** (unavailable app, misleading "Not applied" status, mailbox licensing error, delayed logs, Security Defaults)

---

## 🔀 Note: How This Lab Differs from the Original Exercise

The original Microsoft exercise had me create a policy that **blocks a user from Microsoft Sway** and test it with What If. **Sway did not appear in the available resources in my tenant**, so I couldn't follow that exercise exactly.

Instead of stopping, I adapted the lab to practice the same core concepts:

| | Original exercise | What I did |
|---|---|---|
| **Target resource** | Microsoft Sway | Office 365 |
| **Grant control** | Block access | Require multifactor authentication |
| **Policy state** | On | Report-only |
| **Validation** | What If tool | Real sign-in logs **and** What If tool |

The concepts practiced are the same: user assignment, resource targeting, grant controls, and testing with What If. I also added log-based validation that the original exercise doesn't include.

---

## 🗺️ Lab Workflow

```
Assign license ──► Create policy ──► Report-only ──► Sign-in logs ──► What If ──► Troubleshoot
                  (user + resource    (safe test)     (verify real     (simulate    (5 issues
                   + MFA)                              evaluations)     scenarios)   resolved)
```

---

## 🧭 Walkthrough

### Part 1: Prepare the License

Conditional Access requires Microsoft Entra ID P1 or P2 licensing for the users it covers. An active subscription isn't enough on its own: the license must be **assigned to the user**.

1. In the Microsoft 365 admin center, went to **Users → Active users → Bhogeswar Kalita → Licenses and apps**.
2. Found Microsoft Entra ID P2 available from the active trial but not assigned to the test user.
3. Assigned **Microsoft Entra ID P2** to the user.

![License assignment](screenshots/01-user-license-p2.png)
*Assigning Microsoft Entra ID P2 to the test user*

---

### Part 2: Create the Conditional Access Policy

1. Went to **Protection → Conditional Access → Policies → New policy**.
2. Named the policy `Office 365`.

![Conditional Access overview](screenshots/02-ca-overview.png)
*Conditional Access overview page*

| Section | Configuration |
|---|---|
| **Users** | Include → Select users and groups → Bhogeswar Kalita |
| **Target resources** | Include → Select resources → Office 365 |
| **Grant** | Grant access → **Require multifactor authentication** → Require one of the selected controls |
| **Conditions** | Left unconfigured (user risk, sign-in risk, device platforms, locations, client apps, device filters) |
| **Enable policy** | **Report-only** |

![User assignment](screenshots/03-policy-users.png)
*Policy scoped to the test user only*

![Target resource](screenshots/04-target-resources-office365.png)
*Office 365 selected as the target resource*

![Grant control](screenshots/05-grant-require-mfa.png)
*Grant control: Require multifactor authentication*

![Report-only](screenshots/06-report-only-state.png)
*Policy state set to Report-only*

![Policy created](screenshots/07-policy-created.png)
*Policy visible on the Conditional Access policies list*

> 💡 **Why Report-only?** It records what the policy *would* have done to each sign-in without enforcing it. This is the safe way to test a policy before turning it on, since a misconfigured policy could lock out real users.

---

### Part 3: Test and Troubleshoot

I tried to confirm the policy was being evaluated during real sign-ins, and ran into several issues. Each one taught me something about how Conditional Access works in practice.

| # | Issue | Investigation | Resolution | Lesson |
|---|---|---|---|---|
| 1 | **Sway wasn't available** as a target resource | Searched resources and found Office 365, Teams Connector, and SharePoint Connector | Used Office 365 as the target | Available resources differ by tenant |
| 2 | Sign-ins showed **"Not applied"** for Conditional Access | Checked sign-ins across several apps (Azure Portal, OfficeHome, Power Pages, Outlook) and found a separate **Report-only** section in the sign-in details | Read the Report-only results for the custom policy and found **Report-only: Success** | "Not applied" describes *enforced* policies. Report-only results appear separately. |
| 3 | **Outlook on the web returned an HTTP 500** error (`OwaUserHasNoMailboxAndNoLicenseAssignedException`) | Checked the user's licenses: no Exchange Online license assigned | Recognized the error was a mailbox licensing issue, not a policy problem | Authentication and mailbox availability are separate. The sign-in still succeeded. |
| 4 | **New sign-ins weren't showing** in the logs | Refreshed, widened the time filter to 24 hours, rechecked the user filter, and reviewed interactive sign-ins | Located the newer Outlook sign-in event | Logs are delayed. Check time range and filters before assuming a test failed. |
| 5 | **Security Defaults** was enabled | Reviewed it under Identity → Overview → Properties → Manage security defaults | Left it enabled and kept my policy in Report-only | Security Defaults and custom Conditional Access are separate, and disabling the baseline needs a replacement plan |

![Sway not found](screenshots/08-sway-not-found.png)
*Searching for Sway returned no results in my tenant*

![Not applied](screenshots/09-signin-not-applied.png)
*Sign-in details showing Conditional Access as "Not applied"*

![Report-only success](screenshots/10-signin-report-only-success.png)
*The Report-only tab showing the custom policy evaluated: Success*

![Outlook error](screenshots/11-outlook-500-error.png)
*Outlook HTTP 500 caused by a missing Exchange Online license*

![Security Defaults](screenshots/12-security-defaults.png)
*Security Defaults enabled in the tenant*

---

### Part 4: Verify with Sign-in Logs

I found two Outlook sign-in events for the test user on **November 1, 2026**, at 07:42:38 UTC and 07:58:12 UTC. Both showed the same results:

| Field | Result |
|---|---|
| User | Bhogeswar Kalita |
| Application | One Outlook Web |
| Resource | Office 365 Exchange Online |
| Sign-in status | Success |
| Conditional Access (enforced) | Not applied |
| Custom policy | Office 365 |
| Grant control | MFA |
| **Report-only result** | **Success** |

![Sign-in event 1](screenshots/13-signin-event-1.png)
*Sign-in event at 07:42:38 UTC*

![Sign-in event 2](screenshots/14-signin-event-2.png)
*Sign-in event at 07:58:12 UTC*

**What this proves:**
1. The policy was **evaluated** during a real sign-in.
2. The test user matched the **user assignment**.
3. Exchange Online matched the **resource assignment**.
4. The MFA requirement was satisfied (an earlier sign-in had already provided an MFA claim in the token).

> ⚠️ **Important distinction:** `Report-only: Success` does **not** mean an MFA challenge was enforced. It means the sign-in met the policy's requirements during evaluation.

---

### Part 5: What If Simulations

The **What If** tool shows which policies would apply to a set of sign-in conditions, without performing a real sign-in.

| # | User | Cloud app | Result |
|---|---|---|---|
| 1 | Bhogeswar Kalita | Office 365 Exchange Online | ✅ `Office 365` policy matched (MFA, Report-only, Has Filter: No) |
| 2 | Bhogeswar Kalita | Office 365 SharePoint Online | ✅ `Office 365` policy matched (MFA, Report-only, Has Filter: No) |
| 3 | A different user | Office 365 | ❌ **No policies found** |

![What If: Exchange](screenshots/15-whatif-exchange.png)
*Simulation 1: policy matches the test user on Exchange Online*

![What If: SharePoint](screenshots/16-whatif-sharepoint.png)
*Simulation 2: the same policy also matches SharePoint Online*

![What If: different user](screenshots/17-whatif-different-user.png)
*Simulation 3: no policies found for a user outside the policy's scope*

**Interpretation:**
- Simulation 2 showed that targeting **Office 365** covers multiple services, not just Exchange Online.
- Simulation 3 showed that **user assignments** control which identities a policy affects.
- `Has Filter?: No` was expected, since no device filter was configured.

---

## 🔑 Key Concepts

| Concept | Why it matters |
|---|---|
| **Conditional Access** | If-then rules evaluated at sign-in: if the assignments and conditions match, apply the access controls |
| **Assignments** | Define *who* (users/groups) and *what* (apps/resources) a policy covers |
| **Grant controls** | The outcome: block access, or allow it with requirements such as MFA |
| **Report-only mode** | Evaluates and logs a policy's impact without enforcing it |
| **Sign-in logs** | The record of real authentication events and which policies were evaluated |
| **What If tool** | Simulates a policy match for a chosen user, app, and conditions |
| **Security Defaults** | Baseline protection that is separate from custom Conditional Access policies |
| **Licensing** | Entra ID P1 or P2 must be assigned to users covered by Conditional Access |

---

## 🛡️ Security Practices Applied

- **Test before enforcing:** Report-only mode let me observe the policy's effect without affecting access.
- **Narrow scope:** The policy was limited to one test user rather than the whole tenant.
- **Don't weaken the baseline:** Security Defaults stayed enabled during testing.
- **Verify with evidence:** I confirmed behavior through real sign-in logs instead of assuming the policy worked.
- **Simulate edge cases:** What If testing covered a matching service, a second service, and a user outside the policy's scope.

---

## 💡 Key Takeaways

1. **Authentication doesn't guarantee application access.** A user can sign in successfully and still be unable to open a mailbox without the right license.
2. **Read Report-only results separately.** The overall status can say "Not applied" while the Report-only result says "Success."
3. **Licensing matters.** Entra ID P1 or P2 must be assigned to users covered by Conditional Access.
4. **Logs aren't instant.** Check time ranges and filters before concluding a test failed.
5. **Resource scope can be broader than expected.** Targeting Office 365 matched both Exchange Online and SharePoint Online.
6. **Plan before replacing Security Defaults.** Equivalent protections and emergency access accounts should be in place first.
7. **Adapting is part of the job.** When the exercise's target app wasn't available, I kept the lab's learning goals and documented what I changed.

---

## 🚀 Possible Next Steps

- Rebuild the original **block-access** policy using an app available in the tenant, initially in Report-only mode
- Add **exclusions**, including an admin or emergency access account, to avoid accidental lockout
- Explore **location-based** and **device-based** conditions
- Explore **sign-in risk** and **user risk** policies (requires appropriate licensing)
- Compare Report-only results with an enforced policy in a properly licensed test environment

---

## 🔗 References

- [Conditional Access overview](https://learn.microsoft.com/entra/identity/conditional-access/overview)
- [Conditional Access Report-only mode](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-report-only)
- [What If tool](https://learn.microsoft.com/entra/identity/conditional-access/what-if-tool)
- [Security defaults](https://learn.microsoft.com/entra/fundamentals/security-defaults)
- [Sign-in logs](https://learn.microsoft.com/entra/identity/monitoring-health/concept-sign-ins)

---

<sub>Completed in a Microsoft Entra ID P2 trial tenant. Tenant names and identifiers are redacted from all screenshots.</sub>
