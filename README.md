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

