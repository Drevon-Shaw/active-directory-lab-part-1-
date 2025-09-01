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

## 2️⃣ Create Users

1. In ADUC, navigate to the OU where you want to create a user.
2. Right-click → **New** → **User**.
3. Enter first name, last name, username, and password.
4. Repeat for multiple users in each OU.

**Screenshot:**

![16](https://github.com/user-attachments/assets/af42ac59-3227-45ed-9691-fa6a97babce2)

---

## 3️⃣ Create Security Groups

1. Navigate to the OU where groups should reside.
2. Right-click → **New** → **Group**.
3. Name the group, select **Security**, and choose the scope (usually **Global**).
4. Add users to the group:
   - Example: `EngineeringShare` → add all Engineering OU users.

**Screenshot:**

![34](https://github.com/user-attachments/assets/3ee19ec3-a45d-434a-a701-d741aa4abd8e)

---

## 4️⃣ Assign Group-Based Access

1. Right-click the shared folder → **Properties** → **Security**.
2. Add the group (e.g., `EngineeringShare`) and assign permissions (Read/Write/Modify).
3. Test by logging in as a user from the OU to verify access.

**Screenshot:**

![44](https://github.com/user-attachments/assets/f08f634b-2a9e-49cb-ae86-020d8b3ce3b1)
![49](https://github.com/user-attachments/assets/6b99f26f-4df4-4922-9732-3b4810842838)
![53](https://github.com/user-attachments/assets/0b7a9240-9f60-406d-8a58-c1577be1a3be)

---

## ✅ Outcomes

By completing this section, you can:

- Create OUs for organizational structure
- Add users to AD and assign passwords
- Create security groups and apply group-based permissions
- Enforce least privilege access for shared resources
