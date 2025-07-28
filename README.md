# Windows Server 2022: Active Directory and BitLocker Lab

This repository documents a modular Windows Server 2022 lab environment focused on enterprise identity, access management, and data protection. It demonstrates practical skills in setting up Active Directory Domain Services (AD DS), configuring DNS, and preparing for Group Policy and BitLocker implementation.

Each part of the lab is contained in its own Git branch to provide a clean, modular structure and highlight each stage independently.

---

## Objectives

- Deploy a Windows Server 2022 VM with virtualization features validated
- Install and promote Active Directory Domain Services (AD DS)
- Configure DNS and domain controller settings
- Prepare the foundation for OUs, Group Policies, and BitLocker
- Demonstrate real-world IT infrastructure skills in a Proxmox-based environment

---

## Branch Structure

| Branch Name        | Purpose                                                                 |
|--------------------|-------------------------------------------------------------------------|
| `part-1-vm-setup`  | Validate UEFI, Secure Boot, and TPM 2.0 inside a Windows Server 2022 VM |
| `part-2`           | Install AD DS, promote to Domain Controller, and configure DNS          |
| `main`             | Overview and table of contents (this document)                          |

---

## How to Navigate

To explore each part of the project:

1. Go to the Code tab
2. Use the branch dropdown to select the part you want to view
3. Open the `README.md` in that branch to see full documentation and screenshots

---

## Completed Parts

### `part-1-vm-setup`
Set up the Windows Server 2022 VM with Secure Boot, UEFI, and TPM 2.0 support inside Proxmox. This provides the foundation for BitLocker testing later in the lab.

[View branch](https://github.com/Tariq-homelab/winserver-ad-bitlocker/tree/part-1-vm-setup)

### `part-2`
Installed Active Directory Domain Services (AD DS), configured a static IP, and promoted the server to a Domain Controller for `homelab.local`. Also verified DNS Forward Lookup Zones and domain functionality.

[View branch](https://github.com/Tariq-homelab/winserver-ad-bitlocker/tree/part-2)

---

## Tools and Technologies

- Proxmox Virtual Environment (VE)
- Windows Server 2022 Datacenter Evaluation
- PowerShell
- Group Policy Management Console (GPMC)
- DNS Manager
- TPM 2.0 emulation (via Proxmox)

---

## Related Projects

- [`vms-containers`](https://github.com/Tariq-homelab/vms-containers): Proxmox VM and container provisioning
- [`project-nas`](https://github.com/Tariq-homelab/project-nas): TrueNAS SCALE deployment for SMB and NFS storage
- [`project-vpn`](https://github.com/Tariq-homelab/project-vpn): Secure remote access to homelab using Tailscale VPN

---

## Author

This project is part of a self-directed homelab series designed to showcase job-ready IT infrastructure skills in identity management, virtualization, and security.  
All configurations were performed and tested on real VMs in a Proxmox environment.

---

## Coming Soon

Additional branches will cover:

- Organizational Units (OUs), domain users, and security groups
- Group Policy Objects (GPOs) for access control and configuration
- BitLocker full-disk encryption with TPM and recovery key storage in AD
- Domain-joined client testing (Windows 10/11)

Each future part will follow the same documentation structure with screenshots and practical configuration examples.
