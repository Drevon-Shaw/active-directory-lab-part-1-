# 🛠️ AD Lab - Lab Preparation

## 📌 Objective
Prepare the environment for the Active Directory lab. This includes setting up virtual machines, networking, and initial configuration before installing Active Directory.

---

## 🖥️ Virtual Machines Setup

**VMs required:**

| VM Name | OS                  | Role        |
|---------|-------------------|------------|
| DC01    | Windows Server 2022 | Domain Controller |
| WS01    | Windows 10        | AD-connected client |

**Steps:**

1. Download and install **VirtualBox** or **VMware Workstation**.
2. Create two VMs with the specifications above.
3. Configure **static IP addresses**:

| VM   | IP Address     | Subnet Mask    | Gateway       |
|------|---------------|----------------|--------------|
| DC01 | 192.168.10.10 | 255.255.255.0  | 192.168.10.1 |
| WS01 | 192.168.10.20 | 255.255.255.0  | 192.168.10.1 |

4. Configure **NAT or Host-only networking** for communication between the VMs.

---
## Lab Prep Screenshots

### VM Setup
![VM Setup](assets/screenshots/lab_prep/vm_setup.png)

### Network Configuration
![Network Config](assets/screenshots/lab_prep/network_config.png)

