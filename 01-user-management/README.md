# 👤 Lab 1: User Management in Microsoft Entra ID

[⬅ Back to main README](../README.md) &nbsp;|&nbsp; [Next: Lab 2 – Group Management ➡](../02-group-management/README.md)

![Microsoft Entra ID](https://img.shields.io/badge/Microsoft-Entra%20ID-0078D4?logo=microsoft&logoColor=white)
![Microsoft 365](https://img.shields.io/badge/Microsoft%20365-Admin%20Center-D83B01?logo=microsoft&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Tasks](https://img.shields.io/badge/Tasks-5%20of%205-brightgreen)

> **Scenario:** As an entry-level IAM specialist at Contoso, I handled the full user onboarding lifecycle: creating an employee account, licensing it, inviting an external collaborator, delegating admin roles, and bulk-onboarding users from a CSV file.

---

## 📋 At a Glance

| | |
|---|---|
| **Platform** | Microsoft Entra admin center, Microsoft 365 admin center |
| **Focus area** | Identity lifecycle management & role-based access |
| **Tasks completed** | 5 (plus 2 sub-tasks) |
| **Core skills** | User provisioning, license assignment, B2B guest access, RBAC, bulk operations |

### 🏆 Outcomes

- ✅ Provisioned a new member account and **verified it by signing in** through an InPrivate session
- ✅ Assigned a **Microsoft Power Automate Free** license through the Microsoft 365 admin center
- ✅ Invited an **external guest user** with a custom invitation message
- ✅ Assigned roles using **two methods** and **two assignment types** (Eligible and Active, with a written justification)
- ✅ Onboarded multiple users at once with a **CSV bulk import**

---

## 🗺️ Lab Workflow

```
Create user ──► Verify sign-in ──► Assign license ──► Invite guest ──► Assign roles ──► Bulk import
   Task 1         Subtask 1           Task 2            Task 3          Task 4           Task 5
```

---

## 🧭 Walkthrough

### Task 1: Create a New User

**Goal:** Provision a cloud-only member account for a new employee.

1. Signed in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Navigated to **Users → All users → + New user → Create new user**.
3. Entered the basics: User principal name `BhogeswarK` and display name `Bhogeswar Kalita`. Mail nickname left as the default.
4. Saved the auto-generated password securely for the sign-in test.
5. On the **Properties** tab, set first name `Bhogeswar`, last name `Kalita`, and user type **Member**.
6. Set the **Usage location** (required before a license can be assigned).
7. Selected **Review + create → Create**.

![Navigate to New user](screenshots/01-new-user-menu.png)
*Navigating to All users → New user → Create new user*

![Basics tab](screenshots/02-user-basics.png)
*Basics tab: UPN and display name*

![Properties tab](screenshots/03-user-properties.png)
*Properties tab: first name, last name, and user type*

![Usage location](screenshots/04-usage-location.png)
*Usage location set (required for licensing)*

![Review and create](screenshots/05-review-create.png)
*Review + create*

![User created](screenshots/06-user-created.png)
*New user successfully created*

> 💡 **Member vs. Guest:** A *Member* is an internal user with full standard capabilities. A *Guest* is an external user with restricted default permissions.

#### Subtask: Verify the Account by Signing In

Opened an **InPrivate** window, signed in at the Entra admin center with the new credentials, and completed the MFA setup prompt. Testing as the end user confirms the account actually works rather than assuming it does.

![InPrivate sign-in](screenshots/07-inprivate-login.png)
*Signing in as the new user in an InPrivate window*

![Sign-in confirmed](screenshots/08-signin-confirmed.png)
*Successful sign-in confirmed*

---

### Task 2: Assign a License

**Goal:** Give the new user access to a Microsoft cloud service.

1. Opened the [Microsoft 365 admin center](https://admin.microsoft.com).
2. Went to **Billing → Licenses**.
3. Selected **Microsoft Power Automate Free**.
4. Chose **+ Assign licenses**, selected Bhogeswar Kalita, and selected **Assign**.
5. Confirmed the success message.

![Licenses page](screenshots/09-licenses-page.png)
*Billing → Licenses*

![Power Automate Free](screenshots/10-power-automate-free.png)
*Selecting the Microsoft Power Automate Free license*

![Assign license](screenshots/11-assign-license.png)
*Assigning the license to the user*

![License assigned](screenshots/12-license-success.png)
*License assigned successfully*

---

### Task 3: Invite an External User

**Goal:** Give an outside collaborator access to the tenant (B2B collaboration).

1. In the Entra admin center, went to **Identity → Users → All users → + New user**.
2. Chose **Invite external user**.
3. Entered the email `ExtUser@testemail.com`, display name `External User`, and a custom welcome message for the project.
4. Selected **Review + create → Create**.

![Invite external user](screenshots/13-invite-external-user.png)
*Selecting Invite external user*

![Guest details](screenshots/14-external-user-details.png)
*Guest email, display name, and invitation message*

![Guest created](screenshots/15-external-user-created.png)
*External user invited successfully*

---

### Task 4: Assign Roles to a User

**Goal:** Delegate permissions using the principle of least privilege, using two different methods.

#### Method A: From the user's profile (Eligible assignment)

1. Opened **Bhogeswar Kalita → Assigned roles → + Add assignment**.
2. Selected the **Attribute Definition Reader** role.
3. Set the assignment type to **Eligible**.
4. Selected **Assign**.

![Assigned roles](screenshots/16-assigned-roles.png)
*User's Assigned roles page*

![Eligible assignment](screenshots/17-attribute-definition-reader-eligible.png)
*Attribute Definition Reader set as an Eligible assignment*

#### Method B: From Roles & admins (Active assignment)

1. Went to **Identity → Roles & admins** and selected **Attribute Log Reader**.
2. Chose **+ Add assignment** and selected Bhogeswar Kalita as the member.
3. Set the assignment type to **Active**.
4. Entered a justification: *"User will be working as an Attribute log reader as their primary job."*
5. Selected **Assign**.

![Roles and admins](screenshots/18-roles-and-admins.png)
*Roles & admins page*

![Select member](screenshots/19-attribute-log-reader-select-member.png)
*Selecting the user for the Attribute Log Reader role*

![Active with justification](screenshots/20-active-justification.png)
*Active assignment with a written justification*

![Role assigned](screenshots/21-role-assignment-success.png)
*Role assignment completed*

> 💡 **Eligible vs. Active:**
> - **Eligible** means the user holds the role but must activate it when needed (just-in-time access, which reduces standing privilege).
> - **Active** means the role is in effect immediately. This fits a role needed as part of the user's daily job, and it requires a justification for auditability.

---

### Task 5: Bulk Import Users

**Goal:** Onboard many users at once instead of one at a time.

1. Went to **Users → All users → Bulk operations → Bulk create**.
2. Downloaded the CSV template to review the required fields (username, display name, initial password) and optional fields (such as department and usage location).
3. Edited the provided sample CSV in Notepad, replacing the placeholder domain with the tenant's actual domain, then saved it.
4. Uploaded the file in the Bulk create dialog and selected **Submit**.
5. Verified the new accounts in the **All users** list.

![Bulk create menu](screenshots/22-bulk-create-menu.png)
*Bulk operations → Bulk create*

![Download template](screenshots/23-download-template.png)
*Downloading the CSV template*

![Edit CSV](screenshots/24-edit-csv.png)
*Updating the domain in the CSV file*

![Upload CSV](screenshots/25-upload-csv.png)
*Uploading the CSV file*

![Submit success](screenshots/26-bulk-submit-success.png)
*Bulk creation submitted successfully*

![Users in list](screenshots/27-bulk-users-list.png)
*Bulk-created users now appear in the All users list*

---

## 🔑 Key Concepts

| Concept | Why it matters |
|---|---|
| **Member vs. Guest users** | Controls default permissions; guests enable secure external collaboration without creating internal accounts |
| **Usage location** | Must be set before a license can be assigned |
| **Licensing** | Determines which Microsoft services a user can access |
| **Eligible vs. Active roles** | Eligible assignments support just-in-time access and reduce standing privileges |
| **Role justification** | Creates an audit trail for why elevated access was granted |
| **Bulk operations** | Reduce manual effort and human error during large onboarding events |

---

## 🛡️ Security Practices Applied

- **Least privilege:** Roles were scoped to read-focused roles rather than broad admin roles.
- **Just-in-time access:** An Eligible assignment was used where continuous access wasn't needed.
- **Auditability:** A written justification was recorded for the Active role assignment.
- **Verification:** The new account was tested by signing in as that user.
- **Secure credential handling:** The temporary password was kept out of screenshots and documentation.

---

## 💡 Key Takeaways

- Account creation is only the first step of onboarding. Licensing, role assignment, and verification complete it.
- Choosing between Eligible and Active assignments is a security decision, not just a configuration option.
- Guest accounts let an organization collaborate with outside partners while limiting their default access.
- Bulk import is a major time-saver, but the CSV must be accurate before it's submitted, especially domain names and required fields.

---

## 🔗 References

- [Add or delete users in Microsoft Entra ID](https://learn.microsoft.com/entra/fundamentals/how-to-create-delete-users)
- [Assign licenses to users](https://learn.microsoft.com/entra/identity/users/licensing-groups-assign)
- [B2B collaboration overview](https://learn.microsoft.com/entra/external-id/what-is-b2b)
- [Assign Microsoft Entra roles](https://learn.microsoft.com/entra/identity/role-based-access-control/manage-roles-portal)
- [Bulk create users](https://learn.microsoft.com/entra/identity/users/users-bulk-add)

---

<sub>Completed in a Microsoft training lab environment. Tenant names, passwords, and identifiers are redacted from all screenshots.</sub>
