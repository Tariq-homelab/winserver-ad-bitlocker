# BitLocker Group Policy Enforcement – Part 3

This section documents the implementation and enforcement of BitLocker encryption policies across a Windows 10 domain-joined client using Group Policy Objects (GPOs), Active Directory Domain Services (AD DS), and TPM-based authentication. Recovery key storage is configured both in Active Directory and on a mapped NAS share.

---

## Objectives

- Configure a domain-level GPO for BitLocker.
- Enforce TPM-only startup authentication.
- Enable recovery key backup to AD DS.
- Join the client to the domain and apply GPOs.
- Launch BitLocker and verify recovery mechanisms.

---

## Procedure

### 1. Create BitLocker Group Policy

Opened Group Policy Management on the Domain Controller and created a new GPO named **BitLocker Policy**.

![1-create-gpo.png](./1-create-gpo.png)

---

### 2. Enable TPM for Client VM

Enabled TPM 2.0 in Proxmox for the Windows 10 virtual machine to support BitLocker authentication via hardware TPM.

![2-enable-tpm-proxmox.png](./2-enable-tpm-proxmox.png)

---

### 3. Configure Startup Authentication Policy

Edited the GPO to enable **"Require additional authentication at startup"** and allowed **TPM only**.

![3-require-authentication.png](./3-require-authentication.png)

---

### 4. Enable AD DS Recovery Key Backup

Configured the second GPO setting: **"Save BitLocker recovery information to AD DS for OS drives"**, ensuring recovery keys are centrally stored in Active Directory.

![4-save-recovery-keys-to-ad.png](./4-save-recovery-keys-to-ad.png)

---

### 5. Link GPO to Domain

Linked the `BitLocker Policy` to the `homelab.local` domain root so that it applies to all relevant computer objects.

![5-link-gpo.png](./5-link-gpo.png)

---

### 6. Rename Hostname and Restart

Renamed the client VM to a standardized hostname for easier identification in Active Directory. Restarted the system to apply the new name.

![6-rename-hostname.png](./6-rename-hostname.png)

---

### 7. Join the Client to the Domain

Used the system properties wizard to join the Windows 10 VM to the `homelab.local` domain.

![7-join-domain.png](./7-join-domain.png)

---

### 8. Force GPO Update and Run RSOP

After logging in with a domain user account, ran `gpupdate /force` and launched **Resultant Set of Policy (rsop.msc)** to verify that BitLocker settings were successfully applied.

![8-rsop-confirmation.png](./8-rsop-confirmation.png)

---

### 9. Launch BitLocker Setup

Opened **Control Panel > BitLocker Drive Encryption** to start the encryption process. Encountered a TPM error on first attempt (due to policy sync delay).

![09-enable-bitlocker.png](./09-enable-bitlocker.png)

---

### 10. Reboot and Retry Encryption

After reboot, BitLocker launched successfully. The system prompted for recovery key backup.

![10-bitlocker-enabled.png](./10-bitlocker-enabled.png)

---

### 11. Save Recovery Key to NAS Share

Selected the mapped `Z:` drive (connected to the NAS SMB share) and saved the `.txt` recovery key file to the network location.

![11-save-to-zdrive.png](./11-save-to-zdrive.png)

---

### 12. Verify Recovery Key in AD DS

On the Domain Controller, opened **Active Directory Users and Computers**, navigated to the computer object, and confirmed the recovery key is stored under the **BitLocker Recovery** tab.

![12-ad-bitlocker-tab.png](./12-ad-bitlocker-tab.png)

---

### 13. Check BitLocker Encryption Status

On the client, opened **BitLocker Drive Encryption** again to confirm encryption was in progress. Also verified status using PowerShell with `manage-bde -status`.

![13-bitlocker-encrypting.png](./13-bitlocker-encrypting.png)

---

## Skills Demonstrated

- Group Policy authoring and enforcement
- TPM integration for secure boot authentication
- Active Directory object linking and policy application
- Centralized recovery key management (AD DS + NAS)
- Domain join and remote encryption configuration

---

## Next Steps

Part 4 will extend Active Directory functionality by simulating real-world user management:

- Create Organizational Units (OUs) for departments
- Add users manually and in bulk
- Use PowerShell scripts to automate account creation
- Delegate access control using security groups

This provides a more complete hands-on sysadmin experience using Windows Server 2022 and AD DS.

