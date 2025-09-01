04_GPOs.md
1️⃣ Create a Group Policy Object (GPO)

Open Group Policy Management on the Domain Controller.

Right-click your domain → Create a GPO in this domain, and Link it here…

Name the GPO (e.g., EngineeringWallpaperPolicy).

Screenshot: ![GPO Creation](https://github.com/user-attachments/assets/your_gpo_creation_screenshot.png)

2️⃣ Configure Desktop Wallpaper for OU

Right-click the GPO → Edit.

Navigate to User Configuration → Policies → Administrative Templates → Desktop → Desktop → Desktop Wallpaper.

Enable the setting, enter the wallpaper path, and choose Fill for the style.

Screenshot: ![Wallpaper Policy](https://github.com/user-attachments/assets/your_wallpaper_screenshot.png)

3️⃣ Apply Account Lockout Policy

Navigate to Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy.

Configure:

Account lockout threshold → 3 invalid login attempts

Account lockout duration → 15 minutes

Reset account lockout counter after → 15 minutes

Screenshot: ![Lockout Policy](https://github.com/user-attachments/assets/your_lockout_screenshot.png)

4️⃣ Link GPO to OU

In Group Policy Management, drag the GPO onto the target OU (e.g., Engineering).

Right-click the OU → Link an Existing GPO → select the created GPO.

Screenshot: ![Link GPO](https://github.com/user-attachments/assets/your_link_gpo_screenshot.png)

5️⃣ Test GPO Application

Log in as a user within the OU.

Verify that the desktop wallpaper is applied and account lockout policy works by testing invalid logins.

Screenshot: ![GPO Test](https://github.com/user-attachments/assets/your_gpo_test_screenshot.png)
