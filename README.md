# Part 3 – BitLocker GPO Enforcement and Verification

This section demonstrates how BitLocker drive encryption was enforced on a Windows 10 domain-joined client using Group Policy configured via Windows Server 2022. All configurations were tested and confirmed using real encryption, Active Directory integration, and group policy reporting. Each procedure below includes a corresponding screenshot based on actual VM output, not just filename.

---

## Procedures and Evidence

### 1. Create BitLocker Policy GPO
- Opened **Group Policy Management Console**.
- Created a new GPO called `BitLocker Policy`.
- Screenshot: `<img src="../images/01-create-bitlocker-policy-gpo.png" width="700"/>`

---

### 2. Attach TPM Module to VM
- Enabled TPM 2.0 for the Windows 10 VM in Proxmox settings.
- Screenshot: `<img src="../images/02-add-tpm2-to-vm.png" width="700"/>`

---

### 3. Require Startup Authentication
- Enabled GPO: “Require additional authentication at startup”.
- Configured to allow TPM only.
- Screenshot: `<img src="../images/03-require-authentication-at-startup.png" width="700"/>`

---

### 4. Enable AD DS Recovery Key Backup
- Enabled GPO: “Save BitLocker recovery information to AD DS for OS drives”.
- Ensures that recovery keys are stored in Active Directory.
- Screenshot: `<img src="../images/04-enable-recovery-info-in-ad.png" width="700"/>`

---

### 5. Link GPO to Domain
- Linked `BitLocker Policy` GPO to `homelab.local` domain.
- Screenshot: `<img src="../images/05-link-bitlocker-gpo-to-domain.png" width="700"/>`

---

### 6. Rename Client Hostname
- Renamed the Windows 10 VM to a readable hostname before joining domain.
- Screenshot: `<img src="../images/06-rename-hostname.png" width="700"/>`

---

### 7. Join Domain
- Joined the Windows 10 client to the `homelab.local` domain.
- Screenshot: `<img src="../images/07-domain-join.png" width="700"/>`

---

### 8. Force GPO Update
- Ran `gpupdate /force` in terminal to apply latest GPOs.
- Screenshot: `<img src="../images/08a-gpupdate-success.png" width="700"/>`

---

### 9. Check GPO via gpresult
- Ran `gpresult /h` and generated HTML report.
- Verified that the BitLocker policy was applied.
- Screenshots:
  - `<img src="../images/08b-gpresult-bitlocker-policy.png" width="700"/>`
  - `<img src="../images/08c-gpresult-user-groups.png" width="700"/>`

---

### 10. Enable BitLocker Encryption
- Attempted to enable BitLocker from Control Panel.
- Error encountered: Device encryption support might be limited due to lack of compatible TPM or GPO conditions.
- Screenshot: `<img src="../images/09-enable-bitlocker.png" width="700"/>`

---

### 11. Allow BitLocker Without TPM
- Enabled additional GPO: “Allow BitLocker without a compatible TPM”.
- Required to allow software encryption fallback.
- Screenshot: `<img src="../images/10-allow-bitlocker-without-tpm.png" width="700"/>`

---

### 12. Map Network Drive
- Mapped a network share to store recovery key backup externally.
- Screenshot: `<img src="../images/11-mapped-network-drive.png" width="700"/>`

---

### 13. Save Recovery Key
- During BitLocker setup, chose to save recovery key to mapped network location.
- Screenshot: `<img src="../images/12-save-bitlocker-recovery-key.png" width="700"/>`

---

### 14. Restart Required
- BitLocker prompted restart to begin encryption process.
- Screenshot: `<img src="../images/13-Restart Required After BitLocker Setup.png" width="700"/>`

---

### 15. BitLocker Encryption Confirmed
- Verified BitLocker status via Control Panel: “BitLocker On”.
- Screenshot: `<img src="../images/14-BitLocker Encryption Confirmed.png" width="700"/>`

---

### 16. BitLocker Pre-Boot Authentication Prompt
- Captured the blue-screen pre-boot BitLocker password prompt after restart.
- Screenshot: `<img src="../images/14-BitLocker Pre-Boot Authentication Prompt.png" width="700"/>`

---

### 17. Recovery Key in AD
- Verified recovery key stored in Active Directory via `Active Directory Users and Computers`.
- Screenshot: `<img src="../images/15-Recovery Key Stored on Server.png" width="700"/>`

---

### 18. Enable BitLocker Event Logging
- Enabled security auditing and verified relevant event log categories.
- Screenshot: `<img src="../images/16-enable-bitlocker-event-logging.png" width="700"/>`

---

### 19. Confirm BitLocker Policy with PowerShell
- Ran `Get-BitLockerVolume` and `Get-BitLockerPolicy`.
- Verified encryption method and key protector types.
- Screenshot: `<img src="../images/17-bitlocker-policy-verification.png" width="700"/>`

---

### 20. Get Protector ID
- Used PowerShell to view recovery password protector ID.
- Screenshot: `<img src="../images/18-get-protector-id.png" width="700"/>`

---

### 21. gpresult Summary Report
- Ran `gpresult /h result.html` and opened the full summary report.
- Verified policy status and applied components.
- Screenshots:
  - `<img src="../images/19-gpresult-summary-success.png" width="700"/>`
  - `<img src="../images/20-gpresult-bitlocker-policy-applied.png" width="700"/>`
  - `<img src="../images/21-gpresult-component-status-success.png" width="700"/>`

---

## Result Summary

BitLocker drive encryption was successfully deployed via Group Policy and verified end-to-end:
- Encryption was activated and completed.
- Recovery key was stored on a network drive and in Active Directory.
- Group Policy and PowerShell commands confirmed policy application.
- Event logging was enabled for future auditing.

---

## Next Steps (Part 4 Preview)

In the next phase, the following Active Directory administrative tasks will be completed:

- Design a basic organizational structure:
  - Create Organizational Units (OUs) for departments (e.g., IT, HR, Finance).
  - Create user accounts and assign them to the appropriate OUs.

- Implement automation:
  - Use PowerShell scripts to batch-create users with attributes (name, password, department).
  - Assign group memberships and logon restrictions.

- Simulate real-world AD management:
  - Use Group Policy Objects to restrict/control user environments.
  - Practice user password reset, disable/enable accounts, and delegation.

These tasks will demonstrate core sysadmin competencies often required in enterprise environments.

