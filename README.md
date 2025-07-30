
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

## 1. Launch BitLocker Setup
BitLocker was launched via the Control Panel on the domain-joined client.
<img src="images/01-Launch BitLocker Setup.png" width="700"/>

## 2. BitLocker Setup Wizard: TPM Detected
The setup wizard confirmed that a TPM was detected and required no additional PIN or USB.
<img src="images/02-BitLocker Wizard with TPM Detected.png" width="700"/>

## 3. Encryption Choice: Used Space Only
"Encrypt used disk space only" was selected for faster encryption on new devices.
<img src="images/03-Encrypt Used Disk Space Only.png" width="700"/>

## 4. Encryption Mode: New (XTS-AES)
Selected "New encryption mode" (XTS-AES) as the target machine is modern and supports it.
<img src="images/04-Encryption Mode Selection.png" width="700"/>

## 5. Run BitLocker System Check
Enabled the system check option to verify readiness before encryption.
<img src="images/05-Run BitLocker System Check.png" width="700"/>

## 6. Save Recovery Key: Choose Location
Selected a custom network path as defined by GPO for saving the recovery key.
<img src="images/06-Choose Recovery Key Location.png" width="700"/>

## 7. Network Drive Mapped
Confirmed that the SMB network share was accessible and mapped successfully.
<img src="images/07-Network Drive Mapped for Key Export.png" width="700"/>

## 8. Save Recovery Key to Network
BitLocker exported the recovery key to the mapped SMB share.
<img src="images/08-Recovery Key Saved to Network.png" width="700"/>

## 9. Launching BitLocker Triggers GPO
BitLocker launched with pre-configured options set via Group Policy. Manual options were greyed out.
<img src="images/09-Enable BitLocker.png" width="700"/>

## 10. AD DS Recovery Key Storage Confirmed
Opened Active Directory Users and Computers (ADUC) to view the recovery key.
<img src="images/10-View Recovery Key in ADUC.png" width="700"/>

## 11. Select Network Share for Recovery Key
The wizard showed the SMB path defined in GPO during the save step.
<img src="images/11-Select Network Share for Recovery Key.png" width="700"/>

## 12. Confirm Saved Recovery Key File
The recovery key file was successfully saved on the network share, confirming key export to the SMB location.
<img src="images/12-Recovery Key File Saved on Network.png" width="700"/>

## 13. Restart Prompt After Setup
After applying the BitLocker Group Policy settings, the system prompted for a restart to begin the encryption process.
<img src="images/13-Restart Required After Bitlocker Setup.png" width="700"/>

## 14. BitLocker Status: Encryption Started
Upon reboot, the BitLocker control panel displayed the status "Encryption in progress," confirming that drive encryption had begun.
<img src="images/14-BitLocker Encryption Confirmed.png" width="700"/>

## 15. Pre-Boot Authentication Prompt (TPM)
The system displayed a pre-boot authentication screen confirming that TPM was used for BitLocker protection, as configured in the Group Policy.
<img src="images/14-BitLocker Pre-Boot Authentication Prompt.png" width="700"/>

## 16. Recovery Key Stored in Active Directory
The recovery key was confirmed to be stored in Active Directory. It was accessed through the computer objects properties under the "BitLocker Recovery" tab in Active Directory Users and Computers (ADUC).
<img src="images/15-Recovery Key Stored on Server.png" width="700"/>

## 17. Enable Event Logging (Optional)
BitLocker-related event logging was enabled to assist with auditing and troubleshooting.
<img src="images/16-Event Viewer Logging Enabled.png" width="700"/>

## 18. Confirm BitLocker Event ID
Verified the Event ID 845 (BitLocker status) and 851 (Volume locked) in the Windows Event Viewer.
<img src="images/17-BitLocker Event Viewer Logs.png" width="700"/>

## 19. Verify GPO Configuration
Opened Group Policy Management Editor on the server to review the policy settings.
<img src="images/18-Group Policy Review on Server.png" width="700"/>

## 20. Test Another User Login
Logged in as another domain user on the encrypted machine to confirm policy enforcement.
<img src="images/19-Login with Another Domain User.png" width="700"/>

---

## Summary

- Group Policy settings for BitLocker were created, linked, and enforced successfully.
- TPM-based protection was confirmed via pre-boot prompt.
- Recovery key was saved both to a network share and to Active Directory.
- Encryption status was verified through GUI and PowerShell.
- Auditing was enabled and tested.
- gpresult confirmed policy application from AD DS.

---

## Next Steps

Part 4 will focus on Active Directory user and group administration, OU structuring, and PowerShell-based automation.
