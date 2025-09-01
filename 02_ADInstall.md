# 🖥️ Active Directory Installation Lab

This lab covers installing and configuring **Active Directory Domain Services** (AD DS) and **Certificate Services** on Windows Server 2022.

---

### 🔧 Step 1: Rename the Server

We’ll start by renaming the default computer name to `DC01`.

1. Click **Start** and search for `View your PC name`
2. Click **Rename this PC**
3. Enter `DC01` and click **Next**
4. Restart the system after renaming

---

### 🏗️ Step 2: Install Active Directory Domain Services

1. Open **Server Manager**
2. Click **Manage > Add Roles and Features**  
![DC1](https://github.com/user-attachments/assets/ad434233-28fe-4f0a-9d4a-8dc9217e39b8)
3. Select **Role-based or feature-based installation**  
![2](https://github.com/user-attachments/assets/3cf4e01b-d727-46ea-a2c4-d9f3ebf3d90a)
4. Choose server `DC01` from the pool  
![3](https://github.com/user-attachments/assets/132d7a7d-ce86-40e5-a397-a967c446067a)
5. On **Server Roles**, check **Active Directory Domain Services**  
![4](https://github.com/user-attachments/assets/6538fe66-486e-4803-b001-c9300c3c6e9f)
6. Click **Add Features**  
![5](https://github.com/user-attachments/assets/f55de43b-0d81-40f4-875d-631a10fb0e96)
7. Click **Next** through the wizard and select **Restart the destination server automatically if required**
8. Click **Install** and wait for installation  
![6](https://github.com/user-attachments/assets/5491173c-d121-41b5-898b-445b3a6f4f4d)

---

### 🏁 Step 3: Promote Server to Domain Controller

1. After installation, click **Promote this server to a domain controller**  
![6](https://github.com/user-attachments/assets/cbc72433-73fd-4f3e-8849-66ab4f6e0d3a)
2. Choose **Add a new forest**
3. Enter the root domain name: `LAB.local`  
![7](https://github.com/user-attachments/assets/9f3717e2-ee0e-41a3-b6bf-d42c74a4ee11)
4. Set a password for **Directory Services Restore Mode** (preferably the same as your server password)
5. Accept defaults for database paths and click **Next**
6. Verify prerequisites and click **Install**  
![9](https://github.com/user-attachments/assets/fa28247b-ceee-4031-92d4-d2e335123b01)
7. Server will reboot automatically

---

### ✅ Step 4: Verify Domain Login

1. At log-in screen, confirm the domain shows `LAB\Administrator`  
![10](https://github.com/user-attachments/assets/2a6b43f1-35bc-4c35-820a-d604bcc503f6)
2. Log in with the password you set during installation
3. Desktop loads successfully → domain controller is live 🎉

---

### 🔐 Step 5: Add Active Directory Certificate Services (AD CS)

1. Open **Server Manager > Manage > Add Roles and Features**
2. Select **Role-based or feature-based installation**
3. Choose server `DC01` and click **Next**
4. On **Server Roles**, check **Active Directory Certificate Services**  
![11](https://github.com/user-attachments/assets/01991951-2440-413c-a5e5-46541f010fec)
5. Click **Add Features**
6. Click **Next** through wizard, check **Restart the destination server automatically if required**
7. Click **Install**

---

### ⚙️ Step 6: Configure Active Directory Certificate Services

1. In **Server Manager**, click **Configure Active Directory Certificate Services**
2. Use default domain credentials and click **Next**
3. Select **Certification Authority** and click **Next**
4. Accept defaults on all pages, click **Configure**
5. Wait for green ✓ confirmation, then click **Close**
6. Restart server if prompted

---

> You now have a fully functional **Domain Controller** with **AD CS** installed, ready for advanced tasks in later lab sections.

