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





