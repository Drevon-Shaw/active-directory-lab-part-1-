# 🛠️ AD Lab - Installing Active Directory

## 📌 Objective
Install Active Directory Domain Services (AD DS) on Windows Server 2022 and promote the server to a Domain Controller.

---

## 🧩 Step 1: Install AD DS Role

1. Open **Server Manager** → **Manage** → **Add Roles and Features**.
2. Select **Role-based or feature-based installation**.
3. Choose your server (**DC01**) and click **Next**.
4. Select **Active Directory Domain Services**, click **Next**.
5. Confirm installation and click **Install**.
6. Wait for the installation to complete.

**Screenshot:**
![6](https://github.com/user-attachments/assets/5491173c-d121-41b5-898b-445b3a6f4f4d)

---

## 🧩 Step 2: Promote to Domain Controller

1. After installation, click **Promote this server to a domain controller**.
2. Select **Add a new forest** and set the root domain as `LAB.local`.
3. Set a secure **Directory Services Restore Mode (DSRM) password**.
4. Review options and click **Install**.
5. The server will automatically reboot after promotion.

**Screenshot:**
![9](https://github.com/user-attachments/assets/fa28247b-ceee-4031-92d4-d2e335123b01)

---

## ✅ Outcome

* `DC01` is now a Domain Controller for `LAB.local`.
* Ready for adding users, OUs, and configuring GPOs.
