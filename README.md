# Windows Server AD & BitLocker Lab

This project demonstrates a complete Windows Server 2022 lab environment configured for enterprise use. The focus is on deploying Active Directory Domain Services (AD DS) and implementing BitLocker full disk encryption using TPM 2.0.

Each part of the lab is broken into GitHub branches to show progress and isolate functional milestones.

---

## Part 1: VM Setup and TPM Verification

Note: The base Windows Server 2022 VM installation was completed in another project. For full installation and VM configuration steps, see:  
[homelab-vms-containers](https://github.com/Tariq-homelab/homelab-vms-containers)

### What Was Done

- Accessed the virtual machine through Proxmox Console (noVNC)
- Verified UEFI boot mode and Secure Boot status via System Information
- Confirmed presence and readiness of TPM 2.0 using PowerShell
- Collected a system information report using `Get-ComputerInfo`
- Captured screenshots for documentation

### Commands Used

```
Get-Tpm
Get-ComputerInfo > C:\Users\Public\system-info.txt
```

### Screenshots

| Description                        | File                                           |
|-----------------------------------|------------------------------------------------|
| System Information (UEFI Boot)    | images/01-System-Information-UEFI-TPM.png      |
| TPM Check and SystemInfo Export   | images/02-TPM-PowerShell-and-SystemInfo.png    |

---

## Next Step

Part 2: Active Directory Domain Services (AD DS) Setup
- Promote server to Domain Controller
- Configure root domain and DNS
- Establish basic OU structure

<!-- Part 1 branch confirmed -->
