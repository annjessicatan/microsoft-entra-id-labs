# 👥 Lab 2: Group Management in Microsoft Entra ID

[⬅ Previous: Lab 1 – User Management](../01-user-management/README.md) &nbsp;|&nbsp; [Main README](../README.md) &nbsp;|&nbsp; [Next: Lab 3 – Password Protection ➡](../03-password-protection/README.md)

![Microsoft Entra ID](https://img.shields.io/badge/Microsoft-Entra%20ID-0078D4?logo=microsoft&logoColor=white)
![Microsoft 365](https://img.shields.io/badge/Microsoft%20365-Admin%20Center-D83B01?logo=microsoft&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Tasks](https://img.shields.io/badge/Tasks-4%20of%204-brightgreen)

> **Scenario:** At Contoso, managing access user by user doesn't scale. I built the group structure to organize people by role and project: a collaboration group for a new project, an auto-populating group for guest users, and group-based licensing so access follows membership.

---

## 📋 At a Glance

| | |
|---|---|
| **Platform** | Microsoft Entra admin center, Microsoft 365 admin center |
| **Focus area** | Group management, dynamic membership, group-based licensing |
| **Tasks completed** | 4 (plus 2 sub-tasks) |
| **Core skills** | Microsoft 365 groups, Security groups, dynamic membership rules, group ownership, license assignment |

### 🏆 Outcomes

- ✅ Created a **Microsoft 365 group** (`Project23`) with assigned membership for a project team
- ✅ Built a **dynamic Security group** (`Guest Users`) that automatically collects every guest account in the tenant
- ✅ Added a member to a group using **two different methods**
- ✅ Delegated management by adding a **group owner**
- ✅ Assigned a **license to the whole group** instead of to individual users

---

## 🗺️ Lab Workflow

```
M365 group ──► Dynamic Security group ──► Add members ──► Add owner ──► Group license
  Task 1              Task 2                 Task 3          Task 4        Task 4 (subtask)
```

---

## 🧭 Walkthrough

### Task 1: Create a Microsoft 365 Group

**Goal:** Give a project team a shared group for collaboration.

1. Signed in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Went to **Groups → All groups → New group**.
3. Configured the group:

| Field | Value |
|---|---|
| Group type | Microsoft 365 |
| Group name | `Project23` |
| Description | Members of the new AI Simulation software, codename Project23 |
| Membership type | Assigned |

4. Under **Members**, selected **Bhogeswar Kalita**, then selected **Create**.

![New group menu](screenshots/01-new-group-menu.png)
*Groups → All groups → New group*

![Microsoft 365 group details](screenshots/02-m365-group-details.png)
*Project23 configured as a Microsoft 365 group with Assigned membership*

![Select members](screenshots/03-select-members.png)
*Adding Bhogeswar Kalita as a member*

![Group created](screenshots/04-group-created.png)
*Project23 created successfully*

---

### Task 2: Create a Dynamic Security Group

**Goal:** Automatically collect all guest users into one group, with no manual upkeep.

1. Went to **Groups → All groups → New group**.
2. Configured the group:

| Field | Value |
|---|---|
| Group type | Security |
| Group name | `Guest Users` |
| Description | All Guest users currently in the tenant |
| Membership type | Dynamic User |

3. Under **Dynamic user members**, selected **Add dynamic query** and built this rule:

| Property | Operator | Value |
|---|---|---|
| `userType` | Equals | `Guest` |

4. Saved the rule and selected **Create**.
5. Waited for the group to populate (it can take a couple of minutes), refreshed the list, and opened **Members** to confirm the guest user appeared.

![Security group details](screenshots/05-security-group-details.png)
*Guest Users set up as a Security group with Dynamic User membership*

![Dynamic query](screenshots/06-dynamic-query.png)
*Dynamic rule: userType Equals Guest*

![Guest Users created](screenshots/07-guest-users-created.png)
*Guest Users group created*

![Guest Users members](screenshots/08-guest-users-members.png)
*The External User from Lab 1 was added automatically by the rule*

> 💡 **Why it matters:** When a new guest is invited, they are added to this group automatically. Policies and access assigned to the group apply right away, with no admin action.

---

### Task 3: Add an Existing User to a Group

**Goal:** Add a user to a group using two different paths.

#### Method A: From the group

1. Opened **Groups → All groups → Project23 → Members**.
2. Selected **+ Add members**, marked **External User**, and chose **Select**.

![Add members](screenshots/09-add-members-project23.png)
*Project23 → Members → + Add members*

![Select External User](screenshots/10-select-external-user.png)
*Selecting External User*

![Members list](screenshots/11-members-list.png)
*Updated Project23 member list*

#### Method B: From the user

1. Opened **Users → All users → External User → Groups**.
2. Selected **+ Add memberships**, chose a group, and selected **Select**.

![User groups menu](screenshots/12-user-groups-menu.png)
*External User → Groups*

![Add memberships](screenshots/13-add-memberships.png)
*Adding a group membership from the user's profile*

> 💡 **When to use which:** Starting from the group is faster when adding many people to one group. Starting from the user is faster when giving one person access to several groups.

---

### Task 4: Add an Owner and License to a Group

**Goal:** Delegate group management and give members the services they need.

#### Add an owner

1. Opened **Project23 → Owners**.
2. Selected **+ Add owners**, marked **Bhogeswar**, and chose **Select**.
3. Confirmed the new owner appeared in the list.

![Owners menu](screenshots/14-owners-menu.png)
*Project23 → Owners*

![Add owner](screenshots/15-add-owner.png)
*Selecting Bhogeswar as an owner*

![Owner added](screenshots/16-owner-added.png)
*Owner successfully added*

> 💡 If no owner is specified, the tenant administrator is added as an owner automatically.

#### Assign a license to the group

1. Opened the [Microsoft 365 admin center](https://admin.microsoft.com) and went to **Billing → Licenses**.
2. Selected **Microsoft Power Automate Free**, then the **Groups** tab.
3. Selected **+ Assign licenses**, chose the **Project23** group, and selected **Assign**.
4. Refreshed the page to confirm the group license was added.

![Licenses page](screenshots/17-licenses-power-automate-free.png)
*Billing → Licenses → Microsoft Power Automate Free*

![Groups tab](screenshots/18-groups-tab-assign.png)
*Groups tab → + Assign licenses*

![Select Project23](screenshots/19-select-project23.png)
*Selecting the Project23 group*

![Group license assigned](screenshots/20-group-license-assigned.png)
*License assigned to the group*

---

## 🔑 Key Concepts

| Concept | Why it matters |
|---|---|
| **Microsoft 365 group** | Built for collaboration (shared mailbox, calendar, Teams, SharePoint) |
| **Security group** | Built for controlling access to resources and applying policies |
| **Assigned membership** | Members are added manually by an admin or owner |
| **Dynamic membership** | Members are added or removed automatically based on user attributes |
| **Group owners** | Let a project lead manage membership without tenant-wide admin rights |
| **Group-based licensing** | Licenses follow membership, so joiners get access and leavers lose it automatically |

---

## 🛡️ Practices Applied

- **Automation over manual upkeep:** A dynamic rule keeps guest membership accurate without admin effort.
- **Delegated administration:** Ownership moves day-to-day membership management to the people closest to the project.
- **Scalable licensing:** Assigning a license to a group avoids per-user assignments and reduces errors.
- **Right group for the job:** A Microsoft 365 group was used for collaboration and a Security group for access control.

---

## 💡 Key Takeaways

- Choosing the group type is a design decision: collaboration needs a Microsoft 365 group, while access control needs a Security group.
- Dynamic groups save time and reduce human error, especially for attributes like user type.
- Group-based licensing makes onboarding and offboarding easier, because membership changes handle licensing.
- The same task can often be done from more than one place in the portal, so it helps to know which is most efficient for the situation.

---

## 🔗 References

- [Manage groups in Microsoft Entra ID](https://learn.microsoft.com/entra/fundamentals/how-to-manage-groups)
- [Dynamic membership rules for groups](https://learn.microsoft.com/entra/identity/users/groups-dynamic-membership)
- [Assign licenses to groups](https://learn.microsoft.com/entra/identity/users/licensing-groups-assign)
- [Learn about groups and access rights](https://learn.microsoft.com/entra/fundamentals/concept-learn-about-groups)

---

<sub>Completed in a Microsoft training lab environment. Tenant names and identifiers are redacted from all screenshots.</sub>
