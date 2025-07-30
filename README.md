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
![](images/01-Launch BitLocker Setup.png)
## 2. BitLocker Setup Wizard: TPM Detected
The setup wizard confirmed that a TPM was detected and required no additional PIN or USB.
![](images/02-BitLocker Wizard with TPM Detected.png)
## 3. Encryption Choice: Used Space Only
"Encrypt used disk space only" was selected for faster encryption on new devices.
![](images/03-Encrypt Used Disk Space Only.png)
## 4. Encryption Mode: New (XTS-AES)
Selected "New encryption mode" (XTS-AES) as the target machine is modern and supports it.
![](images/04-Encryption Mode Selection.png)
## 5. Run BitLocker System Check
Enabled the system check option to verify readiness before encryption.
![](images/05-Run BitLocker System Check.png)
## 6. Save Recovery Key: Choose Location
Selected a custom network path as defined by GPO for saving the recovery key.
![](images/06-Choose Recovery Key Location.png)
## 7. Network Drive Mapped
Confirmed that the SMB network share was accessible and mapped successfully.
![](images/07-Network Drive Mapped for Key Export.png)
## 8. Save Recovery Key to Network
BitLocker exported the recovery key to the mapped SMB share.
![](images/08-Recovery Key Saved to Network.png)
## 9. Launching BitLocker Triggers GPO
BitLocker launched with pre-configured options set via Group Policy. Manual options were greyed out.
![](images/09-Enable BitLocker.png)
## 10. AD DS Recovery Key Storage Confirmed
Opened Active Directory Users and Computers (ADUC) to view the recovery key.
![](images/10-View Recovery Key in ADUC.png)
## 11. Select Network Share for Recovery Key
The wizard showed the SMB path defined in GPO during the save step.
![](images/11-Select Network Share for Recovery Key.png)
## 12. Confirm Saved Recovery Key File
The recovery key file was successfully saved on the network share, confirming key export to the SMB
location.
![](images/12-Recovery Key File Saved on Network.png)
## 13. Restart Prompt After Setup
After applying the BitLocker Group Policy settings, the system prompted for a restart to begin the encryption
process.
![](images/13-Restart Required After Bitlocker Setup.png)
## 14. BitLocker Status: Encryption Started
Upon reboot, the BitLocker control panel displayed the status "Encryption in progress," confirming that drive
encryption had begun.
![](images/14-BitLocker Encryption Confirmed.png)
## 15. Pre-Boot Authentication Prompt (TPM)
The system displayed a pre-boot authentication screen confirming that TPM was used for BitLocker
protection, as configured in the Group Policy.
![](images/14-BitLocker Pre-Boot Authentication Prompt.png)
## 16. Recovery Key Stored in Active Directory
The recovery key was confirmed to be stored in Active Directory. It was accessed through the computer
objects properties under the "BitLocker Recovery" tab in Active Directory Users and Computers (ADUC).
![](images/15-Recovery Key Stored on Server.png)
## 17. Enable Event Logging (Optional)
BitLocker-related event logging was enabled to assist with auditing and troubleshooting.
![](images/16-Event Viewer Logging Enabled.png)
## 18. Confirm BitLocker Event ID
Verified the Event ID 845 (BitLocker status) and 851 (Volume locked) in the Windows Event Viewer.
![](images/17-BitLocker Event Viewer Logs.png)
## 19. Verify GPO Configuration
Opened Group Policy Management Editor on the server to review the policy settings.
![](images/18-Group Policy Review on Server.png)
## 20. Test Another User Login
Logged in as another domain user on the encrypted machine to confirm policy enforcement.
![](images/19-Login with Another Domain User.png)
---
## Next Steps
- Extend the lab to cover GPO-enforced BitLocker for removable drives.
- Implement automatic backup of recovery keys to secure off-site storage.
- Simulate drive failure scenarios and validate recovery key usage.
## Steps

### 1. Create BitLocker Policy GPO

A new GPO named **BitLocker Policy** was created under Group Policy Objects.

<img src="images/01-Create-BitLocker-Policy-GPO.png" width="700"/>

---

### 2. Edit Group Policy Settings

Navigated to:
```
Computer Configuration > Administrative Templates > Windows Components > BitLocker Drive Encryption > Operating System Drives
```

Enabled:
- **Require additional authentication at startup**
- **Choose how BitLocker-protected operating system drives can be recovered**

<img src="images/02-Edit-BitLocker-Policy.png" width="700"/>

---

### 3. Allow TPM Startup Without PIN

Enabled the option to allow BitLocker to work with just TPM.

<img src="images/03-Allow-TPM-Only.png" width="700"/>

---

### 4. Save Recovery Key to AD DS

Configured recovery key storage in Active Directory Domain Services (AD DS).

<img src="images/04-Save-Recovery-Key-to-AD.png" width="700"/>

---

### 5. Link GPO to Domain

The policy was linked to the `homelab.local` domain using Group Policy Management Console (GPMC).

<img src="images/05-Link-GPO.png" width="700"/>

---

### 6. Force GPO Update on Client

Used the following command on the client machine:

```powershell
gpupdate /force
```

<img src="images/06-GPUpdate-Force.png" width="700"/>

---

### 7. Verify GPO Application (Resultant Set of Policy)

Confirmed that the BitLocker policy was applied using the `gpresult` tool.

<img src="images/07-GPResult.png" width="700"/>

---

### 8. Launch BitLocker

Accessed BitLocker Drive Encryption from Control Panel on the Windows 10 client.

<img src="images/08-BitLocker-Launch.png" width="700"/>

---

### 9. BitLocker Setup Wizard

Began the BitLocker setup wizard for the operating system drive.

<img src="images/09-Enable-BitLocker.png" width="700"/>

---

### 10. Select Recovery Method

Chose **Save to a file** as the recovery method to store the key on a network share.

<img src="images/10-Save-Recovery-Key-To-File.png" width="700"/>

---

### 11. Select Network Share

Navigated to the designated SMB path to store the recovery key.

<img src="images/11-Select Network Share for Recovery Key.png" width="700"/>

---

### 12. Confirm Saved Recovery Key File

Confirmed that the recovery key was successfully saved to the SMB share.

<img src="images/12-Recovery Key File Saved on Network.png" width="700"/>

---

### 13. Restart Prompt After Setup

After applying the GPO settings, the system prompted for a restart to begin encryption.

<img src="images/13-Restart Required After Bitlocker Setup.png" width="700"/>

---

### 14. BitLocker Status: Encryption Started

The BitLocker control panel displayed "Encryption in progress."

<img src="images/14-BitLocker Encryption Confirmed.png" width="700"/>

---

### 15. Pre-Boot Authentication Prompt (TPM)

The system showed a pre-boot authentication screen confirming TPM-based startup.

<img src="images/14-BitLocker Pre-Boot Authentication Prompt.png" width="700"/>

---

### 16. Recovery Key Stored in Active Directory

Confirmed the recovery key was stored under the computer object's ADUC properties.

<img src="images/15-Recovery Key Stored on Server.png" width="700"/>

---

### 17. Enable Event Logging (Optional)

BitLocker auditing and logging were enabled for security visibility.

<img src="images/16-Enable BitLocker Event Logging.png" width="700"/>

---

### 18. Verify Encryption via PowerShell

Used PowerShell to confirm encryption status:

```powershell
Get-BitLockerVolume
```

<img src="images/17-Verify Encryption with PowerShell.png" width="700"/>

---

### 19. Retrieve Key Protector ID (PowerShell)

Retrieved the protector ID via:

```powershell
(Get-BitLockerVolume -MountPoint "C:").KeyProtector
```

<img src="images/18-get-protector-id.png" width="700"/>

---

### 20. Confirm gpresult Summary

Verified GPO summary confirms enforcement of policy.

<img src="images/19-gpresult-summary-success.png" width="700"/>
<img src="images/20-gpresult-bitlocker-policy-applied.png" width="700"/>
<img src="images/21-gpresult-component-status-success.png" width="700"/>

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

