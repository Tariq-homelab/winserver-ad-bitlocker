# Part 3 – BitLocker GPO Enforcement and Verification

This section covers the implementation of Group Policy Objects (GPOs) for BitLocker drive encryption, applying the policies to a domain-joined Windows 10 client, verifying the enforcement, and confirming backup of the recovery key to Active Directory.

---

## Procedures and Evidence

### 1. Create BitLocker Policy GPO
- Created new GPO: `BitLocker Policy`
- <img src="images/01-create-bitlocker-policy-gpo.png" width="700"/>

### 2. Attach TPM Module to VM
- Enabled TPM 2.0 on the Windows 10 VM via Proxmox
- <img src="images/02-add-tpm2-to-vm.png" width="700"/>

### 3. Require Startup Authentication
- Enabled policy to require authentication at startup
- <img src="images/03-require-authentication-at-startup.png" width="700"/>

### 4. Enable AD DS Recovery Key Backup
- Configured BitLocker recovery key backup to AD DS
- <img src="images/04-enable-recovery-info-in-ad.png" width="700"/>

### 5. Link GPO to Domain
- Linked the GPO to `homelab.local`
- <img src="images/05-link-bitlocker-gpo-to-domain.png" width="700"/>

### 6. Rename Client Hostname
- Renamed the Windows 10 client for clarity in AD
- <img src="images/06-rename-hostname.png" width="700"/>

### 7. Join Domain
- Joined the Windows 10 VM to the domain
- <img src="images/07-domain-join.png" width="700"/>

### 8. Force GPO Update
- Ran `gpupdate /force` to pull the new BitLocker policy
- <img src="images/08a-gpupdate-success.png" width="700"/>

### 9. Verify GPO Application via `gpresult`
- Confirmed user group membership
- <img src="images/08c-gpresult-user-groups.png" width="700"/>
- Verified BitLocker GPOs applied
- <img src="images/08b-gpresult-bitlocker-policy.png" width="700"/>

---

## BitLocker Activation and Monitoring

### 10. Allow BitLocker Without TPM
- Enabled GPO fallback option for machines without compatible TPM
- <img src="images/10-allow-bitlocker-without-tpm.png" width="700"/>

### 11. Enable BitLocker Encryption
- Launched BitLocker encryption process via Control Panel
- <img src="images/09-enable-bitlocker.png" width="700"/>

### 12. Map Network Drive to Save Recovery Key
- Mapped shared folder from the server
- <img src="images/11-mapped-network-drive.png" width="700"/>

### 13. Save BitLocker Recovery Key
- Saved recovery key to the mapped network drive
- <img src="images/12-save-bitlocker-recovery-key.png" width="700"/>

### 14. Restart Client to Trigger Encryption
- Restarted Windows after encryption setup
- <img src="images/13-Restart-Required-After-BitLocker-Setup.png" width="700"/>

### 15. Confirm Pre-Boot Authentication Prompt
- Verified encryption took effect and authentication was required
- <img src="images/14-BitLocker-Pre-Boot-Authentication-Prompt.png" width="700"/>

### 16. Confirm BitLocker Status
- Checked BitLocker status to confirm encryption success
- <img src="images/14-BitLocker-Encryption-Confirmed.png" width="700"/>

---

## Recovery Key Handling and AD DS Integration

### 17. Verify Recovery Key Stored in Active Directory
- Confirmed AD DS received recovery key metadata
- <img src="images/15-Recovery-Key-Stored-on-Server.png" width="700"/>

### 18. Enable Event Logging for BitLocker
- Verified audit policies for tracking BitLocker-related events
- <img src="images/16-enable-bitlocker-event-logging.png" width="700"/>

### 19. Confirm BitLocker GPO Configuration
- Reviewed GPOs for compliance and troubleshooting
- <img src="images/17-bitlocker-policy-verification.png" width="700"/>

### 20. Validate Key Protector ID
- Used PowerShell to list protectors and verify key storage
- <img src="images/18-get-protector-id.png" width="700"/>

---

## Final Validation

### 21. Generate HTML Policy Report with `gpresult`
- Ran `gpresult /h result.html` and opened report
- <img src="images/19-gpresult-summary-success.png" width="700"/>
- <img src="images/20-gpresult-bitlocker-policy-applied.png" width="700"/>
- <img src="images/21-gpresult-component-status-success.png" width="700"/>

---

## ✅ Summary

This section demonstrated how to enforce BitLocker encryption across domain-joined clients using Active Directory Group Policy. Recovery keys were stored both on a secure network share and backed up to AD DS. The `gpresult` tool was used to validate policy enforcement end-to-end.

---

## ▶️ Next Steps (Part 4 Preview)

Part 4 will focus on core Active Directory skills:
- Creating Organizational Units (OUs)
- Structuring users into departments (e.g., HR, IT, Sales)
- Adding users manually and via PowerShell scripts
- Assigning GPOs to specific OUs for practical delegation

```powershell
# Sample task from Part 4
New-ADUser -Name "John Smith" -SamAccountName jsmith -UserPrincipalName jsmith@homelab.local -Path "OU=IT,DC=homelab,DC=local"
```

This will simulate day-to-day sysadmin responsibilities in a real-world enterprise AD environment.

