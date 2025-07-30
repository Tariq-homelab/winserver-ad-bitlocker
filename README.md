# Part 3: BitLocker GPO Enforcement and Verification

This phase demonstrates enforcing BitLocker encryption on domain-joined clients using Group Policy, with recovery key backup to Active Directory. A Windows 10 Pro VM was used to validate that the BitLocker GPO was applied, encryption initiated, and recovery information stored both on a shared folder and within AD DS.

---

## Objectives

- Create and link a Group Policy to enforce BitLocker
- Enable recovery key backup to Active Directory
- Trigger encryption on a domain-joined Windows 10 client
- Save the recovery key to a network share
- Confirm encryption status and AD DS recovery key storage
- Verify policy application using `gpresult` and PowerShell

---

## Procedures and Evidence

1. **Create BitLocker Policy GPO**
   - Created new GPO: `BitLocker Policy`
   - Screenshot: `01-create-bitlocker-policy-gpo.png`

2. **Attach TPM Module to VM**
   - Enabled TPM 2.0 on the Windows 10 VM via Proxmox
   - Screenshot: `02-add-tpm2-to-vm.png`

3. **Require Startup Authentication**
   - Enabled policy to require authentication at startup
   - Screenshot: `03-require-authentication-at-startup.png`

4. **Enable AD DS Recovery Key Backup**
   - Configured BitLocker recovery key backup to AD DS
   - Screenshot: `04-enable-recovery-info-in-ad.png`

5. **Link GPO to Domain**
   - Linked the GPO to `homelab.local`
   - Screenshot: `05-link-bitlocker-gpo-to-domain.png`

6. **Rename Client Hostname**
   - Renamed the Windows 10 client for clarity in AD
   - Screenshot: `06-rename-hostname.png`

7. **Join Domain**
   - Joined the Windows 10 VM to the domain
   - Screenshot: `07-domain-join.png`

8. **Force GPO Update**
   - Ran `gpupdate /force` to pull the new BitLocker policy
   - Screenshot: `08a-gpupdate-success.png`

9. **Verify GPO Application**
   - Used `gpresult /h report.html`
   - Verified user and computer policies
   - Screenshots: `08b-gpresult-bitlocker-policy.png`, `08c-gpresult-user-groups.png`

10. **Enable BitLocker**
    - Launched the BitLocker setup wizard
    - Screenshot: `09-enable-bitlocker.png`

11. **Allow BitLocker Without TPM (if needed)**
    - Allowed fallback configuration for virtual TPM
    - Screenshot: `10-allow-bitlocker-without-tpm.png`

12. **Map Network Drive**
    - Mapped server folder for saving recovery key (Y:)
    - Screenshot: `11-mapped-network-drive.png`

13. **Save Recovery Key**
    - Saved recovery key to network share
    - Screenshot: `12-save-bitlocker-recovery-key.png`

14. **BitLocker Setup Complete**
    - Restarted after setup
    - Screenshot: `13-Restart Required After BitLocker Setup.png`

15. **Encryption Confirmation**
    - Confirmed encryption status via `manage-bde -status`
    - Screenshot: `14-BitLocker Encryption Confirmed.png`

16. **Pre-Boot Authentication Prompt**
    - Screenshot taken during bootup with BitLocker prompt
    - Screenshot: `14-BitLocker Pre-Boot Authentication Prompt.png`

17. **Recovery Key on Server**
    - Verified recovery key file saved to mapped drive
    - Screenshot: `15-Recovery Key Stored on Server.png`

18. **Enable BitLocker Event Logging**
    - Verified event log channels via `wevtutil`
    - Screenshot: `16-enable-bitlocker-event-logging.png`

19. **Verify BitLocker Policy via PowerShell**
    - Used `Get-BitLockerVolume` and protector ID commands
    - Screenshot: `17-bitlocker-policy-verification.png`, `18-get-protector-id.png`

20. **Confirm GPO via HTML Report**
    - Opened `gpresult.html` to confirm BitLocker GPO applied
    - Screenshots:
      - `19-gpresult-summary-success.png`
      - `20-gpresult-bitlocker-policy-applied.png`
      - `21-gpresult-component-status-success.png`

---

## Technical Highlights

- **Group Policy:** Enforced encryption and automated recovery key storage
- **AD DS Integration:** Key is stored under the client’s computer object in Active Directory
- **Network Share:** Key saved to a secure share as backup
- **Logging:** Event channels and PowerShell used to verify enforcement
- **GPO Verification:** HTML report (`gpresult`) confirms BitLocker policy application

---

## Next Steps: Part 4

The next section will transition from BitLocker enforcement to Active Directory administration tasks. Part 4 will include:

- Creating Organizational Units (OUs)
- Defining departments and roles
- Adding users manually and via PowerShell scripting
- Applying GPOs to OUs for realistic AD delegation
- Logging and managing BitLocker recovery keys per user/device

This transition focuses on real-world sysadmin responsibilities.

---
