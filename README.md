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

---

## 🖥️ Lab Setup

| Component         | OS                  | Role                     |
|------------------|---------------------|--------------------------|
| `DC01`           | Windows Server 2022 | Domain Controller        |
| `Client01`       | Windows 10          | AD-connected client PC   |

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
![30a](https://github.com/user-attachments/assets/64f137e6-213f-40f3-9831-2ded4711a7f2)
![30a](https://github.com/user-attachments/assets/33bb08b6-68ab-4145-9bbf-88202193bc9e)

---

### 🗂️ Create a Nested Organizational Unit

You can create an OU inside another OU for more structure.

1. Right-click the `IT` OU > **New > Organizational Unit**
2. Name it `Administrators`
![30a](https://github.com/user-attachments/assets/bb0ce25a-fcc9-4d7f-9c94-239c8c772c1f)

4. Move the `Administrator` account into the `Administrators` OU
![30a](https://github.com/user-attachments/assets/64505e53-359e-4d09-8e3d-b05e6004e701)

---

### 👥 Lets Create a Group inside the engineeing OU 

1. Go to the `Engineering` OU
2. Right-click > **New > Group**
![33](https://github.com/user-attachments/assets/e55a9ac3-0ab4-417d-8bbe-bdf26e86a974)
4. Name the group: `EngineeringShare`
5. Make sure **Group type** is set to **Security**
![33](https://github.com/user-attachments/assets/1a6a12c9-f87a-40fd-92ac-fcac4e7253ec)
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
![41](https://github.com/user-attachments/assets/f63517f8-7142-47a2-949c-fbe9d4aee732)
9. Name the share: `EngineeringShare`
![41](https://github.com/user-attachments/assets/94edd22e-fd8e-419b-abdd-5f85cde357b1)
11. Note the share path: `\\DC01\EngineeringShare`

---

### 🔐 Customize Permissions for the Group

1. When you reach the **Permissions** page, click **Customize Permissions**
![41](https://github.com/user-attachments/assets/031b31c3-b247-44b2-9f6a-3915c6fd5f30)
3. Click **Disable Inheritance** > choose **Convert inherited permissions into explicit permissions**
5. Remove existing users (as needed) as you can see we have more users than needed **I would remove both LAB\USERS**
6. Click **Add > Select a Principal** and add `EngineeringShare` This is the group we created.
![48](https://github.com/user-attachments/assets/d9e0764b-f8c0-4296-b079-1d47f60face4)
8. Grant **Read/Write** permissions
9. Click **Apply > OK > Next > Create > Close** **make sure to apply the changes**

---

### 🧪 Access the Share from Windows 10 Client

1. Log into the Windows 10 VM using a user in the `EngineeringShare` group (e.g., `ljackson`) this varies depending on what users you have in the engennering group
2. Open **File Explorer**
3. Go to **Network**, find `DC01`, and open `EngineeringShare` **Remember to turn on network sharing, also both vms have to be active**
![48](https://github.com/user-attachments/assets/9a3b68ea-2bbd-4e2c-ba0c-393250baf4e3)

You should now be able to open, create, and edit files in this shared folder.
![48](https://github.com/user-attachments/assets/ec9128a6-8ff7-4699-8531-946be102d794)


---

### 💾 Optional: Map Network Drive **This is a common task used by IT administrators for easier access to shared files and folders**

To map the shared folder as a drive letter:

1. Open **This PC**
2. Right-click on blank space > **Map Network Drive**
![55](https://github.com/user-attachments/assets/9f7c8fe6-4d19-42b0-b5d7-aa00c336a094)
4. Choose a drive letter (e.g., `Z:`)
5. Enter the folder path: `\\DC01\EngineeringShare`
![55](https://github.com/user-attachments/assets/3064dbd1-3edf-486c-a3d5-f689696e38bd)
7. Click **Finish**
8. Now the EngineeringShare folder is showing up like a regular driv eon your computer

![57](https://github.com/user-attachments/assets/6a156193-c072-4b1c-97d6-a2fc20d29a6d)

   ---

### ❌ Test Access Denial for Non-Group Users

To confirm our permission settings are working correctly, log into a user **not** in the `EngineeringShare` group (e.g., someone from the `Management` OU).

1. Log into the Windows 10 VM with a different user (e.g., `gowens`)
![58](https://github.com/user-attachments/assets/5ed9cea8-709f-4217-8e37-d526e15f480e)
2. Open **File Explorer**
3. Go to **Network > DC01**

You will see that access to `EngineeringShare` is denied:

![58](https://github.com/user-attachments/assets/589ee6c3-15ec-4c95-b3df-b6662659b711)


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

![61](https://github.com/user-attachments/assets/a6e755de-f274-447a-9fc9-58c00c92abda)

---

### 📂 Copy Wallpaper to Shared Location (NetLogon)

Administrators typically store login scripts and wallpapers in the `NetLogon` share.

1. In **Server Manager**, go to:
   - **File and Storage Services > Shares**
2. Find the **NetLogon** share
![61](https://github.com/user-attachments/assets/7b096dd6-8224-4c59-b723-6f09c111593e)
4. Right-click it > **Open Share**
5. Open your Desktop folder in another window
![63](https://github.com/user-attachments/assets/090440a1-fe5c-4e7a-b69c-b26cfafbad13)
7. Copy and paste the wallpaper into the `NetLogon` folder
![65](https://github.com/user-attachments/assets/0fc0565d-cb62-4af9-b5ed-e2d5f676a0e9)
8. Hold **Shift**, right-click the image file > **Copy as Path**
![66](https://github.com/user-attachments/assets/345e2635-bd81-41c3-beaf-38c625a78a80)


---

### ⚙️ Create and Link a GPO for Engineering

1. Go to **Tools > Group Policy Management**
2. Expand:
   - **Forest > Domains > lab.local > Engineering**
3. Right-click the `Engineering` OU > **Create a GPO in this domain, and Link it here...**
4. Name it: `SetEngineeringBackground`
5. ![66](https://github.com/user-attachments/assets/5becab63-6ab4-459f-bb16-20f774c2f311)
6. Right-click the new GPO > **Edit**
---

### 🛠️ Configure the Wallpaper Policy

1. In the **Group Policy Management Editor**, navigate to:
   - `User Configuration > Policies > Administrative Templates > Desktop > Desktop`
2. Double-click **Desktop Wallpaper**
3. Choose **Enabled**
![66](https://github.com/user-attachments/assets/5e259a59-84cb-479d-b026-8a3af75e17ae)
5. Paste the full path to the `.jpg` file from NetLogon (example):
   ```
   \\DC01\netlogon\engineering_wallpaper.jpg
   ```
6. Set **Wallpaper Style** to `Center`
7. Click **OK**
![66](https://github.com/user-attachments/assets/21f7de1f-7ec7-49e9-b735-ff58d07e22eb)

---

### 💻 Test the GPO from Windows 10

1. Switch to your **Windows 10 VM**
2. Log in as a user from the **Engineering OU** (e.g., `ljackson`, `nmandela`)
3. You should now see the custom **Engineering Dept** wallpaper!
![66](https://github.com/user-attachments/assets/3432c401-293e-4c94-abf9-916160b06287)
   **THIS IS WHERE I MESSED UP BY NOT PLACING THE WORDING IN THE CENTER**
4. Now log in as a non-engineering user (e.g., from Management)
5. You’ll notice the **default wallpaper is still applied**, confirming the GPO was targeted correctly
![66](https://github.com/user-attachments/assets/8abd6162-731b-498c-8966-1b8ee0ef5cd9)

---

> 🧠 This demonstrates how to apply GPOs to specific user groups using OUs — a key concept in managing enterprise environments.

---


### 🔒 Step 11: Account Lockout Policy & Password Reset

In this final step, we’ll simulate a real-world account lockout scenario and walk through how to reset a locked-out user’s password in Active Directory.

---

### 🛠️ Create a Domain-Wide GPO for Account Lockout

1. On the Domain Controller, go to **Tools > Group Policy Management**
2. Right-click on your domain (`lab.local`) > **Create a GPO in this domain, and Link it here**
![74](https://github.com/user-attachments/assets/d0cb7a49-863a-42dc-b887-617f037fbb8b)
4. Name it: `AccountLockoutPolicy`
![74](https://github.com/user-attachments/assets/570ed8ac-f763-4667-ade7-34cc175eb013)
6. Right-click the GPO > **Edit**

---

### ⚙️ Configure the Lockout Threshold

1. Navigate to:
   - `Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy`
2. Double-click **Account lockout threshold**
3. Set to: `3` (invalid login attempts before lockout)
4. Click **Apply**
![74](https://github.com/user-attachments/assets/18fc288a-7794-4a2e-a858-eb9bf3da7a11)
5. Right-click the GPO again > **Enforce**, to make sure it's active
![74](https://github.com/user-attachments/assets/05d93aea-f424-4fc8-a77f-8e58c7ff037e)

---

### 🚫 Simulate a Locked-Out Account

1. On the **Windows 10** VM, log in as one of the users (e.g., `ljackson`)
2. Intentionally enter the **wrong password 3 times**

After the 3rd failed attempt, the user will be locked out:

![74](https://github.com/user-attachments/assets/a674be36-1ccb-4c63-9346-d96da02dfb57)

---

### 🔄 Reset and Unlock the Account in AD

1. On the Domain Controller, go to:
   - **Tools > Active Directory Users and Computers**
2. Use the **Search function** (top icon) to search for the locked-out user
   - Be sure to change scope to **Entire Directory**
![81](https://github.com/user-attachments/assets/15364292-07dd-4a6c-a8d1-6a03c3e7c496)
3. Right-click the user > **Properties > Account tab**
4. Uncheck **Password never expires**
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
4. After that, you'll be successfully logged in
![84](https://github.com/user-attachments/assets/7459a72c-78af-4c3b-83e2-d2270e609896)
![84](https://github.com/user-attachments/assets/c1a806a6-d825-4ff8-bc72-e9fc08e0d110)

> 🎉 Congratulations! You’ve completed the full Active Directory Lab – including domain setup, user creation, OU organization, GPOs, file permissions, and account recovery!


---

## ✅ Lab Outro – Summary & Final Thoughts

In this Active Directory Lab, we built and explored a foundational enterprise-like domain environment using Windows Server 2022 and Windows 10. Here's a summary of what we accomplished:

### 🧠 What We Learned

- 🔧 **Configured a Domain Controller** using Active Directory Domain Services
- 💻 **Joined a Windows 10 machine** to the domain
- 👥 **Created and managed domain users** using Organizational Units (OUs)
- 📂 **Created security groups** and applied **file share permissions**
- 🔐 **Set Group Policy Objects (GPOs)** to enforce desktop backgrounds and lockout policies
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

> Thank you for checking out this lab! If you found it helpful, feel free to fork the repo, share feedback, or build on top of it.













