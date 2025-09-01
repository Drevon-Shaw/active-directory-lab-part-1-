 Apply a Group Policy Object (GPO) – Custom Wallpaper

**Group Policy Objects (GPOs)** control system behavior for users, groups, or computers in an Active Directory environment.  

In this step, we’ll apply a custom desktop wallpaper **only** for the `Engineering` OU users using GPO.

---

### 🖼️ Create the Custom Wallpaper

1. Open **Paint** on your Domain Controller.  
2. Create a large background image and type:



![61](https://github.com/user-attachments/assets/cdbe29fc-cabf-4eb0-84ae-000e7747909c)  
*Remember to center the words – a small mistake might happen, that’s okay.*

3. Save the file to the **Desktop** as `engineering_wallpaper.jpg`  

![60](https://github.com/user-attachments/assets/cabc4e3e-8628-47e2-88a1-609d0f873f38)  

---

### 📂 Copy Wallpaper to Shared Location (NetLogon)

Administrators typically store wallpapers in the `NetLogon` share.

1. In **Server Manager**, go to:
   - **File and Storage Services → Shares**
2. Find the **NetLogon** share  

![62](https://github.com/user-attachments/assets/e08d5ffa-8681-49c1-ac59-01d9e26995c2)  

3. Right-click → **Open Share**  
4. Open your Desktop folder in another window  

![63](https://github.com/user-attachments/assets/090440a1-fe5c-4e7a-b69c-b26cfafbad13)  

5. Copy and paste the wallpaper into the `NetLogon` folder  

![64](https://github.com/user-attachments/assets/3722199e-49b7-4cf0-9264-667d49d9ed0c)  
![65](https://github.com/user-attachments/assets/0fc0565d-cb62-4af9-b5ed-e2d5f676a0e9)  

6. Hold **Shift**, right-click the image file → **Copy as Path**  

![66](https://github.com/user-attachments/assets/345e2635-bd81-41c3-beaf-38c625a78a80)  

---

### ⚙️ Create and Link a GPO for Engineering

1. Go to **Tools → Group Policy Management**  
2. Expand:  
   - **Forest → Domains → lab.local → Engineering**  
3. Right-click the `Engineering` OU → **Create a GPO in this domain, and Link it here…**  
4. Name it: `SetEngineeringBackground`  

![69](https://github.com/user-attachments/assets/317788fb-6e85-43b6-ac4c-edd424311543)  

5. Right-click the new GPO → **Edit**  

---

### 🛠️ Configure the Wallpaper Policy

1. In the **Group Policy Management Editor**, navigate to:  
   - `User Configuration → Policies → Administrative Templates → Desktop → Desktop`  
2. Double-click **Desktop Wallpaper**  
3. Choose **Enabled**  
4. Paste the full path to the `.jpg` file from NetLogon (example):  

