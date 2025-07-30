# BitLocker Group Policy Enforcement – Part 3

This section documents the implementation and enforcement of BitLocker encryption policies across the Windows 10 domain-joined client using Group Policy Objects (GPOs), Active Directory Domain Services (AD DS) integration, and TPM-based authentication.

## Objectives
- Create and configure a BitLocker policy via GPO.
- Enforce TPM startup authentication.
- Store recovery keys in Active Directory.
- Link policy to domain.
- Validate GPO delivery and BitLocker enforcement.

## Procedure

### 1. Create BitLocker Policy GPO
- Opened **Group Policy Management Console**.
- Created a new GPO named `BitLocker Policy`.

![1-create-gpo.png](../../images/1-create-gpo.png)

---

### 2. Attach TPM Module to VM
- Enabled **TPM 2.0** in Proxmox for the Windows 10 VM.

![2-enable-tpm-proxmox.png](../../images/2-enable-tpm-proxmox.png)

---

### 3. Require Startup Authentication
- Edited GPO to enable **"Require additional authentication at startup"**.
- Configured the policy to allow **TPM only**.

![3-require-authentication.png](../../images/3-require-authentication.png)

---

### 4. Enable AD DS Recovery Key Backup
- Enabled GPO: **"Save BitLocker recovery information to AD DS for OS drives"**.

![4-save-recovery-keys-to-ad.png](../../images/4-save-recovery-keys-to-ad.png)

---

### 5. Link GPO to Domain
- Linked `BitLocker Policy` GPO to the domain `homelab.local`.

![5-link-gpo.png](../../images/5-link-gpo.png)

---

### 6. Rename Hostname and Restart
- Renamed the Windows 10 client to a standardized hostname.
- Rebooted for domain join prep.

![6-rename-hostname.png](../../images/6-rename-hostname.png)

---

### 7. Join Client to Domain
- Joined the Windows 10 client to `homelab.local` domain.

![7-join-domain.png](../../images/7-join-domain.png)

---

### 8. Force GPO Update and Check Results
- Ran `gpupdate /force` and confirmed GPO via `rsop.msc`.

![8-gpupdate.png](../../images/8-gpupdate.png)  
![8-gpo-confirm-1.png](../../images/8-gpo-confirm-1.png)  
![8-gpo-confirm-2.png](../../images/8-gpo-confirm-2.png)

---

### 9. Launch BitLocker Setup
- Attempted to enable BitLocker from Control Panel.
- Encountered TPM error due to initial sync delay.

![9-enable-bitlocker.png](../../images/9-enable-bitlocker.png)

---

### 10. Retry After Reboot
- Rebooted the system and launched BitLocker successfully.

![10-bitlocker-success.png](../../images/10-bitlocker-success.png)

---

### 11. Save Recovery Key to Network Share
- Mapped drive to NAS as `Z:\`.
- Saved BitLocker recovery key `.txt` file.

![11-save-recovery-key-to-z.png](../../images/11-save-recovery-key-to-z.png)

---

### 12. Verify Recovery Key in AD
- Opened **Active Directory Users and Computers**.
- Viewed recovery key under computer object properties.

![12-ad-recovery-tab.png](../../images/12-ad-recovery-tab.png)

---

### 13. Confirm Encryption Status
- Viewed encryption status via Control Panel and `manage-bde`.

![13-encrypting-status.png](../../images/13-encrypting-status.png)

---

## Skills Demonstrated
- Group Policy authoring and linking
- BitLocker policy configuration
- TPM-based authentication
- Active Directory integration
- Recovery key backup to AD
- Network drive mapping
- Domain-joined client configuration

## Next Steps
Proceed to **Part 4** of the project, focusing on Active Directory administrative tasks:
- Create organizational units (OUs)
- Batch-create users
- Delegate control via groups
- Automate user provisioning using PowerShell

This will build essential sysadmin skills beyond BitLocker deployment.
