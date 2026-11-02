# 🔑 Lab 4: Self-Service Password Reset (SSPR)

[⬅ Previous: Lab 3 – Password Protection](../03-password-protection/README.md) &nbsp;|&nbsp; [Main README](../README.md) &nbsp;|&nbsp; [Next: Lab 5 – MFA ➡](../05-mfa/README.md)

![Microsoft Entra ID](https://img.shields.io/badge/Microsoft-Entra%20ID-0078D4?logo=microsoft&logoColor=white)
![Focus](https://img.shields.io/badge/Focus-Self--Service%20%26%20Security-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Tasks](https://img.shields.io/badge/Tasks-1%20of%201-brightgreen)

> **Scenario:** Password resets are one of the most common help desk requests. At Contoso, I configured Self-Service Password Reset so users can recover their own accounts securely, which cuts support workload and gets people back to work faster.

---

## 📋 At a Glance

| | |
|---|---|
| **Platform** | Microsoft Entra admin center |
| **Focus area** | Self-service identity recovery and help desk reduction |
| **Tasks completed** | 1 (plus 3 sub-tasks) |
| **Core skills** | SSPR scoping, authentication methods, registration policy, admin notifications |

### 🏆 Outcomes

- ✅ Enabled SSPR for **selected users only** by scoping it to the `Project23` group
- ✅ Configured **three verification methods**: email, mobile phone, and mobile app code
- ✅ Required users to **register for SSPR at sign-in**, with re-confirmation every **90 days**
- ✅ Turned on **admin notifications** when other admins reset their passwords

---

## 🗺️ Lab Workflow

```
Enable & scope SSPR ──► Authentication methods ──► Registration ──► Notifications
      Task 1                 Subtask 1              Subtask 2         Subtask 3
```

---

## 🧭 Walkthrough

### Task 1: Enable SSPR for a Specific Group

**Goal:** Roll out SSPR to a defined set of users instead of the whole organization.

1. Signed in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Went to **Protection → Password reset**.
3. Located the **Self service password reset enabled** setting, which has three options:

| Value | What it means |
|---|---|
| **None** | No users can use SSPR |
| **Selected** | Only members of the chosen group(s) can use SSPR |
| **All** | Every user can use SSPR |

4. Set the value to **Selected**.
5. Chose the **Project23** group created in [Lab 2](../02-group-management/README.md).
6. Selected **Save**.

![Password reset menu](screenshots/01-password-reset-menu.png)
*Protection → Password reset*

![SSPR set to Selected](screenshots/02-sspr-selected.png)
*SSPR enabled for Selected users*

![Select Project23](screenshots/03-select-project23.png)
*Choosing the Project23 group*

![Configuration saved](screenshots/04-sspr-saved.png)
*Configuration saved*

> 💡 **Why Selected?** Starting with a pilot group lets you test the experience and catch problems before enabling SSPR for everyone.

---

### Subtask 1: Configure Authentication Methods

**Goal:** Decide how users prove their identity before resetting a password.

1. Opened **Authentication methods** under Password reset.
2. Set **Number of methods required to reset** to `1`.
3. Selected the available methods: **Email**, **Mobile phone**, and **Mobile app code**.
4. Selected **Save**.

![Authentication methods page](screenshots/05-authentication-methods.png)
*Password reset → Authentication methods*

![Methods selected](screenshots/06-methods-selected.png)
*One method required; email, mobile phone, and mobile app code available*

![Methods saved](screenshots/07-auth-methods-saved.png)
*Authentication methods saved*

> 💡 **Good to know:** A password is not an option for verifying identity during a reset. If Security Questions are used, you must also set how many questions each user must register and answer.

---

### Subtask 2: Configure Registration

**Goal:** Make sure users have verification methods on file before they ever need to reset a password.

1. Opened **Registration** under Password reset.
2. Set **Require users to register when signing in?** to **Yes**.
3. Set **Number of days before users are asked to re-confirm their authentication information** to `90`.
4. Selected **Save**.

![Registration settings](screenshots/08-registration-settings.png)
*Registration required at sign-in; re-confirmation every 90 days*

![Registration saved](screenshots/09-registration-saved.png)
*Registration settings saved*

---

### Subtask 3: Configure Notifications

**Goal:** Keep users and administrators informed when passwords are reset.

1. Opened **Notifications** under Password reset.
2. Left **Notify users on password reset?** at the default, **Yes**.
3. Set **Notify all admins when other admins reset their password?** to **Yes**.
4. Selected **Save**.

![Notification settings](screenshots/10-notification-settings.png)
*User and admin notifications enabled*

![Notifications saved](screenshots/11-notifications-saved.png)
*Notification settings saved*

---

## 🔑 Key Concepts

| Concept | Why it matters |
|---|---|
| **SSPR** | Lets users verify their identity and reset their own passwords without contacting IT |
| **Scoped rollout** | Enabling a feature for a pilot group first reduces risk |
| **Authentication methods** | The verification options a user can choose from during a reset |
| **Number of methods required** | One method is more convenient. Requiring two is stronger. |
| **Registration** | Users must register methods ahead of time, or they can't use SSPR when locked out |
| **Re-confirmation period** | Prompts users to keep their contact details current |
| **Reset notifications** | Alert users to unexpected resets, which can help spot account takeover |

---

## 🛡️ Security Practices Applied

- **Phased rollout:** SSPR was limited to a defined group rather than enabled tenant-wide.
- **Verified recovery:** Users must prove their identity with a registered method before resetting.
- **Up-to-date contact info:** The 90-day re-confirmation keeps recovery methods from going stale.
- **Visibility into privileged actions:** Notifying admins about other admins' resets adds oversight to a high-risk activity.

---

## 💡 Key Takeaways

- SSPR improves both security and productivity: users recover access faster, and the help desk handles fewer routine tickets.
- Registration is what makes SSPR work. Without registered methods, a locked-out user can't reset anything.
- Authentication method choices are a balance between convenience and strength. Requiring two methods is generally the more secure option.
- Notifications for admin password resets are a simple control that adds oversight over powerful accounts.

---

## 🔗 References

- [How Microsoft Entra SSPR works](https://learn.microsoft.com/entra/identity/authentication/concept-sspr-howitworks)
- [Enable self-service password reset tutorial](https://learn.microsoft.com/entra/identity/authentication/tutorial-enable-sspr)
- [Authentication methods in SSPR](https://learn.microsoft.com/entra/identity/authentication/concept-authentication-methods)

---

<sub>Completed in a Microsoft training lab environment. Tenant names and identifiers are redacted from all screenshots.</sub>
