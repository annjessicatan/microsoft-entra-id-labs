# 🛡️ Lab 5: Multifactor Authentication (MFA)

[⬅ Previous: Lab 4 – SSPR](../04-sspr/README.md) &nbsp;|&nbsp; [Main README](../README.md) &nbsp;|&nbsp; [Next: Lab 6 – Conditional Access ➡](../06-conditional-access/README.md)

![Microsoft Entra ID](https://img.shields.io/badge/Microsoft-Entra%20ID-0078D4?logo=microsoft&logoColor=white)
![Security](https://img.shields.io/badge/Focus-Strong%20Authentication-red)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Tasks](https://img.shields.io/badge/Tasks-3%20of%203-brightgreen)

> **Scenario:** A stolen password alone shouldn't be enough to get into Contoso's systems. I enabled MFA for a user, reviewed the service settings that control how MFA behaves, and configured account lockout rules to stop attackers who try to wear users down with repeated approval prompts.

---

## 📋 At a Glance

| | |
|---|---|
| **Platform** | Microsoft Entra admin center |
| **Focus area** | Strong authentication and account protection |
| **Tasks completed** | 3 |
| **Core skills** | Per-user MFA, MFA service settings, Trusted IPs, MFA account lockout |

### 🏆 Outcomes

- ✅ Enabled **per-user MFA** for a user and confirmed the status change
- ✅ Reviewed the MFA **service settings**: app passwords, Trusted IPs, verification options, and remembered devices
- ✅ Configured **MFA account lockout**: 3 denials trigger a lockout, with a 180-minute counter reset and a 15-minute automatic unblock
- ✅ Reviewed related protections: **fraud alert**, **block/unblock users**, and **notifications**

---

## 🗺️ Lab Workflow

```
Enable per-user MFA ──► Review service settings ──► Configure account lockout
       Task 1                  Task 2                       Task 3
```

---

## 🧭 Walkthrough

### Task 1: Enable Per-User MFA

**Goal:** Require an additional verification step for a specific user.

1. Signed in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Went to **Identity → Users → All users → Per-user MFA**.
3. Selected **Bhogeswar Kalita** and chose **Enable MFA**.
4. Read the information box. It includes a link that can be sent to the user so they can complete MFA setup.
5. Selected **Enable** and confirmed the user's MFA status updated (shown as **Enforced** in my lab).

![Per-user MFA menu](screenshots/01-per-user-mfa-menu.png)
*Users → All users → Per-user MFA*

![Enable MFA](screenshots/02-select-user-enable-mfa.png)
*Selecting the user and choosing Enable MFA*

![Enable MFA pop-up](screenshots/03-enable-mfa-popup.png)
*Information box with the MFA setup link for the user*

![MFA status](screenshots/04-mfa-status-enforced.png)
*User's MFA status after enabling*

---

### Task 2: Review MFA Service Settings

**Goal:** Understand the tenant-wide options that shape how MFA behaves.

1. From **Per-user MFA**, opened **Service settings**.
2. Reviewed each section (no changes were saved):

| Setting | What it's for |
|---|---|
| **App passwords** | Lets users keep using legacy apps that don't support MFA |
| **Trusted IPs** | Lets users from known, safe IP ranges (such as the office network) skip MFA prompts |
| **Verification options** | Controls which methods users can use as their second factor |
| **Remember MFA on trusted device** | Lets users on trusted devices skip MFA for a set number of days |

![Service settings page](screenshots/05-service-settings-page.png)
*Per-user MFA → Service settings*

![Trusted IPs and verification options](screenshots/06-trusted-ips-verification-options.png)
*Reviewing Trusted IPs, verification options, and remembered devices*

> ⚠️ **Security note:** App passwords and Trusted IPs both reduce MFA coverage. Use them sparingly, and keep trusted ranges as narrow as possible.

---

### Task 3: Configure MFA Account Lockout

**Goal:** Block accounts that receive repeated denied MFA prompts, a sign that someone else may be trying to sign in.

1. Went to **Protection → Show more → Multifactor authentication → Account lockout**.
2. Configured the following values:

| Setting | Value | Meaning |
|---|---|---|
| **Number of MFA denials to trigger account lockout** | `3` | Three denied prompts lock the account |
| **Minutes until account lockout counter is reset** | `180` | The denial count resets after 3 hours |
| **Minutes until account is automatically unblocked** | `15` | The account unlocks itself after 15 minutes |

3. Selected **Save**.
4. Reviewed other MFA options: **Fraud alert**, **Block/unblock users**, and **Notifications**.

![MFA menu](screenshots/07-mfa-menu.png)
*Protection → Multifactor authentication*

![Account lockout values](screenshots/08-account-lockout-values.png)
*Lockout configured: 3 denials, 180-minute reset, 15-minute unblock*

![Lockout saved](screenshots/09-lockout-saved.png)
*Settings saved*

![Other MFA options](screenshots/10-other-mfa-options.png)
*Reviewing fraud alert, block/unblock users, and notifications*

---

## 🔑 Key Concepts

| Concept | Why it matters |
|---|---|
| **MFA** | Requires more than a password, such as an app prompt or phone code, so a stolen password alone isn't enough |
| **Per-user MFA** | Enables MFA one account at a time. It's simple but doesn't scale. |
| **Trusted IPs** | Convenient for known networks, but each exception is a gap an attacker could use |
| **App passwords** | A workaround for legacy apps that carries more risk |
| **MFA account lockout** | Limits repeated denied prompts, helping defend against "MFA fatigue" attacks |
| **Fraud alert** | Lets users report an unexpected MFA prompt so the account can be blocked |

> 💡 **Per-user MFA vs. Conditional Access:** Per-user MFA is the older approach. For larger environments, Microsoft recommends enforcing MFA through Conditional Access policies, which are more flexible and based on context. That's what [Lab 6](../06-conditional-access/README.md) covers.

---

## 🛡️ Security Practices Applied

- **Defense in depth:** MFA adds a second barrier even if a password is compromised.
- **Attack-aware configuration:** Lockout thresholds target MFA fatigue, where attackers spam prompts hoping the user approves one.
- **Minimizing exceptions:** Service settings that bypass MFA (Trusted IPs, app passwords, remembered devices) were reviewed rather than loosened.
- **Reviewing before changing:** Settings in Task 2 were inspected without saving changes.

---

## 💡 Key Takeaways

- MFA is one of the most effective single controls against account compromise, but its exceptions (Trusted IPs, app passwords, remembered devices) need careful management.
- A lockout policy that is too strict can lock out real users, while one that is too loose lets attackers keep trying. The values need to balance both.
- Per-user MFA is useful for understanding the basics, but policy-based enforcement scales better.
- Fraud alerts and notifications give users a way to help detect attacks.

---

## 🔗 References

- [How Microsoft Entra Multifactor Authentication works](https://learn.microsoft.com/entra/identity/authentication/concept-mfa-howitworks)
- [Enable per-user MFA](https://learn.microsoft.com/entra/identity/authentication/howto-mfa-userstates)
- [Configure MFA settings](https://learn.microsoft.com/entra/identity/authentication/howto-mfa-mfasettings)

---

<sub>Completed in a Microsoft training lab environment. Tenant names and identifiers are redacted from all screenshots.</sub>
