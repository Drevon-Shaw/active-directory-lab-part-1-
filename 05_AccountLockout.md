# 🔒 Step 11: Account Lockout Policy & Password Reset

In this step, we simulate a real-world account lockout scenario and walk through how to reset a locked-out user’s password in Active Directory.

---

## 🛠️ Create a Domain-Wide GPO for Account Lockout

1. On the Domain Controller, go to **Tools > Group Policy Management**
2. Right-click on your domain (`lab.local`) > **Create a GPO in this domain, and Link it here**
3. Name it: `AccountLockoutPolicy`
![75](https://github.com/user-attachments/assets/22e8f137-2c47-4647-8e2e-45ced7c3761a)
4. Right-click the GPO > **Edit**

---

## ⚙️ Configure the Lockout Threshold

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

## 🚫 Simulate a Locked-Out Account

1. On the **Windows 10** VM, log in as one of the users (e.g., `ljackson`)
2. Intentionally enter the **wrong password 3 times**

After the 3rd failed attempt, the user will be locked out:

![80](https://github.com/user-attachments/assets/e0b09fbc-0446-4cef-bf01-d17729bf46ed)

---

## 🔄 Reset and Unlock the Account in AD

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

> **Note:** For this lab, when we initially created the passwords, we used **Password never expires**. This must be changed to allow the user to reset the password on the next login.

6. Right-click the user again > **Reset Password**
7. Enter a new password
8. Check:
   - ✅ **User must change password at next logon**
   - ✅ **Unlock the user’s account**
9. Click **OK**
![84](https://github.com/user-attachments/assets/7f6f099e-4d8a-4f6a-b2ca-9cd9dd7b2676)

---

## 🔓 Final Test – Log in Again and Change Password

1. Go back to the **Windows 10 VM**
2. Log in as the user with the **new password**
3. You’ll be prompted to **create a new password**
![85](https://github.com/user-attachments/assets/ea7ade54-6dcb-47e4-bb24-9c40dbe93040)
![86](https://github.com/user-attachments/assets/2cce6568-8e9c-4991-87ea-27a05dcf1512)
4. After that, you'll be successfully logged in

> 🎉 Congratulations! You’ve completed the full Active Directory Lab, including domain setup, user creation, OU organization, GPOs, file permissions, and account recovery!
