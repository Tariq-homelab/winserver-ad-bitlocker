# Part 3: BitLocker GPO Enforcement and Verification

This documentation outlines the process of enforcing BitLocker encryption via Group Policy in an Active Directory environment, followed by verification of policy application and encryption behavior on a domain-joined Windows 10 client.

---

## 1. Create a GPO for BitLocker

A new GPO named **BitLocker Policy** was created within the Group Policy Management Console.

![](images/01-create-bitlocker-policy-gpo.png)

---

## 2. Add TPM 2.0 Device to VM

The Windows 10 Pro client VM was configured in Proxmox to include a virtual TPM 2.0 module to support hardware-based BitLocker encryption.

![](images/02-add-tpm2-to-vm.png)

---

## 3. Require Startup Authentication

Group Policy setting **"Require additional authentication at startup"** was enabled with TPM selected to enforce pre-boot authentication.

![](images/03-require-authentication-at-startup.png)

---

## 4. Save Recovery Information to AD

Group Policy setting **"Save BitLocker recovery information to AD DS"** was enabled to allow storing recovery keys centrally in Active Directory.

![](images/04-enable-recovery-info-in-ad.png)

---

## 5. Link GPO to Domain Root

The BitLocker Policy GPO was linked to the root of the domain (`homelab.local`) to apply settings across all domain-joined clients.

![](images/05-link-bitlocker-gpo-to-domain.png)

---

## 6. Rename Client Hostname

Before joining the domain, the Windows 10 client was assigned a consistent hostname.

![](images/06-rename-hostname.png)

---

## 7. Join Windows 10 Client to Domain

The system was successfully joined to the domain `homelab.local`.

![](images/07-domain-join.png)

---

## 8. Refresh and Check GPO Application

Group Policy was refreshed using `gpupdate /force`, and `gpresult /r` confirmed that the BitLocker Policy GPO was applied to the machine.

![](images/08a-gpupdate-success.png)  
![](images/08b-gpresult-bitlocker-policy.png)

---

## 9. Verify GPO Security Filtering

The GPO’s scope and security filtering were validated in GPMC to confirm that it applies to authenticated users and computers.

![](images/08c-gpresult-user-groups.png)

---

## 10. Launch BitLocker and Observe Prompt

BitLocker was launched on the client machine. Due to TPM-only enforcement, a TPM-based confirmation screen appeared.

![](images/09-enable-bitlocker.png)

---

## 11. (Optional) TPM-less Scenario (Not Used)

The GPO setting to allow BitLocker without a compatible TPM was reviewed but left disabled to enforce TPM-only compliance.

![](images/10-allow-bitlocker-without-tpm.png)

---

## 12. Validate Recovery Key Storage Option

During BitLocker setup, the wizard indicated that the recovery key would be stored in Active Directory, confirming GPO enforcement.

![](images/11-mapped-network-drive.png)  
![](images/12-save-bitlocker-recovery-key.png)

---

## 13. Restart Prompt After Setup

After completing BitLocker configuration, a restart was required to begin encryption.

![](images/13-Restart Required After BitLocker Setup.png)

---

## 14. BitLocker Status: Encryption Started

Upon reboot, BitLocker began encrypting the drive. Status was shown directly in the BitLocker control panel.

![](images/14-BitLocker Encryption Confirmed.png)

---

## 15. Pre-Boot Authentication Prompt (TPM)

A pre-boot authentication prompt confirmed the use of TPM for boot security.

![](images/14-BitLocker Pre-Boot Authentication Prompt.png)

---

## 16. Recovery Key Stored in Active Directory

The client machine’s recovery key was successfully found within the corresponding computer object in Active Directory.

![](images/15-Recovery Key Stored on Server.png)

---

## 17. Enable Event Logging (Optional)

BitLocker-related event logging was enabled to assist with auditing and troubleshooting.

![](images/16-enable-bitlocker-event-logging.png)

---

## 18. PowerShell: Verify Protection Status

Used PowerShell to verify that the volume was protected by BitLocker:

```powershell
Get-BitLockerVolume

---

19. Retrieve Key Protector ID  
Command used: (Get-BitLockerVolume -MountPoint "C:").KeyProtector  
Screenshot: images/18-get-protector-id.png

20. Confirm gpresult Summary  
Screenshots:  
- images/19-gpresult-summary-success.png  
- images/20-gpresult-bitlocker-policy-applied.png  
- images/21-gpresult-component-status-success.png

SUMMARY:  
- Group Policy settings for BitLocker were created, linked, and enforced.  
- TPM-based protection and recovery key storage in AD were verified.  
- Encryption was initiated and confirmed via both UI and PowerShell.  
- GPO application confirmed via gpresult, PowerShell, and AD inspection.

NEXT STEPS:  
Part 4 will focus on Active Directory user and group administration, OU structuring, and automation using PowerShell.

