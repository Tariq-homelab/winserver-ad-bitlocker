# BitLocker GPO Enforcement – Part 3

This section documents the full implementation of a Group Policy Object (GPO) that enforces BitLocker encryption on a Windows 10 domain-joined VM. All images and descriptions are based on actual system outputs.

---

## Procedures and Output

### 1. Create BitLocker Policy GPO

- Opened **Group Policy Management Console**
- Created a new GPO called `BitLocker Policy`
- Screenshot:  
  <img src="../images/01-create-bitlocker-policy-gpo.png" width="700"/>

---

### 2. Attach TPM Module to VM

- Enabled TPM 2.0 for the Windows 10 VM in **Proxmox** settings  
- Screenshot:  
  <img src="../images/02-add-tpm2-to-vm.png" width="700"/>

---

### 3. Require Startup Authentication

- Enabled GPO: **Require additional authentication at startup**
- Configured to allow TPM only (no PIN)
- Screenshot:  
  <img src="../images/03-require-authentication-at-startup.png" width="700"/>

---

### 4. Enable AD DS Recovery Key Backup

- Enabled GPO: **Save BitLocker recovery information to AD DS for OS drives**
- Ensures recovery keys are stored in **Active Directory**
- Screenshot:  
  <img src="../images/04-enable-recovery-info-in-ad.png" width="700"/>

---

### 5. Link GPO to Domain

- Linked the `BitLocker Policy` GPO to the domain `homelab.local`
- Screenshot:  
  <img src="../images/05-link-bitlocker-gpo-to-domain.png" width="700"/>

---

### 6. Rename Client Hostname

- Renamed the Windows 10 client hostname for easier AD identification
- Screenshot:  
  <img src="../images/06-rename-hostname.png" width="700"/>

---

### 7. Join Domain

- Joined the Windows 10 VM to the `homelab.local` domain
- Screenshot:  
  <img src="../images/07-domain-join.png" width="700"/>

---

### 8. Force GPO Update

- Ran `gpupdate /force` on the client to apply new policies
- Screenshot:  
  <img src="../images/08a-gpupdate-success.png" width="700"/>

---

### 9. Verify GPO with gpresult

- Ran `gpresult /h report.html` to confirm GPO application
- Verified applied GPO and user group memberships
- Screenshots:  
  <img src="../images/08b-gpresult-bitlocker-policy.png" width="700"/>  
  <img src="../images/08c-gpresult-user-groups.png" width="700"/>

---

### 10. Launch BitLocker

- Attempted to enable BitLocker via **Control Panel**
- Error occurred due to missing TPM configuration or delay
- Screenshot:  
  <img src="../images/09-enable-bitlocker.png" width="700"/>

---

### 11. Enable BitLocker without TPM (GPO Edit)

- Enabled policy: **Allow BitLocker without compatible TPM**
- Only enabled temporarily to bypass TPM check during testing
- Screenshot:  
  <img src="../images/10-allow-bitlocker-without-tpm.png" width="700"/>

---

### 12. Map Network Drive for Key Storage

- Created shared folder on NAS to store recovery keys
- Mapped Z: drive on client
- Screenshot:  
  <img src="../images/11-mapped-network-drive.png" width="700"/>

---

### 13. Save Recovery Key to NAS

- Saved recovery key to Z: drive during BitLocker setup
- Screenshot:  
  <img src="../images/12-save-bitlocker-recovery-key.png" width="700"/>

---

### 14. Restart Triggered by BitLocker Setup

- Client prompted for restart after enabling BitLocker
- Screenshot:  
  <img src="../images/13-Restart Required After BitLocker Setup.png" width="700"/>

---

### 15. BitLocker Encryption Status Verified

- Encryption progress and success confirmed via BitLocker UI
- Screenshot:  
  <img src="../images/14-BitLocker Encryption Confirmed.png" width="700"/>

---

### 16. Pre-Boot Authentication Prompt

- Verified TPM prompt upon reboot (pre-boot)
- Screenshot:  
  <img src="../images/14-BitLocker Pre-Boot Authentication Prompt.png" width="700"/>

---

### 17. Recovery Key Stored in AD DS

- Verified that recovery key was backed up to **Active Directory**
- Screenshot:  
  <img src="../images/15-Recovery Key Stored on Server.png" width="700"/>

---

### 18. Event Logging for BitLocker

- Enabled BitLocker logging to monitor status via Event Viewer
- Screenshot:  
  <img src="../images/16-enable-bitlocker-event-logging.png" width="700"/>

---

### 19. BitLocker Status Verified via PowerShell

- Used PowerShell: `Get-BitLockerVolume` to confirm encryption status
- Screenshot:  
  <img src="../images/17-bitlocker-policy-verification.png" width="700"/>

---

### 20. Retrieved Protector ID

- Used PowerShell: `manage-bde -protectors -get C:`
- Screenshot:  
  <img src="../images/18-get-protector-id.png" width="700"/>

---

### 21. gpresult Summary Output

- Verified policy enforcement summary via HTML report
- Screenshot:  
  <img src="../images/19-gpresult-summary-success.png" width="700"/>

---

### 22. gpresult Policy Application Status

- Verified all components of the BitLocker policy were applied successfully
- Screenshot:  
  <img src="../images/20-gpresult-bitlocker-policy-applied.png" width="700"/>  
  <img src="../images/21-gpresult-component-status-success.png" width="700"/>

---

## Next Steps – Part 4

Proceed to **Part 4: Active Directory Organizational Structure and Automation**. This next phase will focus on:

- Creating Organizational Units (OUs) for departments
- Adding users manually and via PowerShell scripting
- Applying user-level GPOs
- Practicing common AD maintenance tasks (resetting passwords, disabling users, etc.)

This concludes the GPO-level BitLocker enforcement and verification workflow.

