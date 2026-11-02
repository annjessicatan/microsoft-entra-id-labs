# 🔒 Lab 3: Password Protection in Microsoft Entra ID

[⬅ Previous: Lab 2 – Group Management](../02-group-management/README.md) &nbsp;|&nbsp; [Main README](../README.md) &nbsp;|&nbsp; [Next: Lab 4 – SSPR ➡](../04-sspr/README.md)

![Microsoft Entra ID](https://img.shields.io/badge/Microsoft-Entra%20ID-0078D4?logo=microsoft&logoColor=white)
![Security](https://img.shields.io/badge/Focus-Credential%20Security-red)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Tasks](https://img.shields.io/badge/Tasks-1%20of%201-brightgreen)

> **Scenario:** Weak and guessable passwords are one of the easiest ways into an organization. At Contoso, I configured Microsoft Entra password protection to slow down brute-force attempts and to block passwords that include company-specific words attackers would try first.

---

## 📋 At a Glance

| | |
|---|---|
| **Platform** | Microsoft Entra admin center |
| **Focus area** | Credential hardening and attack prevention |
| **Tasks completed** | 1 |
| **Core skills** | Smart lockout, custom banned password list, enforcement modes |

### 🏆 Outcomes

- ✅ Configured **custom smart lockout**: lockout after **5** failed attempts, for **30 seconds**
- ✅ Enabled a **custom banned password list** with `Contoso`, `London`, and `Widget`
- ✅ Set the policy mode to **Enforced** so the rules are actively applied, not just logged
- ✅ Saved and verified the configuration

---

## 🗺️ Lab Workflow

```
Open Password protection ──► Set smart lockout ──► Add banned words ──► Enforce mode ──► Save
```

---

## 🧭 Walkthrough

### Task 1: Configure Smart Lockout and Custom Banned Passwords

**Goal:** Reduce the risk of password attacks with two controls: limiting repeated login failures and blocking predictable passwords.

#### Step 1: Open Password protection

1. Signed in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Went to **Protection → Authentication methods → Password protection**.

![Authentication methods menu](screenshots/01-authentication-methods-menu.png)
*Protection → Authentication methods*

![Password protection page](screenshots/02-password-protection-page.png)
*Password protection settings page*

#### Step 2: Configure custom smart lockout

| Setting | Value | Purpose |
|---|---|---|
| **Lockout threshold** | `5` | Number of failed sign-ins before the account locks |
| **Lockout duration (seconds)** | `30` | How long the account stays locked once the threshold is reached |

![Smart lockout values](screenshots/03-smart-lockout-values.png)
*Lockout threshold set to 5 and duration to 30 seconds*

#### Step 3: Create a custom banned password list

1. Set **Enforce custom list** to **Yes**.
2. Added three organization-specific terms:

| Banned term | Why it's banned |
|---|---|
| `Contoso` | The company name |
| `London` | The company's location |
| `Widget` | The company's product |

![Custom banned list](screenshots/04-custom-banned-list.png)
*Custom banned password list with Contoso, London, and Widget*

#### Step 4: Enforce and save

1. Set **Mode** to **Enforced**.
2. Selected **Save**.

![Mode enforced](screenshots/05-mode-enforced.png)
*Mode set to Enforced*

![Settings saved](screenshots/06-settings-saved.png)
*Configuration saved successfully*

---

## 🔑 Key Concepts

| Concept | Why it matters |
|---|---|
| **Smart lockout** | Locks sign-ins after repeated failures, which slows brute-force and password-spray attacks |
| **Lockout threshold** | The number of failed attempts allowed. A lower number is stricter but may lock out legitimate users who mistype. |
| **Lockout duration** | How long the lockout lasts. A longer duration slows attackers more but affects users more. |
| **Custom banned password list** | Blocks organization-specific words that attackers are likely to guess |
| **Global banned password list** | A Microsoft-maintained list of commonly used weak passwords, applied automatically |
| **Enforced vs. Audit mode** | Enforced blocks banned passwords. Audit only logs them, which is useful for testing impact first. |

> 💡 **How the banned list works:** Banned terms are blocked as a whole or as part of a password. Microsoft Entra also normalizes common character substitutions (for example, `0` for `o`), so simple variations of a banned word are caught too.

---

## 🛡️ Security Practices Applied

- **Defense against brute force:** Limiting failed attempts makes automated guessing impractical.
- **Context-aware protection:** Banning company-specific words closes a gap that generic password rules miss.
- **Enforcement over observation:** The policy was set to Enforced so the protection is active.
- **Balancing security and usability:** The lockout values stop attackers without keeping real users locked out for long.

---

## 💡 Key Takeaways

- Strong passwords aren't only about length and complexity. Predictable, company-related words are among the first things an attacker tries.
- Smart lockout is a trade-off. The threshold and duration should deter attackers without disrupting legitimate users.
- Audit mode is a safe way to measure the impact of a banned list before enforcing it in a real environment.
- Password protection works best alongside MFA and Conditional Access, which the next labs cover.

---

## 🔗 References

- [Microsoft Entra Password Protection](https://learn.microsoft.com/entra/identity/authentication/concept-password-ban-bad)
- [Protect accounts from attacks with smart lockout](https://learn.microsoft.com/entra/identity/authentication/howto-password-smart-lockout)
- [Eliminate bad passwords using Microsoft Entra Password Protection](https://learn.microsoft.com/entra/identity/authentication/howto-password-ban-bad-on-premises-operations)

---

<sub>Completed in a Microsoft training lab environment. Tenant names and identifiers are redacted from all screenshots.</sub>
