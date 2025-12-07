# 🛠 Active Directory Lab in Azure (Windows Server 2025)

![Azure](https://img.shields.io/badge/Azure-0089D6?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Windows Server](https://img.shields.io/badge/Windows%20Server-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![Active Directory](https://img.shields.io/badge/Active%20Directory-0067C5?style=for-the-badge&logo=microsoft&logoColor=white)
![Help Desk](https://img.shields.io/badge/Help%20Desk%20Skills-4CAF50?style=for-the-badge)

This project is a hands-on Active Directory lab built entirely in Microsoft Azure.  
It recreates a real enterprise IT environment with a Windows Server 2025 Domain Controller.  
The goal is to demonstrate core IT support skills including domain creation, DNS, user management, RDP, and Azure VM administration.

---

# 🎯 Project Overview

This lab simulates a real on-premises IT environment using cloud-hosted Azure VMs.

**Completed so far:**

- Deployed a Windows Server 2025 Azure VM  
- Assigned static private IP for DC reliability  
- Installed Active Directory Domain Services  
- Promoted server to a Domain Controller  
- Created the forest/domain `lab.local`  
- Logged in using domain credentials (`lab\labadmin`)  

This environment is ideal for practising IT Support, Desktop Support, Service Desk, and junior Sysadmin tasks.

---

# ☁️ Azure Infrastructure Setup

## 1️⃣ Resource Group  
- **Name:** `AD-Lab-RG`  
- **Region:** West Europe  

![Resource Group](Screenshots/Resource%20Group.PNG)

---

## 2️⃣ Virtual Network  
- **VNet:** `AD-Lab-VNet`  
- **Subnet:** `default`  
- **Address Space:** `10.0.0.0/16`
- **Subnet Space:** `10.0.0.0/24`

![VN](Screenshots/AD-LAB-VN.PNG)

---

## 3️⃣ Windows Server 2025 Virtual Machine  
- **VM Name:** `AD-Lab-VM`  
- **Size:** `B2ls_v2`  
- **OS:** Windows Server 2025 Datacenter  
- **Inbound Ports:** RDP (3389)

![VM Overview](Screenshots/VM.PNG)

---

## 4️⃣ Network Interface + Static IP  
- Enabled static private IP to support domain controller functions  
- Ensures DNS and authentication stability  

**NIC settings:**

![NIC](Screenshots/Network%20Interface.PNG)

**Static Private IP:**

![Static IP](Screenshots/static.PNG)

---

# 🛠 Active Directory Domain Setup

## 1️⃣ Installed AD DS Role  
Using Server Manager → Add Roles and Features → Active Directory Domain Services

---

## 2️⃣ Promoted to Domain Controller  
Created a new forest:

- **Domain:** `lab.local`  
- DNS configured automatically  
- Server rebooted after installation  

**Domain Controller Confirmation:**

![Domain Controller](Screenshots/Domain%20Controller.PNG)

---

## 3️⃣ Logged in Using Domain Credentials  
Signed in as:
labadmin@LAB.LOCAL

---

# 🧠 Skills Demonstrated So Far

### 🔹 Azure Skills
- Deploying virtual machines  
- Network Interface configuration  
- Static IP assignment  
- Managing VNets and subnets  
- RDP connectivity troubleshooting  

### 🔹 Windows Server Skills
- Installing server roles  
- Managing Server Manager  
- Understanding domain controllers  
- DNS configuration  

### 🔹 Active Directory Skills
- Creating a new forest and domain  
- Promoting a server to Domain Controller  
- Logging in with domain credentials  
- Understanding domain structure  

This already demonstrates Tier 1 and Tier 2 support capabilities.

---

# 📸 Screenshots

| Description | Image |
|------------|--------|
| Azure Resource Group | ![Resource Group](Screenshots/Resource%20Group.PNG) |
| Azure VM Overview | ![VM](Screenshots/VM.PNG) |
| Network Interface | ![NIC](Screenshots/Network%20Interface.PNG) |
| Static Private IP Configuration | ![Static IP](Screenshots/static.PNG) |
| Domain Controller Confirmation | ![Domain Controller](Screenshots/Domain%20Controller.PNG) |

# 📌 Phase 2 — Active Directory Foundation Completed 

Phase 2 establishes the core Active Directory environment inside `lab.local`.  
This includes departments, users, admin accounts, service accounts, onboarding accounts, RDP permissions, and domain-level security policies.

---

## 🗂️ Organizational Units (OUs) Created

A clean, enterprise-style OU structure was created:

- **_Admins**
- **_Users**
- **_Groups**
- **_Computers**
- **_Departments**
  - IT
  - HR
  - Finance
  - Sales
  - Operations

📸 *OU Structure:*  
![OU Structure](Screenshots/Full%20OU%20Structure.PNG)

---

## 👥 Standard User Accounts (10 Users)

10 realistic employee accounts were added into `_Users`, then moved into their respective department OUs.

| Name | Username | Department |
|------|----------|------------|
| Adam Reid | areid | IT |
| Daniel Grant | dgrant | IT |
| Sarah Khan | skhan | HR |
| Laura Ibrahim | librahim | HR |
| Michael Brown | mbrown | Finance |
| Martin Stone | mstone | Finance |
| Emma Patel | epatel | Sales |
| Aisha Rahman | arahman | Sales |
| Jason Lee | jlee | Operations |
| Chloe Adams | cadams | Operations |

All users were created with:
- No forced password change at logon  
- Password never expires: **disabled**  
- Accounts enabled  

📸 *Users in Department OUs:*  
![Department Users](Screenshots/Department%20OUs%20with%20users.PNG)

---

## 🔐 Privileged & Special Accounts

### 🛠️ IT Admin (Domain Administrator)
- Username: `itadmin`
- Added to:
  - Domain Admins  
  - Enterprise Admins  
  - Schema Admins  
- Password never expires: enabled

📸 *IT Admin Group Membership:*  
![IT Admin Group Membership](Screenshots/IT%20Admin%20group%20membership.PNG)

---

### ⚙️ Service Account (SQL Service)
- Username: `sqlsvc`
- Password never expires: enabled  
- User cannot change password: enabled  

📸 *Service Account Settings:*  
![Service Account Password Settings](Screenshots/Service%20account%20password%20settings.PNG)

---

### 🚫 Onboarding Account
- Username: `new.starter`
- Account disabled  
- Simulates HR pre-staging

📸 *Disabled Account:*  
![Disabled Onboarding Account](Screenshots/Disabled%20onboarding%20account.PNG)

---

### 🔒 Locked-Out User (Help Desk Simulation)
- Username: `locktest`
- Locked via incorrect login attempts  
- Unlocked through ADUC (Account tab)

📸 *Locked-Out Account:*  
![Locked Out Account](Screenshots/LocktestLockedOut.PNG)

---

## 🔐 RDP & User Logon Rights Configuration

To allow non-admin users (like `locktest`) to use RDP:

### ✔ Added to Remote Desktop Users  
- `locktest` added to the **Remote Desktop Users** local group  

### ✔ Updated Local Security Policy  
- Confirmed Remote Desktop Users has RDP logon rights  

---

## 🔄 Account Lockout Policy (Domain Security)

Configured via **Default Domain Policy**:

- Lockout threshold: 3 attempts  
- Lockout duration: 30 minutes  
- Reset counter after: 30 minutes  

Successfully tested with `locktest`.

---

---
---

# 📌 Phase 3 — Department File Shares and NTFS Security (Completed)

Phase 3 introduces enterprise-style file sharing and NTFS permission design.  
Each department receives a secure folder and access is granted strictly through AD security groups.  
This demonstrates help desk and junior sysadmin skills including least privilege access control and permissions troubleshooting.

---

## 🗂️ Department Shares Created

A shared root directory was created on the Domain Controller.

C drive folder location:
    C:\Shares

Folder structure:
    C:\Shares
        IT
        HR
        Finance
        Sales
        Operations

📸 Folder structure  
![Shares Folder Structure](./Screenshots/SharesFolderStructure.PNG)

---

## 👥 Active Directory Security Groups Created

Each department received a dedicated security group used for access control:

- IT_Staff_Members  
- HR_Staff_Members  
- Finance_Staff_Members  
- Sales_Staff_Members  
- Operations_Staff_Members  

📸 Group list  
![Groups List](./Screenshots/GroupsList.PNG)

📸 IT group membership example  
![IT Staff Members](./Screenshots/IT_Staff_Members.PNG)

---

## 🔐 NTFS Permission Configuration

Key NTFS rules applied:
- Removed Authenticated Users  
- Granted Modify permissions to the correct department group  
- Domain Admins and SYSTEM keep Full Control  
- NTFS permissions control access rather than share permissions  
- Implements RBAC (Role Based Access Control)

---

## 📁 NTFS Permissions Per Department

### IT  
![IT NTFS Permissions](./Screenshots/NTFSPermissions_IT.PNG)

### HR  
![HR NTFS Permissions](./Screenshots/NTFSPermissions_HR.PNG)

### Finance  
![Finance NTFS Permissions](./Screenshots/NTFSPermissions_Finance.PNG)

### Sales  
![Sales NTFS Permissions](./Screenshots/NTFSPermissions_Sales.PNG)

### Operations  
![Operations NTFS Permissions](./Screenshots/NTFSPermissions_Operations.PNG)

---

# 📌 Phase 3.5 — Access Testing and Verification (Completed)

A real user (areid from IT) logged in to test permissions.

Expected behaviour:
- IT user can access IT folder  
- IT user cannot access HR, Finance, Sales or Operations  

---

## 🧪 Access Test Results (User: areid)

| Folder | Expected | Result |
|--------|----------|--------|
| IT | Allowed | ✔ Confirmed |
| HR | Denied | ✔ Confirmed |


📸 IT user accessing IT folder  
![IT Folder Access](./Screenshots/IT_User_Access_ITFolder.PNG)

📸 IT user denied from HR folder  
![Access Denied HR](./Screenshots/IT_User_AccessDenied_HR.PNG)

---

# 🎉 Phase 3 and 3.5 Completed

This phase established:

- A clean enterprise style shared folder system  
- NTFS least privilege security  
- AD group based RBAC  
- Removal of inherited permissions  
- Department access isolation  
- Real world permissions troubleshooting  
- Hands on testing using standard domain accounts  

These are core skills used daily in IT Support, Service Desk and Junior Sysadmin roles.

---
# ⭐ Phase 4. Group Policy Configuration

This phase introduces organisation wide security controls and user experience settings using Group Policy on the domain controller AD-Lab-VM. Policies include password requirements, lockout rules, login banners, mapped drives and user restrictions.

---

# 👉 Step 0. Open Group Policy Management

On AD-Lab-VM:

- Start  
- Type gpmc.msc  
- Open Group Policy Management  

All GPOs in this phase are created and linked here.

---

# ⭐ 4.1 Domain Security Policy  
**GPO Name:** ORG-SecurityPolicy  
**Linked To:** lab.local

Configured:

- Minimum password length set to 8  
- Password complexity enabled  
- Maximum password age set to 90 days  
- Minimum password age set to 1 day  
- Password history set to 5 remembered  
- Account lockout threshold set to 5 attempts  
- Lockout duration set to 15 minutes  
- Reset counter after 15 minutes  

### Screenshots  
![Password Policy](Screenshots/SecurityPolicy_PasswordSettings.PNG)  
![Lockout Policy](Screenshots/SecurityPolicy_LockoutSettings.PNG)

---

# ⭐ 4.2 Login Banner  
**GPO Name:** ORG-LoginBanner  
**Linked To:** lab.local

Displays a login warning message to all domain users.

Configured:

- Message title: Authorised Access Only  
- Message text: This system is for authorised use only. Activity may be monitored and recorded.  

### Screenshot  
![Login Banner](Screenshots/LoginBanner.PNG)

---

# ⭐ 4.3 Block USB Storage  
**GPO Name:** ORG-DisableUSB  
**Linked To:** _Users OU

USB storage devices are restricted for standard users.

Configured under System → Removable Disks:

- Deny execute access  
- Deny read access  
- Deny write access  

### Screenshot  
![USB Block Policy](Screenshots/DisableUSB.PNG)

---

# ⭐ 4.4 Department Drive Mapping  
Mapped drives are assigned per department.  
Only IT mapping is shown as an example.

**UNC Paths:**  
Root: \\AD-Lab-VM\Shares\

| Department | Drive Letter | Path |
|-----------|--------------|------------------------------|
| IT        | I:           | \\AD-Lab-VM\Shares\IT        |
| HR        | H:           | \\AD-Lab-VM\Shares\HR        |
| Finance   | F:           | \\AD-Lab-VM\Shares\Finance   |
| Sales     | S:           | \\AD-Lab-VM\Shares\Sales     |
| Operations| O:           | \\AD-Lab-VM\Shares\Operations|

### Screenshot (IT)
![IT Drive Mapping](Screenshots/IT_DriveMapping1.PNG)

---

# ⭐ 4.5 Corporate Wallpaper  
**GPO Name:** ORG-Wallppaper  
**Linked To:** _Users OU

Wallpaper stored in:

```
\\AD-Lab-VM\NETLOGON\wallpaper.jpg
```

Applied using Desktop Wallpaper policy set to Fill.

### Screenshot  
![Wallpaper Policy](Screenshots/DesktopWallpaper.PNG)

---

# ⭐ 4.6 Disable Control Panel  
**GPO Name:** ORG-DisableControlPanel  
**Linked To:** _Users OU

Prevents standard users from opening Control Panel or PC Settings.

### Screenshot  
![Control Panel Disabled](Screenshots/DisableControlPanel.PNG)

---

# ⭐ 4.7 Apply All GPOs

On AD-Lab-VM:

```
gpupdate /force
```

### Screenshot  
![GPO Update](Screenshots/GPOUpdate.PNG)

---

# ⭐ 4.8 Testing (Performed on Windows 11 VM)

Testing completed while logged in as the IT user: lab\areid

Verified:

- I drive successfully mapped  
- Corporate wallpaper applied  
- Control Panel blocked  

### Screenshots  
![Drive Mapping Test](Screenshots/Test_DriveMappings.PNG)  
![Wallpaper Test](Screenshots/Test_Wallpaper.PNG)  
![Control Panel Test](Screenshots/Test_ControlPanel.PNG)

---

# Phase Outcome

Phase 4 successfully implemented organisation wide Group Policy settings including password policies, login warnings, USB restrictions, mapped drives, wallpapers and user restrictions. These controls standardise configuration and improve security across the lab environment.


---
# ⭐ Phase 5 — Windows 11 Client Deployment Using Tailscale (Completed)

Phase 5 connects a remote Windows 11 VM to the Azure hosted Domain Controller using Tailscale, simulating a real corporate remote worker environment.  
This allows secure delivery of DNS, LDAP, Kerberos and GPOs over an encrypted mesh network.

---

# ⭐ 5.1 Tailscale Network Setup

Tailscale was installed on:

- AD-Lab-VM (Domain Controller)  
- Host PC (DESKTOP-ASOA97E)  
- Windows 11 Client VM  

Each device received a private Tailscale IP:

| Machine | Tailscale IP |
|---------|--------------|
| AD-Lab-VM | `100.85.64.63` |
| Host PC | `100.89.252.38` |
| Windows 11 VM | `100.x.x.x` |

This created a secure mesh network allowing the Windows 11 VM to communicate with the Domain Controller even though they are in different locations.

### 📸 Required Screenshot  
- Tailscale running on AD-Lab-VM  
  ![Tailscale](Screenshots/Tailscale_DC.PNG)

---

# ⭐ 5.2 DNS Configuration on Windows 11 VM

Active Directory requires clients to use the Domain Controller for DNS.

DNS was set as:

- Preferred DNS: `100.85.64.63`  
- Alternate DNS: `8.8.8.8` (optional)

This forces all Active Directory queries through the Domain Controller.

### 📸 Required Screenshot  
- Windows 11 DNS settings  
  ![W11 DNS](Screenshots/W11_DNS.PNG)

---

# ⭐ 5.3 Connectivity Checks

Before joining the domain:

nslookup lab.local


DNS successfully resolved the domain through the Domain Controller’s Tailscale IP.

(ICMP ping blocking is normal in Azure environments.)

### 📸 Required Screenshot  
- Successful nslookup  
 ![NS Lookup](Screenshots/W11_NSLookup.PNG)

---

# ⭐ 5.4 Joining the Windows 11 VM to lab.local

The VM was joined to the domain using:

lab.local
lab\itadmin

After reboot, the domain relationship was established.

---

# ⭐ 5.5 Domain Login and GPO Application

Logged in using the IT user:
lab\areid


The initial login took longer due to:

- New profile creation  
- GPOs applying over Tailscale  
- SYSVOL and NETLOGON access over encrypted tunnel  

Once logged in, these GPOs were confirmed working:

- Corporate wallpaper  
- Drive mappings  
- Control Panel restriction  
- Login banner  

### 📸 Required Screenshots  
- Wallpaper applied  
  ![Wallpaper](Screenshots/Wallpaper.PNG)  
- Drive mapping visible  
  ![DriveMapping](Screenshots/DriveMapping.PNG)  
- Control Panel blocked  
  ![Control Panel Blocked](Screenshots/ControlPanelBlocked.PNG)

---

# ⭐ 5.6 Confirmation in Active Directory

The Windows 11 VM appeared under the **_Computers** container in ADUC, confirming a successful join and trust relationship.

### 📸 Required Screenshot  
- Computer object in ADUC  
  ![Client AD](Screenshots/Client_ADUC.PNG)

---

# 🎉 Phase 5 Completed

This phase demonstrated:

- Secure remote AD communication using mesh VPN  
- Remote domain join capability  
- DNS redirection for Active Directory  
- Delivery of GPOs over encrypted WAN  
- SYSVOL access and GPO enforcement through Tailscale  
- Realistic simulation of remote employee onboarding  

This is advanced enterprise level AD and networking knowledge typically used by IT Support, Systems Engineers and Cloud Administrators.

---


---

# 🧑‍💻 Author  
**Mohammad Masood (mullvad25)**  
Aspiring IT Support & Systems Engineer  
Focused on infrastructure, cloud, networking, and enterprise IT tools.

---

# 🌐 Purpose of This Lab  
This project is meant to:

- Build real job-ready IT skills  
- Strengthen a professional portfolio  
- Prove hands-on technical ability to recruiters  
- Prepare for IT Support, Help Desk, Desktop Support, and Sysadmin roles  

---

