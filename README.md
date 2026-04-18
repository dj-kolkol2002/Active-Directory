# Active Directory & Windows Server Infrastructure 🖥️

![Windows Server](https://img.shields.io/badge/Windows_Server-OS-0078D6?style=flat-square&logo=windows)
![Active Directory](https://img.shields.io/badge/Active_Directory-Identity-0078D6?style=flat-square)
![Networking](https://img.shields.io/badge/Networking-DNS_&_DHCP-009639?style=flat-square)
![Status: Done](https://img.shields.io/badge/Status-Done-green?style=flat-square)

**Educational infrastructure deployment for centralized network management**
This project involves the comprehensive setup and configuration of a Windows Server environment. It solves the problem of decentralized user and network administration by implementing an Active Directory domain (`kolkol.local`). It is designed for educational/academic purposes (PANS university) to demonstrate core system administration and network deployment skills.

## 🛠️ Technologies
* Windows Server
* Active Directory Domain Services (AD DS)
* Domain Name System (DNS)
* Dynamic Host Configuration Protocol (DHCP)
* Internet Information Services (IIS)
* Group Policy Management (GPO)

## ✨ Features
* Centralized identity and access management through Active Directory organizational units (OUs).
* Automated client IP addressing via a configured DHCP server scope.
* Internal hostname resolution handled by an integrated DNS server.
* Centralized workstation configuration and enforcement using Group Policy Objects (GPOs), such as unified desktop wallpapers.
* Internal web application hosting using an IIS server.

## ⚙️ The Process
The setup process followed standard Microsoft deployment practices to transition a standalone server into a fully functional Domain Controller:
1. **Domain Creation:** Installed the AD DS role and promoted the server to a Domain Controller, establishing a new forest named `kolkol.local`.
2. **Network Services Setup:** Deployed DNS for internal resolution pointing to the static IP `10.1.1.128`. Configured a DHCP scope distributing addresses from `10.1.1.1` to `10.1.1.254` with a /24 subnet mask to automate client network connections.
3. **Organizational Structure:** Designed a logical OU hierarchy reflecting the company structure (`Budynek_C` -> `Dzial Kadr`, `Dzial Finansowy`) and provisioned user accounts (e.g., Jan Kadrowy).
4. **GPO Implementation:** Created and linked a specific Group Policy Object named "Zdefiniowanie jednolitego tla pulpitu" to enforce a corporate desktop background across all machines in the domain.
5. **Web Hosting:** Installed the IIS role and configured a local testing website accessible via `www.kolkol.local`.

## 📊 Proof of Concept / Testing

* **Server Manager / AD Deployment:**
  *(Insert your `obraz1.png` here)*
  Adding a new forest with the root domain name `kolkol.local` on the target server.

* **DHCP Configuration:**
  *(Insert your `dhcp.png` here)*
  Defining the IPv4 address range (`10.1.1.1` - `10.1.1.254`) for automatic client assignment.

* **DNS Resolution Test:**
  *(Insert your `nslookup.png` here)*
  Command prompt output showing successful DNS resolution for `dc1.kolkol.local` and `dc.kolkol.local` pointing to IP `10.1.1.128`.

* **Active Directory Users and Computers:**
  *(Insert your `users.png` here)*
  Creating a new domain user "Jan Kadrowy" (`kadrowy@kolkol.local`) within the `Dzial Kadr` OU.

* **Group Policy Verification:**
  *(Insert your `policies.png` here)*
  `gpresult` command output showing the successful application of the "Zdefiniowanie jednolitego tla pulpitu" GPO on the domain controller.

* **Client Machine GPO Application:**
  *(Insert your `background.png` here)*
  The custom corporate desktop background (PANS W NYSIE) successfully forced by the deployed Group Policy.

* **IIS Web Server Test:**
  *(Insert your `IIS.png` here)*
  Accessing the internally hosted testing website through the browser using the local domain address `www.kolkol.local`.

## 💡 What I Learned
* How to plan, deploy, and promote a Windows Server to a primary Domain Controller.
* Configuring crucial network infrastructure roles like DNS zones and DHCP scopes from scratch.
* Creating logical Active Directory structures and managing domain users.
* Applying and troubleshooting Group Policy Objects to enforce rules on client machines.
* Setting up basic web hosting using Microsoft IIS.

## 🚀 What can be improved
* Add a secondary Domain Controller (Read-Only or standard) to ensure high availability and fault tolerance.
* Implement more complex GPOs, such as blocking external USB drives or mapping network drives automatically.
* Configure an active Certificate Authority (AD CS) to secure the IIS website with SSL/TLS (HTTPS).
* Automate user creation and management using PowerShell scripts.

## How to run the Project
Since this is an infrastructure project, you need a virtualized lab environment rather than a simple script execution:
1. Deploy a Virtual Machine (e.g., in VirtualBox, VMware, or Hyper-V) and install Windows Server.
2. Assign a static IP address to the server (e.g., `10.1.1.128`).
3. Open **Server Manager** and install the **AD DS, DNS, DHCP, and Web Server (IIS)** roles.
4. Promote the server to a Domain Controller and create a new forest (e.g., `yourdomain.local`).
5. Configure the DHCP scope and activate it.
6. Deploy a client VM (Windows 10/11), ensure it receives an IP from your DHCP, and join it to your newly created domain to test the policies.
