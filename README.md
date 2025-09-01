

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





















































# 🛠️ Active Directory Lab – Part 1


![AD lab diagram](https://github.com/user-attachments/assets/6971d2d4-d01b-4e98-943e-7fcb62fed4ec)


## 📖 Overview

This project simulates a small enterprise Active Directory environment using Windows Server 2022 and Windows 10. It is designed to demonstrate user and group management, domain joining, and Group Policy configuration.

**Lab Goals:**
- Set up a Windows Server 2022 Domain Controller
- Join a Windows 10 machine to the domain
- Create Active Directory users and groups
- Apply Group Policy Objects (GPOs) to manage user restrictions
- Reset passwords and simulate basic administrative tasks

---

## 🖥️ Lab Setup

| Component         | OS                  | Role                     |
|------------------|---------------------|--------------------------|
| `DC01`           | Windows Server 2022 | Domain Controller        |
| `WS01`           | Windows 10          | AD-connected client PC   |

- Both machines run on VirtualBox
- Networking configured using **NAT Network** mode
- Domain: `LAB.local`
- 4 Active Directory users created for testing group policies and user restrictions


## 🧱 Configuring Server as Domain Controller

Before we begin, make sure Windows Server 2022 and windows 10 is fully installed and running.

➡️ **Download ISOs (Windows Server + Windows 10)**  
You can obtain official ISO files from Microsoft:  
[https://www.microsoft.com/en-us/evalcenter/](https://www.microsoft.com/en-us/evalcenter/)

**THIS LAB WILL NOT BE GOING THROUGH THE PROCCESS OF INSTALLING VMS AND CONFIGURING THEM. IF NEEDED TO KNOW HOW TO DO THIS YOUTUBE IS GREAT. OR I WILL MAKE ANOTHER REPOSITORY ON HOW TO**
**VMWARE OR ORACLE VIRTUAL BOX IS FINE WHEN DOING THIS LAB. ALSO BE AWARE OF PC REQUIRMENTS BECAUSE WE WILL BE RUNNING 2 VMS AT THE SAME TIME**

---

### 🔧 Step 1: Rename the Server

We’ll start by renaming the default computer name to `DC01`. In this instance the default computer is the Windows 2022 server. 

1. Click **Start** and search for `View your PC name`
2. Click **Rename this PC**
3. Enter `DC01` and click **Next**
4. Restart the system when after.

---

### 🏗️ Step 2: Install Active Directory Domain Services 

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
3. Click **Next** to proceed to the Domain Controller Options screen.
   For this Screen its going to ask you to make a password for restore mode just choose any password perferabbly the same one you made for the windows server.
   Continue to click next and leave all the data bases and setting paths and options as deafult.

4. Let it run through the prerequisites, check and make sure everything is okay. It will take a few seconds, ignore the warnings.
![9](https://github.com/user-attachments/assets/fa28247b-ceee-4031-92d4-d2e335123b01)
5. Click install and let the VM reboot.

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

---

### ⚙️ Step 6: Configure Active Directory Certificate Services

When installation completes and the server restarts, you’ll see a notification to configure the role:

1. In **Server Manager**, click **Configure Active Directory Certificate Services**  
2. Use the default (domain) credentials and click **Next**
3. Check **Certification Authority** and click **Next**  
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

The **Administrator** account is the domain's top-level account  it belongs to multiple powerful groups including **Domain Admins**, **Enterprise Admins**, and more. It’s like having the keys to the castle.


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



---

### 🖥️ Step 8: Attach Windows 10 VM to the Domain

Before joining the domain, we need to ensure that both virtual machines (Windows Server and Windows 10) are on the same **NAT Network** and using proper static IP addresses.

---

### 🌐 Set Up NAT Network in VirtualBox

1. In **Oracle VirtualBox**, click **File > Tools > Network Manager**
2. Click **NAT Network > Create**
3. Rename the new network to `AD Network` or `Active Directory Network`
4. Leave the rest of the settings as default and click **Apply**
![18](https://github.com/user-attachments/assets/45cc50b4-78ea-4312-8413-9258744c3aaa)

---

### 🧾 VM Settings for Windows Server and Windows 10

1. Open **Settings** for both VMs
2. Under **System**, adjust RAM if needed just make sure it stays in the green zone. Remember we are now running 2 vms therefore you might need to lower it. 
3. Under **Network**, ensure **Adapter 1** is set to:
   - **Attached to**: NAT Network
   - **Name**: `AD Network`
![19](https://github.com/user-attachments/assets/a0583b10-9be7-478a-901a-494e2bde61a5)

---

### 🌍 Set a Static IP for the Domain Controller (DC01)

1. Start the Windows Server VM (`DC01`)
2. Open **Command Prompt** and run:
   ```
   ipconfig
   ```
3. Note the current IP address (e.g., `10.0.2.15`)
   
![20](https://github.com/user-attachments/assets/8bfe1a15-a917-4e77-984d-ebadda3a10a1)

4. Right click the network icon (bottom-right) > **Open Network & Internet Settings**
5. Click **Change Adapter Options**
6. Right click the adapter > **Properties**
![22](https://github.com/user-attachments/assets/696875c0-2002-4f02-bd45-d6b7b0255107)
8. Double-click **Internet Protocol Version 4 (TCP/IPv4)**
![23](https://github.com/user-attachments/assets/4fab1aec-9bf7-4bcf-892c-a96c7e2f9ba9)

   

Enter the following: Copy everyting we seen in the ipconfig command propmt
- **IP address**: `10.0.2.15`
- **Subnet mask**: `255.255.255.0`
- **Default gateway**: `10.0.2.1` *(if applicable)*
- **Preferred DNS server**: `127.0.0.1` the dns server we are setting to ourselves, because we are the host.
![24](https://github.com/user-attachments/assets/0951ebe2-4732-4f0c-9184-3766f409782c)




---

### 💻 Configure Windows 10 Client

1. Start the **Windows 10 VM**
2. Log in with your local user account
3. Change the PC name to `WS01`:
   - **Settings > System > About > Rename this PC**
   - Restart when prompted

![image](https://github.com/user-attachments/assets/15175925-9503-452b-8606-7834a89f1fb0)


4. Open **Command Prompt** and run:
   ```
   ipconfig
   ```

5. Go to **Network Settings > Change Adapter Options**
6. Set static IP like before:
   - **IP address**: `10.0.2.16` we are going to make the IPs sequential in this case 
   - **Subnet mask**: `255.255.255.0`
   - **Default gateway**: `10.0.2.1`
   - **Preferred DNS server**: `10.0.2.15` *(points to Domain Controller)*
**Be aware you IPs might be different than mine.**
---

### 🔗 Join the Domain from Windows 10

1. In **Settings**, search for **Access Work or School**
![26](https://github.com/user-attachments/assets/77d9f1fe-e6f3-4dfa-8e85-5775e6a4ccd3)
2. Click **Connect > Join this device to a local Active Directory domain**
3. Enter your domain (e.g., `LAB.local`)
![image](https://github.com/user-attachments/assets/292f76a7-742e-4857-b7b1-ca185e500ec9)
4. When prompted, enter:
   - **Username**: `Administrator`
   - **Password**: (the one set on DC01)
![image](https://github.com/user-attachments/assets/2284de4f-d087-4ff6-9fc7-2763528a54ef)


5. Restart when prompted

---

### 🔓 Log In as a Domain User

1. At the login screen, click **Other User**
2. Enter the credentials of one of your custom users (e.g., `ljackson`, `kmahomes`, etc.)
3. Format: `LAB\username`

---

### ✅ Confirm on the Domain Controller

1. Go back to `DC01`
2. Open **Active Directory Users and Computers**
3. Click on the **Computers** container
4. You should now see `WS01` listed — showing it's joined to the domain

![image](https://github.com/user-attachments/assets/70e51166-0d56-404c-85fb-f3517425d983)

---

> 🥳 Congratulations! Your Windows 10 client is now successfully joined to the domain and is ready for testing policies and user access in your lab.

---

### 🧱 Step 9: Organizational Units (OUs) and Groups

Let’s now dive deeper into structuring and managing users using **Organizational Units (OUs)** and **Security Groups**.

---

### 📁 What Are Organizational Units?

Organizational Units are used to organize Active Directory objects such as:
- Users
- Computers
- Groups
- Even other OUs

> 🔸 OUs are the smallest administrative units where you can assign Group Policies  
> 🔸 **OUs can contain groups, but groups cannot contain OUs**

---

### 🏗️ Create Department-Based Organizational Units

1. Go to **Tools > Active Directory Users and Computers**
2. Right-click your domain (`LAB.local`) > **New > Organizational Unit**
![28](https://github.com/user-attachments/assets/93ed0abd-e80e-41bd-ae01-5a88153e22f5)

4. Create the following OUs:
   - `Engineering`
   - `Management`
   - `IT`

![29](https://github.com/user-attachments/assets/6797cfd3-6a6b-4087-b925-31ed2dca93f2)


4. Move users into appropriate departments:
   - `ljackson` and `nmandela` → `Engineering`
   - `gowens` 'khamilton' → `Management`
   - `Administrator` → `IT`

![30a](https://github.com/user-attachments/assets/9a46496c-8763-435a-b864-902f2a7b9982) 
![30b](https://github.com/user-attachments/assets/0192ef75-4f8b-4a4b-9478-9c8cff2f4db6)
![30c](https://github.com/user-attachments/assets/7da91378-fecb-4491-9399-cd26d5fbec7e)


---

### 🗂️ Create a Nested Organizational Unit

You can create an OU inside another OU for more structure.

1. Right-click the `IT` OU > **New > Organizational Unit**
2. Name it `Administrators`
![31](https://github.com/user-attachments/assets/cb7ab4e6-24e7-458f-87e3-5e55e47a7680)


4. Move the `Administrator` account into the `Administrators` OU
![32](https://github.com/user-attachments/assets/1d387452-4865-4b96-a4a7-d6111e8db069)


---

### 👥 Lets Create a Group inside the engineeing OU 

1. Go to the `Engineering` OU
2. Right-click > **New > Group**
![33](https://github.com/user-attachments/assets/e55a9ac3-0ab4-417d-8bbe-bdf26e86a974)
4. Name the group: `EngineeringShare`
5. Make sure **Group type** is set to **Security**
![34](https://github.com/user-attachments/assets/3ee19ec3-a45d-434a-a701-d741aa4abd8e)

7. Click **OK**

---

### ➕ Add Members to the Group

1. Double-click `EngineeringShare` group
2. Go to the **Members** tab
3. Click **Add** and add:
   - `ljackson`
   - `nmandela`
   - `gowens` (from Management OU) you can add members from other OUs if they require access in this instance Gary from manangment would want access to the engineering group too.
![35](https://github.com/user-attachments/assets/0482789e-260d-453d-b5cf-0d4cbf703f9f)


---

### 📂 Create and Secure a Shared Folder

Now what we can do with this gorup is we’ll create a shared folder and restrict access to only the `EngineeringShare` group.

1. Go to **Server Manager > File and Storage Services > Shares**
![38](https://github.com/user-attachments/assets/0009c73e-b969-48af-91b6-6abe22cd2441)
3. On the right, under **Tasks**, click **New Share**
![40](https://github.com/user-attachments/assets/3eab63b9-3884-47a4-884b-20d06fb0972a)
5. Select **SMB Share - Quick**
![41](https://github.com/user-attachments/assets/4cfaa7f9-74c6-4ba8-ba93-850f2a80feeb)
7. Leave the default location in the `C:` drive
![42](https://github.com/user-attachments/assets/2548a301-a758-40cf-a375-85b56ac62793)
9. Name the share: `EngineeringShare`
![43](https://github.com/user-attachments/assets/06bb80e5-1a88-4a72-ab85-61fd2d0b78b7)
11. Note the share path: `\\DC01\EngineeringShare`

---

### 🔐 Customize Permissions for the Group

1. When you reach the **Permissions** page, click **Customize Permissions**
![44](https://github.com/user-attachments/assets/f08f634b-2a9e-49cb-ae86-020d8b3ce3b1)
3. Click **Disable Inheritance** > choose **Convert inherited permissions into explicit permissions**
   ![45](https://github.com/user-attachments/assets/d4509cba-6640-4746-86d7-3816286fbad5)
4. Remove existing users (as needed) as you can see we have more users than needed **I would remove both LAB\USERS**
5. Click **Add > Select a Principal** and add `EngineeringShare` This is the group we created.
![48](https://github.com/user-attachments/assets/d9e0764b-f8c0-4296-b079-1d47f60face4)
6. Grant **Read/Write** permissions
![49](https://github.com/user-attachments/assets/6b99f26f-4df4-4922-9732-3b4810842838)
7. Click **Apply > OK > Next > Create > Close** **make sure to apply the changes**

---

### 🧪 Access the Share from Windows 10 Client

1. Log into the Windows 10 VM using a user in the `EngineeringShare` group (e.g., `ljackson`) this varies depending on what users you have in the engennering group
2. Open **File Explorer**
3. Go to **Network**, find `DC01`, and open `EngineeringShare` **Remember to turn on network sharing, also both vms have to be active**
![52](https://github.com/user-attachments/assets/9d468c3b-afff-41b1-a60d-a6f55add427d)


You should now be able to open, create, and edit files in this shared folder.
![53](https://github.com/user-attachments/assets/0b7a9240-9f60-406d-8a58-c1577be1a3be)
![54](https://github.com/user-attachments/assets/38fc93cf-4a35-47f7-84f9-718af3e706ba)



---

### 💾 Optional: Map Network Drive **This is a common task used by IT administrators for easier access to shared files and folders**

To map the shared folder as a drive letter:

1. Open **This PC**
2. Right-click on blank space > **Map Network Drive**
![55](https://github.com/user-attachments/assets/9f7c8fe6-4d19-42b0-b5d7-aa00c336a094)
4. Choose a drive letter (e.g., `Z:`)
5. Enter the folder path: `\\DC01\EngineeringShare`
![56](https://github.com/user-attachments/assets/ddabe20c-4ba4-407a-b371-1474ec0e1e12)

7. Click **Finish**
8. Now the EngineeringShare folder is showing up like a regular driv eon your computer

![57](https://github.com/user-attachments/assets/adc8dd0e-5d6a-4cb4-968c-69c21a490754)


   ---

### ❌ Test Access Denial for Non-Group Users

To confirm our permission settings are working correctly, log into a user **not** in the `EngineeringShare` group (e.g., someone from the `Management` OU).

1. Log into the Windows 10 VM with a different user (e.g., `gowens`)
![58](https://github.com/user-attachments/assets/5ed9cea8-709f-4217-8e37-d526e15f480e)
2. Open **File Explorer**
3. Go to **Network > DC01**

You will see that access to `EngineeringShare` is denied:

![59](https://github.com/user-attachments/assets/75dd9786-b982-4948-9845-bd1921f43bc8)



> 🔒 This confirms that only members of the `EngineeringShare` group can access the shared folder — enforcing proper access control using security groups and permissions.




> 🧠 Now you’ve successfully created OUs, organized users, created security groups, applied permissions, and validated access from the client side.


### 🎨 Step 10: Apply a Group Policy Object (GPO) – Custom Wallpaper

**Group Policy Objects (GPOs)** are a collection of policy settings used to control system behavior for users, groups, or computers in an Active Directory environment.

In this step, we’ll apply a custom desktop wallpaper **only** for the `Engineering` OU users using GPO.

---

### 🖼️ Create the Custom Wallpaper

1. Open **Paint** on your Domain Controller
2. Create a large background image and type:
   ```
   Engineering Dept
   ```
![61](https://github.com/user-attachments/assets/cdbe29fc-cabf-4eb0-84ae-000e7747909c)
   **Remember to center the words I made a mistake on mine you will see later**

4. Save the file to the **Desktop** as a `.jpg` named `engineering_wallpaper.jpg`

![60](https://github.com/user-attachments/assets/cabc4e3e-8628-47e2-88a1-609d0f873f38)


---

### 📂 Copy Wallpaper to Shared Location (NetLogon)

Administrators typically store wallpapers in the `NetLogon` share.

1. In **Server Manager**, go to:
   - **File and Storage Services > Shares**
2. Find the **NetLogon** share
![62](https://github.com/user-attachments/assets/e08d5ffa-8681-49c1-ac59-01d9e26995c2)

3. Right-click it > **Open Share**
4. Open your Desktop folder in another window
![63](https://github.com/user-attachments/assets/090440a1-fe5c-4e7a-b69c-b26cfafbad13)
5. Copy and paste the wallpaper into the `NetLogon` folder
![64](https://github.com/user-attachments/assets/3722199e-49b7-4cf0-9264-667d49d9ed0c)

![65](https://github.com/user-attachments/assets/0fc0565d-cb62-4af9-b5ed-e2d5f676a0e9)
6. Hold **Shift**, right-click the image file > **Copy as Path**
![66](https://github.com/user-attachments/assets/345e2635-bd81-41c3-beaf-38c625a78a80)


---

### ⚙️ Create and Link a GPO for Engineering

1. Go to **Tools > Group Policy Management**
2. Expand:
   - **Forest > Domains > lab.local > Engineering**
3. Right-click the `Engineering` OU > **Create a GPO in this domain, and Link it here...**
4. Name it: `SetEngineeringBackground`
![69](https://github.com/user-attachments/assets/317788fb-6e85-43b6-ac4c-edd424311543)
5. Right-click the new GPO > **Edit**
---

### 🛠️ Configure the Wallpaper Policy

1. In the **Group Policy Management Editor**, navigate to:
   - `User Configuration > Policies > Administrative Templates > Desktop > Desktop`
2. Double click **Desktop Wallpaper**
3. Choose **Enabled**
4. Paste the full path to the `.jpg` file from NetLogon (example):
   ```
   \\DC01\netlogon\engineering_wallpaper.jpg
   ```
![71](https://github.com/user-attachments/assets/557df7ed-5c1d-46ff-9023-5d6fcb66129c)

7. Click **OK**

---

### 💻 Test the GPO from Windows 10

1. Switch to your **Windows 10 VM**
2. Log in as a user from the **Engineering OU** (e.g., `ljackson`, `nmandela`)
3. You should now see the custom **Engineering Dept** wallpaper!
![72](https://github.com/user-attachments/assets/b038676c-b31f-4a76-85c2-134c5db18d1e)

   **THIS IS WHERE I MESSED UP BY NOT PLACING THE WORDING IN THE CENTER**
4. Now log in as a non-engineering user (e.g., from Management)
5. You’ll notice the **default wallpaper is still applied**, confirming the GPO was targeted correctly
![73](https://github.com/user-attachments/assets/cca2d847-d728-4bcd-8058-bdc95d551b33)


---

> 🧠 This demonstrates how to apply GPOs to specific user groups using OUs — a key concept in managing enterprise environments.

---


### 🔒 Step 11: Account Lockout Policy & Password Reset

In this final step, we’ll simulate a real-world account lockout scenario and walk through how to reset a locked-out user’s password in Active Directory.

---

### 🛠️ Create a Domain-Wide GPO for Account Lockout

1. On the Domain Controller, go to **Tools > Group Policy Management**
2. Right-click on your domain (`lab.local`) > **Create a GPO in this domain, and Link it here**
3. Name it: `AccountLockoutPolicy`
![75](https://github.com/user-attachments/assets/22e8f137-2c47-4647-8e2e-45ced7c3761a)
4. Right-click the GPO > **Edit**

---

### ⚙️ Configure the Lockout Threshold

1. Navigate to:
   - `Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy`
2. Double-click **Account lockout threshold**
![76](https://github.com/user-attachments/assets/e8f0b96e-d963-45a5-bf37-2bb4e94891d6)

3. Set to: `3` (invalid login attempts before lockout)
![77](https://github.com/user-attachments/assets/2e2fa917-0cd6-4b1f-802c-69674672cf90)
4. Click **Apply**
5. Right-click the GPO again > **Enforce**, to make sure it's active
![79](https://github.com/user-attachments/assets/23ecf288-545f-4414-8e88-8cbfc1662667)

---

### 🚫 Simulate a Locked-Out Account

1. On the **Windows 10** VM, log in as one of the users (e.g., `ljackson`)
2. Intentionally enter the **wrong password 3 times**

After the 3rd failed attempt, the user will be locked out:

![80](https://github.com/user-attachments/assets/e0b09fbc-0446-4cef-bf01-d17729bf46ed)


---

### 🔄 Reset and Unlock the Account in AD

1. On the Domain Controller, go to:
   - **Tools > Active Directory Users and Computers**
2. Use the **Search function** (top icon) to search for the locked-out user
   - Be sure to change scope to **Entire Directory**
![81](https://github.com/user-attachments/assets/15364292-07dd-4a6c-a8d1-6a03c3e7c496)
3. Right-click the user > **Properties > Account tab**
4. Uncheck **Password never expires**
![83](https://github.com/user-attachments/assets/7124c046-2bba-4d94-8eb1-8c0dd89e96ad)

5. Click **Apply**
![83](https://github.com/user-attachments/assets/d6f5de5c-ccec-483b-8c89-840c1ac70000)
**REMEMBER FOR THIS LAB WHEN WE CREATED THE PASSWORDS WE DID PASSWORD NEVER EXPIRES THEREFORE WE HAVE TO CHANGE IT IN ORDER FOR THE USER TO RESET HIS PASSWORD ON NEW LOG IN **
6. Now, right-click the user again > **Reset Password**
7. Enter a new password
8. Check:
   - ✅ **User must change password at next logon**
   - ✅ **Unlock the user’s account**
9. Click **OK**
![84](https://github.com/user-attachments/assets/7f6f099e-4d8a-4f6a-b2ca-9cd9dd7b2676)
---

### 🔓 Final Test – Log in Again and Change Password

1. Go back to the **Windows 10 VM**
2. Log in as the user with the **new password**
3. You’ll be prompted to **create a new password**
![85](https://github.com/user-attachments/assets/ea7ade54-6dcb-47e4-bb24-9c40dbe93040)
![86](https://github.com/user-attachments/assets/2cce6568-8e9c-4991-87ea-27a05dcf1512)

4. After that, you'll be successfully logged in

> 🎉 Congratulations! You’ve completed the full Active Directory Lab  including domain setup, user creation, OU organization, GPOs, file permissions, and account recovery!


---

## ✅ Lab Outro – Summary & Final Thoughts

In this Active Directory Lab, we built and explored a foundational enterprise-like domain environment using Windows Server 2022 and Windows 10. Here's a summary of what we accomplished:

### 🧠 What We Learned

- 🔧 **Configured a Domain Controller** using Active Directory Domain Services
- 💻 **Joined a Windows 10 machine** to the domain
- 👥 **Created and managed domain users** using Organizational Units 
- 📂 **Created security groups** and applied **file share permissions**
- 🔐 **Set Group Policy Objects** to enforce desktop backgrounds and lockout policies
- 🧪 **Simulated account lockout** scenarios and learned how to reset passwords and unlock users

These are **core tasks** that IT administrators regularly perform in real-world enterprise environments.

---

### 🚀 What's Next?

This lab focused on the **manual administration** side of Active Directory. In a production environment, most of these tasks can (and should) be automated using **PowerShell**.

Using PowerShell, admins can:
- Create users and OUs in bulk
- Assign group memberships programmatically
- Set GPOs and apply permissions at scale
- Automate auditing, lockout monitoring, and incident response
### In part 2 of the lab we will be setting up a siem using splunk, Attcking the machine using Kali, and Ingesting logs to the siem using sysmon stay tuned. 

> Thank you for checking out this lab!













