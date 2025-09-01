# 👥 Users & Organizational Units (OUs)

This section covers creating users, organizational units, and security groups in Active Directory.

---

## 1️⃣ Create Organizational Units (OUs)

1. Open **Active Directory Users and Computers (ADUC)** on your Domain Controller.
2. Right-click the domain `LAB.local` → **New** → **Organizational Unit**.
3. Name your OUs:
   - `Engineering`
   - `Management`
   - `IT`
4. (Optional) Nest an `Admins` OU inside `IT` for administrative accounts.

**Screenshot:**

![29](https://github.com/user-attachments/assets/6797cfd3-6a6b-4087-b925-31ed2dca93f2)

---

3️⃣ Create Security Groups

Navigate to the OU where groups should reside.

Right-click → New → Group.

Name the group, select Security, and choose the scope (usually Global).

Add users to the group:

Example: EngineeringShare → add all Engineering OU users.

Screenshot: ![35](https://github.com/user-attachments/assets/0482789e-260d-453d-b5cf-0d4cbf703f9f)

4️⃣ Create and Secure a Shared Folder

Go to Server Manager → File and Storage Services → Shares
![38](https://github.com/user-attachments/assets/0009c73e-b969-48af-91b6-6abe22cd2441)

On the right, under Tasks, click New Share
![40](https://github.com/user-attachments/assets/3eab63b9-3884-47a4-884b-20d06fb0972a)

Select SMB Share - Quick
![41](https://github.com/user-attachments/assets/4cfaa7f9-74c6-4ba8-ba93-850f2a80feeb)

Leave the default location on the C: drive
![42](https://github.com/user-attachments/assets/2548a301-a758-40cf-a375-85b56ac62793)

Name the share: EngineeringShare
![43](https://github.com/user-attachments/assets/06bb80e5-1a88-4a72-ab85-61fd2d0b78b7)

Note the share path: \\DC01\EngineeringShare

🔐 Customize Permissions for the Group

On the Permissions page, click Customize Permissions
![44](https://github.com/user-attachments/assets/f08f634b-2a9e-49cb-ae86-020d8b3ce3b1)

Click Disable Inheritance → Convert inherited permissions into explicit permissions
![45](https://github.com/user-attachments/assets/d4509cba-6640-4746-86d7-3816286fbad5)

Remove unnecessary users (e.g., LAB\USERS).

Click Add → Select a Principal, add EngineeringShare group
![48](https://github.com/user-attachments/assets/d9e0764b-f8c0-4296-b079-1d47f60face4)

Grant Read/Write permissions
![49](https://github.com/user-attachments/assets/6b99f26f-4df4-4922-9732-3b4810842838)

Click Apply → OK → Next → Create → Close
