# Part 3 – BitLocker Group Policy Enforcement and Verification

This phase focuses on applying and verifying domain-level BitLocker encryption policies using Group Policy Objects (GPOs) and Active Directory integration. Each step below includes a description and a reference image captured during implementation.

---

## Procedures and Results

### 1. Create BitLocker Policy GPO
- Opened **Group Policy Management Console**.
- Created a new GPO named `BitLocker Policy`.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/01-create-bitlocker-policy-gpo.png" width="700"/>

---

### 2. Attach TPM Module to VM
- Enabled **TPM 2.0** for the Windows 10 VM inside Proxmox settings.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/02-add-tpm2-to-vm.png" width="700"/>

---

### 3. Require Startup Authentication
- Enabled GPO: `Require additional authentication at startup`.
- Configured to allow **TPM only**.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/03-require-authentication-at-startup.png" width="700"/>

---

### 4. Enable AD DS Recovery Key Backup
- Enabled GPO: `Save BitLocker recovery information to AD DS for OS drives`.
- Ensures keys are saved to **Active Directory**.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/04-enable-recovery-info-in-ad.png" width="700"/>

---

### 5. Link GPO to Domain
- Linked `BitLocker Policy` GPO to domain `homelab.local`.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/05-link-bitlocker-gpo-to-domain.png" width="700"/>

---

### 6. Rename Hostname and Restart
- Renamed Windows 10 client hostname and rebooted for AD consistency.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/06-rename-hostname.png" width="700"/>

---

### 7. Join Client to Domain
- Joined client to `homelab.local` domain using domain credentials.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/07-domain-join.png" width="700"/>

---

### 8. Force GPO Update and Check Results
- Ran `gpupdate /force` from CLI and verified:
  - BitLocker policy presence
  - Security group membership
  - Component policy delivery status

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/08a-gpupdate-success.png" width="700"/>
<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/08b-gpresult-bitlocker-policy.png" width="700"/>
<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/08c-gpresult-user-groups.png" width="700"/>

---

### 9. Launch BitLocker Setup
- Attempted to launch BitLocker via Control Panel.
- Encountered TPM error due to delayed domain sync on first boot.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/09-enable-bitlocker.png" width="700"/>

---

### 10. Allow BitLocker Without TPM (Test Scenario)
- Enabled fallback GPO: `Allow BitLocker without compatible TPM`.
- This allows test encryption in virtualized environments.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/10-allow-bitlocker-without-tpm.png" width="700"/>

---

### 11. Map Network Drive for Recovery Key Storage
- Mapped a shared network folder as `Z:\` to store exported recovery key manually.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/11-mapped-network-drive.png" width="700"/>

---

### 12. Save Recovery Key to Network Location
- Selected option to back up key to file.
- Saved recovery key to mapped drive `Z:\`.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/12-save-bitlocker-recovery-key.png" width="700"/>

---

### 13. Proceed with BitLocker Encryption
- Rebooted to initiate encryption process.
- TPM now recognized post-reboot.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/13-Restart Required After BitLocker Setup.png" width="700"/>

---

### 14. BitLocker Encryption Confirmed
- Confirmed encryption in progress and recovery options applied.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/14-BitLocker Encryption Confirmed.png" width="700"/>

---

### 15. BitLocker Pre-Boot Prompt Active
- Verified TPM prompt at pre-boot.
- Confirms policy enforcement at hardware level.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/14-BitLocker Pre-Boot Authentication Prompt.png" width="700"/>

---

### 16. Recovery Key Stored in AD
- Verified presence of recovery key inside Active Directory (using `Active Directory Users and Computers`).

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/15-Recovery Key Stored on Server.png" width="700"/>

---

### 17. Enable BitLocker Event Logging
- Enabled auditing to track BitLocker-related events.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/16-enable-bitlocker-event-logging.png" width="700"/>

---

### 18. Verify BitLocker Policy Status via PowerShell
- Confirmed protector type, encryption status, and key protector ID.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/17-bitlocker-policy-verification.png" width="700"/>
<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/18-get-protector-id.png" width="700"/>

---

### 19. Final GPO Result Summary
- Verified GPO policy application via `gpresult /h report.html`.
- Confirmed `BitLocker Policy` and all subcomponents were applied.

<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/19-gpresult-summary-success.png" width="700"/>
<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/20-gpresult-bitlocker-policy-applied.png" width="700"/>
<img src="/Tariq-homelab/winserver-ad-bitlocker/raw/main/images/21-gpresult-component-status-success.png" width="700"/>

---

## Next Steps (Part 4)

The next phase will involve:

- Creating **Active Directory Organizational Units (OUs)**.
- Structuring departments and user groups (e.g., IT, HR, Finance).
- Creating sample user accounts manually and via **PowerShell scripting**.
- Testing **GPO filtering**, delegation, and user login scenarios.

This will complete the core AD lab and simulate real-world sysadmin tasks.

