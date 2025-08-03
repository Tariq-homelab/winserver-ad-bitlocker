# Windows Server 2022: Active Directory and BitLocker Lab

This repository documents a modular Windows Server 2022 lab environment focused on enterprise identity, access management, and data protection. It demonstrates practical skills in setting up Active Directory Domain Services (AD DS), configuring DNS, implementing Group Policy, and managing BitLocker encryption using TPM.

Each part of the lab is contained in its own Git branch to provide a clean, modular structure and highlight each stage independently.

---

## Objectives

- Deploy a Windows Server 2022 VM with virtualization features validated
- Install and promote Active Directory Domain Services (AD DS)
- Configure DNS and domain controller settings
- Apply Group Policies for encryption and access management
- Implement BitLocker full-disk encryption with TPM and AD-integrated recovery keys
- Demonstrate real-world IT infrastructure skills in a Proxmox-based environment

---

## Branch Structure

| Branch Name | Purpose |
|-------------|---------|
| [`part-1`](https://github.com/Tariq-homelab/winserver-ad-bitlocker/tree/part-1) | Validate UEFI, Secure Boot, and TPM 2.0 inside a Windows Server 2022 VM |
| [`part-2`](https://github.com/Tariq-homelab/winserver-ad-bitlocker/tree/part-2) | Install AD DS, promote to Domain Controller, and configure DNS |
| [`part-3`](https://github.com/Tariq-homelab/winserver-ad-bitlocker/tree/part-3) | Configure BitLocker via GPO, enforce encryption, and store recovery keys in AD |
| `main` | Overview and table of contents (this document) |

---

## How to Navigate

To explore each part of the project:

1. Go to the Code tab.
2. Use the branch dropdown to select the part you want to view.
3. Open the `README.md` in that branch to see full documentation and screenshots.

---

## Tools and Technologies

- Proxmox Virtual Environment (VE)
- Windows Server 2022 Datacenter Evaluation
- PowerShell
- Group Policy Management Console (GPMC)
- DNS Manager
- BitLocker
- TPM 2.0 emulation (via Proxmox)

---

## Related Projects

- [`vms-containers`](https://github.com/Tariq-homelab/vms-containers): Proxmox VM and container provisioning
- [`project-nas`](https://github.com/Tariq-homelab/project-nas): TrueNAS SCALE deployment for SMB and NFS storage
- [`project-vpn`](https://github.com/Tariq-homelab/project-vpn): Secure remote access to homelab using Tailscale VPN

---

## Author

This project is part of a self-directed homelab series designed to showcase job-ready IT infrastructure skills in identity management, virtualization, and data protection.  
All configurations were performed and tested on real VMs in a Proxmox environment.

---

## Coming Soon

The final part of this project will cover:

- Organizational Units (OUs), domain users, and security groups
- Group Policy Objects (GPOs) targeted to specific OUs
- PowerShell automation for bulk user creation
- Optional password complexity and login restriction policies

Each part follows the same documentation structure with screenshots and technical notes.
