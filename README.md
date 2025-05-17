# 🛠️ Active Directory Lab – Part 1

![ChatGPT Image May 16, 2025, 03_07_38 PM](https://github.com/user-attachments/assets/c3d535dd-8190-4df3-a551-48db666d5964)


## 📖 Overview

This project simulates a small enterprise Active Directory environment using Windows Server 2022 and Windows 10. It is designed to demonstrate user and group management, domain joining, and Group Policy configuration.

**Lab Goals:**
- Set up a Windows Server 2022 Domain Controller
- Join a Windows 10 machine to the domain
- Create Active Directory users and groups
- Apply Group Policy Objects (GPOs) to manage user restrictions
- Reset passwords and simulate basic administrative tasks

This lab sets the foundation for Part 2, which will include:
- SIEM integration with Splunk
- Adversary simulation using Atomic Red Team
- Security automation using LimaCharlie (EDR) and Tines (SOAR)

---

## 🖥️ Lab Setup

| Component         | OS                  | Role                     |
|------------------|---------------------|--------------------------|
| `DC01`           | Windows Server 2022 | Domain Controller        |
| `Client01`       | Windows 10          | AD-connected client PC   |

- Both machines run on VirtualBox
- Networking configured using **Internal Network** mode
- Domain: `corp.local`
- 4 Active Directory users created for testing group policies and user restrictions


## 🧱 Configuring Server as Domain Controller

Before we begin, make sure Windows Server 2022 is fully installed and running.

➡️ **Download ISOs (Windows Server + Windows 10)**  
You can obtain official ISO files from Microsoft:  
[https://www.microsoft.com/en-us/evalcenter/](https://www.microsoft.com/en-us/evalcenter/)

---

### 🔧 Step 1: Rename the Server

We’ll start by renaming the default computer name to `DC01`. In this instance the default computer is the Windows 2022 server. 

1. Click **Start** and search for `View your PC name`
2. Click **Rename this PC**
3. Enter `DC01` and click **Next**
4. Restart the system when prompted.


---

### 🏗️ Step 2: Install Active Directory Domain Services (ADDS)

After renaming and restarting the server, we’ll configure it to act as a Domain Controller.

1. Open **Server Manager**
2. Click **Manage > Add Roles and Features**
  ![DC1](https://github.com/user-attachments/assets/ad434233-28fe-4f0a-9d4a-8dc9217e39b8)
4. In the wizard, select **Role-based or feature-based installation**
   ![2](https://github.com/user-attachments/assets/3cf4e01b-d727-46ea-a2c4-d9f3ebf3d90a)
6. Choose the server (`DC01`) from the server pool
   ![3](https://github.com/user-attachments/assets/132d7a7d-ce86-40e5-a397-a967c446067a)
8. On the **Server Roles** screen, check **Active Directory Domain Services** This will allow us to act as the domain Service 
  ![4](https://github.com/user-attachments/assets/6538fe66-486e-4803-b001-c9300c3c6e9f)
10. A popup will appear — click **Add Features**
    ![5](https://github.com/user-attachments/assets/f55de43b-0d81-40f4-875d-631a10fb0e96)
12. Click **Next** through the rest of the wizard
14. On the final screen, check **Restart the destination server automatically if required**
16. Click **Install** and wait for installation. it will take a minute 
![6](https://github.com/user-attachments/assets/5491173c-d121-41b5-898b-445b3a6f4f4d)


---

### 🏁 Step 3: Promote Server to Domain Controller

Once installation finishes click: 

> **Promote this server to a domain controller**
![6](https://github.com/user-attachments/assets/cbc72433-73fd-4f3e-8849-66ab4f6e0d3a)
1. Choose **"Add a new forest"**
2. Enter a **Root domain name** (e.g., `LAB.local`) we are going to use LAB.local since its a local lab but you can change it to anything you want .
   ![7](https://github.com/user-attachments/assets/9f3717e2-ee0e-41a3-b6bf-d42c74a4ee11)
4. Click **Next** to proceed to the Domain Controller Options screen.
   -For this Screen its going to ask you to make a password for restore mode just choose any password perferabbly the same one you made for the windows server.
   -Continue to click next and leave all the data bases and setting paths and options as deafult.
5. Let it run through the prerequisites check and make sure everyhting is okay. It will take a few seconds and dont worry about the warnings that pop up.
   ![9](https://github.com/user-attachments/assets/fa28247b-ceee-4031-92d4-d2e335123b01)
6. Click install and let the VM reboot.


---

### ✅ Step 4: Verify Domain Login

After `DC01` restarts, you should now see the option to log in with the **domain administrator** account.

1. At the log‑in screen, confirm the sign‑in field shows `LAB\Administrator`
   ![10](https://github.com/user-attachments/assets/2a6b43f1-35bc-4c35-820a-d604bcc503f6)
3. Enter the same password you set during installation
4. If you successfully reach the desktop, the domain controller is live 🎉

---

### 🔐 Step 5: Add Active Directory Certificate Services (AD CS)

To enable secure protocols for future labs, we’ll install the Certificate Services role.

1. Open **Server Manager**
2. Click **Manage > Add Roles and Features**
3. Select **Role‑based or feature‑based installation** and click **Next**
4. Choose the server (`DC01`) and click **Next**
6. On **Server Roles**, check **Active Directory Certificate Services**
7. In the pop‑up window, click **Add Features**
   ![11](https://github.com/user-attachments/assets/01991951-2440-413c-a5e5-46541f010fec)

8. Click **Next** through all remaining pages
9. Check **Restart the destination server automatically if required**
10. Click **Install**

📸 *Screenshot: Selecting AD CS Role*  
![ADCS Role](images/add-adcs-role.png)

---

### ⚙️ Step 6: Configure Active Directory Certificate Services

When installation completes and the server restarts, you’ll see a notification to configure the role:

1. In **Server Manager**, click **Configure Active Directory Certificate Services**  
   ![Configure Notification](images/configure-adcs-notify.png)
2. Use the default (domain) credentials and click **Next**
3. Check **Certification Authority** and click **Next**  
   ![Select CA](images/select-ca.png)
4. Accept all remaining defaults, clicking **Next** on each screen
5. On the final page, click **Configure** and wait for the green ✓ confirmation
6. Click **Close** and allow the server to restart if prompted


---

> You now have a fully functional **Domain Controller** with **Active Directory Certificate Services** installed, ready for advanced tasks in later parts of the lab.


---

### 👥 Step 7: Create Domain Users & Organize AD Structure

Now we’ll create real users in Active Directory and organize them into a custom Organizational Unit (OU).

---

### 🧭 Navigate to Active Directory Users and Computers

1. Open **Server Manager**
2. Click **Tools > Active Directory Users and Computers**
![13](https://github.com/user-attachments/assets/ab6a9f68-12f4-45e2-8437-27b3fc059054)

---

### 🗂️ Explore the Domain Tree

- You should see the domain listed (e.g., `lab.local`)
- Expand the domain to see:
  - **Computers** (currently empty)
  - **Domain Controllers** (you’ll see `DC01`)
  - **Users** (contains default system users/groups)

---

### 📁 Create a New Organizational Unit

To keep things tidy, let’s move all default groups into a separate OU.

1. Right-click on the domain (e.g., `lab.local`)
2. Hover over **New > Organizational Unit**
![user account dashboard](https://github.com/user-attachments/assets/e06b599c-acbd-45a7-8659-7eee6c631a91)
4. Name it `Groups`
![image](https://github.com/user-attachments/assets/a0b3ce87-6150-47d4-9d61-79a7e5d28d92)


---

### 📦 Move Default Groups into the OU

1. Go to the **Users** folder
2. Hold **Shift** and click to select all group objects (not users)
   ![image](https://github.com/user-attachments/assets/d8e38241-b7a6-4e04-a477-f3170364fed5)
4. Right-click > **Move**, and select the `Groups` OU
5. Click **Yes** on the warning prompt
6. Now you can see only the guest and admin is left
   



This keeps your **Users** container clean and easy to manage.

---

### 👑 Review the Built-In Administrator Account

You’ll now see only two accounts in `Users`:
- `Administrator`
- `Guest`
![image](https://github.com/user-attachments/assets/862d4046-3a9b-492b-8e26-e0f0c09c44fc)

The **Administrator** account is the domain's top-level account — it belongs to multiple powerful groups including **Domain Admins**, **Enterprise Admins**, and more. It’s like having the keys to the castle.


> ⚠️ Best practice is to avoid using this account for everyday activity.

---

### 🙋 Create New Domain Users

Let’s create domain users that we’ll later use to log in from our Windows 10 client.

1. Right-click anywhere in the `Users` container
2. Click **New > User**
3. Enter a first and last name (e.g., `nelson mandela`)
4. Set the user logon name as the first initial + last name (e.g., `nmandela`)
![16](https://github.com/user-attachments/assets/af42ac59-3227-45ed-9691-fa6a97babce2)

6. Click **Next**

---

### 🔐 Set Password

1. Set a password for the account (you can use the same for all in this lab)
2. Check **Password never expires** (for lab convenience)
3. Click **Next**, then **Finish**
![image](https://github.com/user-attachments/assets/f707e364-5b30-4479-af80-0a5c79a06cf2)

---

### ➕ Copy to Create More Users

Instead of starting from scratch, you can **right-click your first user > Copy**, and reuse the settings.

- Create 3 additional users using this method
- Use the same password, different names/logins (e.g., `kmahomes`, `tbrady`, `jjallen`)
![17](https://github.com/user-attachments/assets/0ef4f137-42a3-42ab-b1a7-c1c30c9fa298)
These are all the users I created 
---

> ✅ You now have **4 custom users** added to your domain — ready to be used for testing group policies and login behavior from other VMs.








