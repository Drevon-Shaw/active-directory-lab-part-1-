

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


## 🗂️ Lab Table of Contents

1. [📖 Lab Overview](#-lab-overview)
2. [🖥️ Environment](#-environment)
3. [🔧 Step 1: Rename the Server](#-step-1-rename-the-server)
4. [🏗️ Step 2: Install Active Directory Domain Services](#-step-2-install-active-directory-domain-services)
5. [🏁 Step 3: Promote Server to Domain Controller](#-step-3-promote-server-to-domain-controller)
6. [✅ Step 4: Verify Domain Login](#-step-4-verify-domain-login)
7. [🔐 Step 5: Add Active Directory Certificate Services (AD CS)](#-step-5-add-active-directory-certificate-services-ad-cs)
8. [⚙️ Step 6: Configure Active Directory Certificate Services](#-step-6-configure-active-directory-certificate-services)
9. [3️⃣ Create Organizational Units (OUs)](#3-create-organizational-units-ous)
10. [3️⃣ Create Users & Security Groups](#3-create-users--security-groups)
11. [📂 Create and Secure a Shared Folder](#-create-and-secure-a-shared-folder)
12. [🔐 Customize Permissions for the Group](#-customize-permissions-for-the-group)
13. [🎨 Step 10: Apply a Group Policy Object (GPO) – Custom Wallpaper](#-step-10-apply-a-group-policy-object-gpo--custom-wallpaper)
14. [🔒 Step 11: Account Lockout Policy & Password Reset](#-step-11-account-lockout-policy--password-reset)
15. [💡 Lab Outcomes](#-lab-outcomes)



































































