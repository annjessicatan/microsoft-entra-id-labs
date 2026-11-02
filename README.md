# 🔐 Microsoft Entra ID: Identity & Access Management Labs

![Microsoft Entra ID](https://img.shields.io/badge/Microsoft-Entra%20ID-0078D4?logo=microsoft&logoColor=white)
![Labs](https://img.shields.io/badge/Labs-6%20Completed-success)
![Level](https://img.shields.io/badge/Level-Beginner-blue)
![Focus](https://img.shields.io/badge/Focus-IAM%20%26%20Security-red)

> Hands-on labs covering the core identity and access management (IAM) tasks an IAM specialist performs in Microsoft Entra ID: managing users and groups, hardening authentication, and enforcing access policies.

---

## 📌 Overview

This repository documents six hands-on labs I completed in Microsoft Entra ID, based on the Microsoft Learn interactive labs module. The labs follow a realistic scenario: **I joined Contoso, a technology company, as an entry-level Identity and Access Management specialist**. My job is to make sure employees and external partners have the right access to the right resources, while keeping company systems secure.

Each lab has its own write-up with step-by-step actions, screenshots, and key takeaways. Use the table below to jump to the one you want.

---

## 🧪 Labs at a Glance

| # | Lab | What I Did | Key Skills | Details |
|---|-----|-----------|------------|---------|
| 1 | **User Management** | Created a user, assigned a license, invited an external (guest) user, assigned a role, and bulk-imported users | User lifecycle, licensing, B2B collaboration, RBAC, bulk operations | [View Lab 1](./01-user-management/README.md) |
| 2 | **Group Management** | Created a Security group and a Microsoft 365 group, added members, and assigned licenses to groups | Group types, membership management, group-based licensing | [View Lab 2](./02-group-management/README.md) |
| 3 | **Password Protection** | Enabled password protection, set smart lockout values, and reviewed custom banned passwords | Credential hardening, brute-force mitigation | [View Lab 3](./03-password-protection/README.md) |
| 4 | **Self-Service Password Reset (SSPR)** | Enabled SSPR, configured authentication methods, and scoped it to designated users | Helpdesk workload reduction, user empowerment, scoped rollout | [View Lab 4](./04-sspr/README.md) |
| 5 | **Multifactor Authentication (MFA)** | Enabled and disabled per-user MFA, reviewed Trusted IPs, and configured MFA lockout settings | Strong authentication, access hardening, account protection | [View Lab 5](./05-mfa/README.md) |
| 6 | **Conditional Access** | Built a policy to block access to Microsoft Sway and tested it with the **What If** tool | Policy design, Zero Trust principles, pre-deployment testing | [View Lab 6](./06-conditional-access/README.md) |

---

## 🎯 Skills Demonstrated

**Identity Management**
- Creating, licensing, and managing cloud user accounts
- Inviting and managing external (guest) users
- Bulk user import via CSV
- Creating and managing Security and Microsoft 365 groups

**Access Control**
- Assigning Microsoft Entra roles (least-privilege mindset)
- Group-based license assignment

**Authentication & Security**
- Password protection, smart lockout, and custom banned password lists
- Self-Service Password Reset configuration
- Per-user Multifactor Authentication and lockout settings
- Conditional Access policies and What If analysis

---

## 🛠️ Tools & Technologies

- Microsoft Entra ID (Microsoft Entra admin center)
- Microsoft 365
- Conditional Access
- Microsoft Entra Password Protection
- Self-Service Password Reset
- Microsoft Entra Multifactor Authentication

---

## 🧭 Scenario: Contoso Onboarding

| Phase | Responsibility |
|-------|----------------|
| **Week 1** | Set up user accounts, licenses, guest access, and roles |
| **Week 2** | Organize users into groups and streamline resource access |
| **Week 3** | Strengthen authentication with password protection, SSPR, and MFA |
| **Week 4** | Enforce access controls with Conditional Access |

---

## 📂 Repository Structure

```
.
├── README.md
├── 01-user-management/
│   ├── README.md
│   └── screenshots/
├── 02-group-management/
│   ├── README.md
│   └── screenshots/
├── 03-password-protection/
│   ├── README.md
│   └── screenshots/
├── 04-sspr/
│   ├── README.md
│   └── screenshots/
├── 05-mfa/
│   ├── README.md
│   └── screenshots/
└── 06-conditional-access/
    ├── README.md
    └── screenshots/
```

---

## 💡 Key Takeaways

- **Identity is the new security perimeter.** Access decisions start with who the user is and how they authenticated.
- **Layered controls work best.** Password protection, SSPR, MFA, and Conditional Access each cover a different gap.
- **Test before you enforce.** The What If tool lets you validate a Conditional Access policy before it affects real users.
- **Groups scale; individual assignments don't.** Group-based licensing and access reduce admin overhead and errors.

---

## 📚 Related Certifications

These labs build foundational knowledge relevant to:
- **SC-900:** Microsoft Security, Compliance, and Identity Fundamentals
- **SC-300:** Microsoft Identity and Access Administrator

---

## 🔗 Resources

- [Microsoft Entra documentation](https://learn.microsoft.com/entra/)
- [Microsoft Learn: Microsoft Entra interactive labs](https://learn.microsoft.com/training/)

---

## 👤 About Me

**[Your Name]**
Aspiring IAM / Cloud Security professional building hands-on experience in Microsoft identity and security.

- 💼 LinkedIn: [your-linkedin-url](https://linkedin.com/in/your-profile)
- 📧 Email: your.email@example.com
- 🌐 Portfolio: [your-site.com](https://your-site.com)

---

⭐ If you found this helpful, feel free to star the repo!

> *These labs were completed in a sandbox/training environment. No real organizational data is shown.*
