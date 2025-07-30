# BitLocker Group Policy Configuration and Validation

## Objectives

This lab demonstrates how to configure and enforce BitLocker drive encryption using Group Policy in a Windows Server 2022 Active Directory environment. It includes the following goals:

- Enforce TPM-based startup authentication for operating system drives.
- Configure BitLocker recovery key backup to Active Directory.
- Save recovery keys to a designated SMB network share.
- Verify encryption status through both GUI and PowerShell.
- Confirm storage of recovery keys in AD DS.
- Ensure auditing is enabled for security compliance.

---

## 1. Create BitLocker Policy GPO

A new Group Policy Object was created named "BitLocker Policy" to manage encryption settings.

<img src="images/01-create-bitlocker-policy-gpo.png" width="700"/>

## 2. Add TPM 2.0 to VM

The virtual machine was configured to include a TPM 2.0 device via Proxmox.

<img src="images/02-add-tpm2-to-vm.png" width="700"/>

## 3. Require Authentication at Startup

The policy "Require additional authentication at startup" was enabled and set to allow TPM only or TPM + PIN.

<img src="images/03-require-authentication-at-startup.png" width="700"/>

## 4. Enable Recovery Info in AD

Configured policy to store BitLocker recovery keys in Active Directory.

<img src="images/04-enable-recovery-info-in-ad.png" width="700"/>

## 5. Link BitLocker GPO to Domain

The GPO was successfully linked to the domain to enforce the settings.

<img src="images/05-link-bitlocker-gpo-to-domain.png" width="700"/>

## 6. Rename Hostname

The system hostname was renamed to follow lab naming standards.

<img src="images/06-rename-hostname.png" width="700"/>

## 7. Domain Join

The Windows 10 client was joined to the Active Directory domain.

<img src="images/07-domain-join.png" width="700"/>

## 8. Force Group Policy Update

Used `gpupdate /force` to apply new GPO settings.

<img src="images/08a-gpupdate-success.png" width="700"/>

## 8b. Confirm GPO BitLocker Policy

Used `gpresult` to confirm that BitLocker GPO was successfully applied to the client.

<img src="images/08b-gpresult-bitlocker-policy.png" width="700"/>

## 8c. Confirm GPO User Group

Validated the user group policy scope.

<img src="images/08c-gpresult-user-groups.png" width="700"/>

## 9. Enable BitLocker

BitLocker setup was launched and confirmed TPM availability.

<img src="images/09-enable-bitlocker.png" width="700"/>

## 10. Allow BitLocker Without TPM (GPO Fallback)

Displayed policy allowing BitLocker without a compatible TPM (optional testing scenario).

<img src="images/10-allow-bitlocker-without-tpm.png" width="700"/>

## 11. Mapped Network Drive

An SMB network share was mapped to store recovery keys.

<img src="images/11-mapped-network-drive.png" width="700"/>

## 12. Save BitLocker Recovery Key

The wizard showed the SMB path defined in GPO during the save step.

<img src="images/12-save-bitlocker-recovery-key.png" width="700"/>

## 13. Restart Required After BitLocker Setup

After applying the BitLocker Group Policy settings, the system prompted for a restart to begin the encryption process.

<img src="images/13-Restart Required After BitLocker Setup.png" width="700"/>

## 14. BitLocker Encryption Confirmed

Upon reboot, the BitLocker control panel displayed the status "Encryption in progress," confirming that drive encryption had begun.

<img src="images/14-BitLocker Encryption Confirmed.png" width="700"/>

## 15. Recovery Key Stored on Server

The recovery key file was successfully saved on the network share, confirming key export to the SMB location.

<img src="images/15-Recovery Key Stored on Server.png" width="700"/>

## 16. Enable BitLocker Event Logging

Security logging for BitLocker activity was enabled via Group Policy.

<img src="images/16-enable-bitlocker-event-logging.png" width="700"/>

## 17. BitLocker Policy Verification

Final GPO confirmation for BitLocker drive encryption enforcement.

<img src="images/17-bitlocker-policy-verification.png" width="700"/>

## 18. Get Protector ID via PowerShell

Used PowerShell to retrieve BitLocker protector ID.

<img src="images/18-get-protector-id.png" width="700"/>

## 19. Gpresult Summary: Success

Final GPO report shows all policies applied successfully.

<img src="images/19-gpresult-summary-success.png" width="700"/>

## 20. BitLocker Policy Applied

Confirmed BitLocker policy status applied to current user and computer context.

<img src="images/20-gpresult-bitlocker-policy-applied.png" width="700"/>

## 21. Component Status Success

Verified all BitLocker components were reported successful.

<img src="images/21-gpresult-component-status-success.png" width="700"/>

---

## Next Steps

In future extensions of this project, additional administrative tasks will be performed including:

- Bulk creation of Active Directory users and OUs
- Advanced GPO management (e.g., software deployment, script enforcement)
- Audit log collection and reporting
- Proxmox snapshot backup automation

This concludes Part 3: BitLocker GPO enforcement and validation.
