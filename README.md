

# 🛠️ Active Directory Lab

![AD Lab Diagram](https://github.com/user-attachments/assets/6971d2d4-d01b-4e98-943e-7fcb62fed4ec)

## 📖 Lab Overview

This lab simulates a small enterprise Active Directory environment using **Windows Server 2022** and **Windows 10**. It demonstrates key IT administration tasks and foundational skills in:

* Active Directory domain setup
* User and group management
* Organizational Unit (OU) structuring
* Group Policy Object (GPO) configuration
* File share permissions and access control
* Account lockout and password recovery

**Lab Goals:**

* Configure a Domain Controller (DC) and join a Windows 10 client
* Create and manage users, OUs, and security groups
* Apply GPOs for user policies (desktop wallpaper, lockout policy)
* Test file share permissions and group-based access control

---

## 🖥️ Environment

| Component | OS                  | Role                |
| --------- | ------------------- | ------------------- |
| `DC01`    | Windows Server 2022 | Domain Controller   |
| `WS01`    | Windows 10          | AD-connected client |

* Both machines run on **VirtualBox** with NAT networking
* Domain: `LAB.local`
* 4 custom users created for testing policies and permissions

---

## 🧠 Key Skills Demonstrated

* ✅ Domain Controller setup and AD DS installation
* ✅ OU creation and user management
* ✅ Security group creation and shared folder permissions
* ✅ GPO creation and targeted application (wallpaper, account lockout)
* ✅ Simulation of real-world scenarios: account lockout & recovery

---

## 👥 Users, Groups & Access Control

* Department-based OUs: `Engineering`, `Management`, `IT`
* Nested OU for administrators
* Security group `EngineeringShare` with controlled access to shared folder
* Enforced **least privilege access** with testing of denied permissions

---

## 🔐 GPOs & Policy Enforcement

* Custom desktop wallpaper applied for **Engineering OU** users
* Domain-wide account lockout policy (3 invalid login attempts)
* Demonstrated account unlock and password reset workflow

---

## 💡 Lab Outcomes

By completing this lab, the following skills were gained:

* Enterprise Active Directory administration
* Practical application of OUs, groups, and GPOs
* File share management and permission testing
* Understanding domain-joined client workflows
* Hands-on troubleshooting for account lockouts


## 🗂️ Table of Contents

1. [Lab Preparation](https://github.com/Drevon-Shaw/active-directory-lab-part-1-/blob/main/Labprep.md)
2. [Create Users and Organizational Units (OUs)](https://github.com/Drevon-Shaw/active-directory-lab-part-1-/blob/main/03_UsersAndOUs.md)
3. [Create Group Policy Objects (GPOs)](https://github.com/Drevon-Shaw/active-directory-lab-part-1-/blob/main/04_GPOs.md)
4. [Account Lockout Policy & Password Reset](https://github.com/Drevon-Shaw/active-directory-lab-part-1-/blob/main/05_AccountLockout.md)
5. [Lab Summary](https://github.com/Drevon-Shaw/active-directory-lab-part-1-/blob/main/06_LabSummary.md)

### 📌 How to Use This Table of Contents

- **Click on any of the above links** to navigate directly to that section.
- **Follow the steps in order** to set up and configure your Active Directory environment.
- **Ensure all prerequisites are met** as outlined in the Lab Preparation section before proceeding.




































































