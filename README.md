# Windows Server 2022: Active Directory and BitLocker Lab

This repository documents a comprehensive Windows Server 2022 lab environment focused on enterprise identity, access management, and data protection. The project demonstrates practical experience in deploying Active Directory Domain Services (AD DS), enforcing Group Policies, and implementing BitLocker full-disk encryption using TPM 2.0.

Each functional stage of the lab is isolated in a dedicated Git branch to clearly demonstrate progression and allow focused exploration of each component.

---

## Objectives

- Deploy and configure a secure Windows Server 2022 domain environment
- Install and promote Active Directory Domain Services (AD DS)
- Configure DNS and domain controller settings
- Create and manage Organizational Units (OUs), users, and security groups
- Apply and test Group Policy Objects (GPOs)
- Implement BitLocker encryption and manage TPM-based protection
- Join Windows 10/11 clients to the domain
- Demonstrate PowerShell scripting for administrative tasks

---

## Branch Structure

| Branch Name              | Purpose                                                                 |
|--------------------------|-------------------------------------------------------------------------|
| [part-1-vm-setup](https://github.com/Tariq-homelab/winserver-ad-bitlocker/tree/part-1-vm-setup) | Validate UEFI, Secure Boot, and TPM 2.0 settings on Windows Server 2022 |
| part-2-adds-install      | Install and configure AD DS, DNS, and promote to domain controller      |
| part-3-ous-users-gpos    | Create OUs, users, groups, and apply Group Policy Objects (GPOs)         |
| part-4-client-join       | Deploy client systems and join them to the Active Directory domain       |
| part-5-bitlocker         | Configure BitLocker encryption via GPO and verify TPM-based enforcement |
| main                     | Overview and entry point (this document)                                |

Each branch contains its own README and image assets for documentation and clarity.

---

## Tools and Technologies

- Proxmox Virtual Environment
- Windows Server 2022 Datacenter Evaluation
- Windows 10 and 11 client virtual machines
- PowerShell
- Group Policy Management Console (GPMC)
- BitLocker with TPM 2.0

---

## Documentation Structure

Each branch includes the following elements:

- Summary of key tasks
- Commands executed (especially PowerShell)
- Visual verification through screenshots
- Optional scripting or automation techniques

---

## Security and Infrastructure Concepts

- Centralized identity and access management via AD DS
- Role-based access control (RBAC) using groups and OUs
- Domain-based security policy enforcement via GPOs
- TPM-integrated full-disk encryption with BitLocker
- Administrative task automation and system interrogation via PowerShell

---

## Repository Usage

To view the work done in a specific part:

1. Navigate to the Code tab.
2. Select the desired branch from the dropdown menu (for example, `part-2-adds-install`).
3. Open the README file to review the documentation and screenshots for that part.

---

## Related Projects

- [vms-containers](https://github.com/Tariq-homelab/vms-containers): VM and container provisioning in Proxmox
- [project-nas](https://github.com/Tariq-homelab/project-nas): TrueNAS SCALE storage implementation with SMB and NFS
- [project-vpn](https://github.com/Tariq-homelab/project-vpn): Remote VPN access using Tailscale

---

## Author

This project is part of a self-directed homelab series designed to demonstrate job-ready IT infrastructure skills.  
All configurations were performed and tested on real virtual machines in a Proxmox environment.
