# Active Directory Lab in Azure (Windows Server 2025)

This project is a hands-on Active Directory lab built entirely in Microsoft Azure.  
It recreates a real enterprise environment with a Windows Server domain controller.  
The goal is to demonstrate core IT help desk and sysadmin skills including domain creation, DNS, user management, and Azure VM management.

---

## 🎯 Project Overview

This lab simulates an on-premise IT environment using Azure virtual machines.  
It includes:

- A Windows Server 2025 virtual machine running as a Domain Controller  
- A newly created Active Directory forest and domain (`lab.local`)  
- DNS services configured automatically during domain controller promotion  
- Static private IP configuration for reliable domain operations  
- Future steps: OUs, users, group policies, Windows 11 domain join, help desk tasks  

This project is foundational for anyone aiming for IT support, help desk, or junior sysadmin roles.

---

## ☁️ Azure Infrastructure Setup

### 1. Created a Resource Group  
- **Name:** `AD-Lab-RG`  
- **Region:** West Europe

### 2. Created a Virtual Network  
- **Name:** `AD-Lab-VNet`  
- **Subnet:** `default`  
- **Address space:** `10.0.0.0/24`

### 3. Deployed Windows Server 2025 VM  
- **VM Name:** `AD-DC01`  
- **Size:** `B2ls_v2`  
- **OS:** Windows Server 2025 Datacenter  
- **Inbound Ports:** RDP (3389)  
- **Static Private IP assigned:** `10.0.0.4`

### 4. Connected via RDP  
- Used Azure RDP connection  
- Logged in as local admin: `labadmin`

---

## 🛠️ Active Directory Domain Setup

### 1. Installed AD DS Role  
Using Server Manager:  
- **Manage → Add Roles and Features**  
- Selected **Active Directory Domain Services**

### 2. Promoted the Server to a Domain Controller  
- Used the AD DS configuration wizard  
- Created a new forest  
- **Domain name:** `lab.local`  
- Configured DNS automatically  
- Server rebooted and became a Domain Controller

### 3. Logged in Using Domain Credentials  
- Signed in as: `lab\labadmin`  
- Confirmed domain status under System Info

---

## 📘 Skills Demonstrated So Far

- Creating Azure virtual machines  
- Working with VNets and subnets  
- Static IP configuration  
- RDP connectivity  
- Installing Active Directory Domain Services  
- Promoting Windows Server to Domain Controller  
- Creating and understanding a domain (`lab.local`)  
- Logging in with domain credentials  
- Basic understanding of DNS, domain controllers, and Azure networking  

---

## 🚀 Next Steps (To Be Added Later)

These improvements will be added as the lab expands:

- Create Organizational Units (OUs)  
- Create users and security groups  
- Implement Group Policies (GPOs)  
- Deploy a Windows 11 VM and join it to the domain  
- Map network drives  
- Simulate help desk tasks:
  - Password resets  
  - Account lockouts  
  - Permissions issues  
  - Access requests  
- (Optional) Sync on-prem AD to Azure AD using Azure AD Connect  

This README will be updated as the project grows.

---

## 📸 Screenshots (Coming Soon)

I will include screenshot proof of:

- Azure VM deployment  
- Static IP settings  
- AD DS installation  
- Domain promotion  
- Domain login (`lab\labadmin`)  
- ADUC console  
