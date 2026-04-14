# IT Support Capstone – Ticket Resolution Lab

**Author:** Austin Thai

**Program:** Per Scholas

**Date:** April 2026

---

## Overview

This project simulates a real-world IT help desk environment in a Windows-based virtual machine. Support tickets were assigned and resolved, covering common technical issues related to user account management, network connectivity, file system permissions, and hardware/driver functionality.

The goal of this lab was to apply structured troubleshooting methods, identify root causes, and document resolutions in a format aligned with IT support workflows.

---

## Skills Demonstrated

- Windows 10 troubleshooting
- Local user account and password management (`lusrmgr.msc`)
- Network diagnostics and service management (DHCP, `ipconfig`, `services.msc`)
- File system permissions and access control
- Device Manager and driver troubleshooting
- Ticket documentation and root cause analysis

---

## Environment

- **OS:** Windows 10 (Virtual Machine)
- **Platform:** Oracle VirtualBox
- **Network:** NAT / Virtualized environment

---

## Ticket Resolutions

---

### Ticket 1004 – Windows Login Issue (Locked Out Account)

**Issue:** User changed their password and was subsequently locked out of Windows, unable to log in.

**Diagnosis:**

| Step | Action Taken | Purpose | Result |
|------|-------------|---------|--------|
| 1 | Opened `lusrmgr.msc` to review local user accounts | Verify account status and password settings | Found "Password never expires" was enabled on Learner01's account |
| 2 | Unchecked "Password never expires" and set a temporary password with "User must change password at next logon" enabled | Restore login access and enforce password reset | Temporary password successfully applied |
| 3 | Logged in as Learner01 using temporary credentials | Confirm password reset and validate access | User was prompted to create a new password and successfully logged in |

**Root Cause:** The "Password never expires" setting was conflicting with the password change attempt, causing the account lockout.

**Resolution:** Disabled "Password never expires" via `lusrmgr.msc`, set a temporary password, and enabled forced password reset on next logon.

**Result:** User successfully logged in and regained full desktop access.

<img width="975" height="604" alt="Image" src="https://github.com/user-attachments/assets/baefeeca-25d0-49f2-8a2b-881a001b8da5" />

<img width="975" height="608" alt="Image" src="https://github.com/user-attachments/assets/1965a38b-d480-49db-86d3-abad636b0ee7" />

<img width="975" height="731" alt="Image" src="https://github.com/user-attachments/assets/bb2d6f3c-8acf-43ca-9391-80302c083aeb" />

<img width="975" height="738" alt="Image" src="https://github.com/user-attachments/assets/7ae28cd4-be4d-47ec-a718-3edc5aa74cbd" />

---

### Ticket 1005 – Application Connectivity Issue (Skype)

**Issue:** Skype unable to connect to meetings; user received "Unable to sign in, please check your internet connection."

**Diagnosis:**

| Step | Action Taken | Purpose | Result |
|------|-------------|---------|--------|
| 1 | Checked `services.msc` for required network services | Ensure all necessary services were running | Found DHCP Client service was disabled |
| 2 | Enabled the DHCP Client service | Allow the system to receive a proper IP address | IP address successfully assigned |
| 3 | Ran `ipconfig /flushdns` and `ipconfig /all` | Clear DNS cache and verify connectivity | Network connectivity restored; confirmed active IP |

**Root Cause:** The DHCP Client service was disabled, preventing the system from obtaining an IP address and breaking application network access.

**Resolution:** Enabled DHCP Client via `services.msc` and verified IP assignment with `ipconfig /all`.

**Result:** Skype successfully connected; application functioning normally.

<img width="975" height="525" alt="Image" src="https://github.com/user-attachments/assets/5ecfea98-4bd6-42e5-adeb-4a15721586db" />

---

### Ticket 1006 – Access Denied (Drive F: Permissions)

**Issue:** User unable to access the F: drive to save files; received "Access Denied" error.

**Diagnosis:**

| Step | Action Taken | Purpose | Result |
|------|-------------|---------|--------|
| 1 | Attempted to access F: drive as Learner01 | Confirm the issue exists and identify the error | "Access Denied" error confirmed |
| 2 | Logged into admin account and reviewed drive F: properties/permissions | Determine if user had any assigned permissions | Found Learner01 had no permissions on the drive |
| 3 | Added Learner01 to the F: drive access control list with appropriate permissions | Grant necessary access to resolve the ticket | User now appeared in permissions list |

**Root Cause:** Learner01 was not assigned any file system permissions for the F: drive.

**Resolution:** Navigated to F: drive properties under the admin account, added Learner01 to the ACL with the appropriate permissions.

**Result:** User successfully accessed the F: drive and was able to save files.

<img width="975" height="554" alt="Image" src="https://github.com/user-attachments/assets/a461e795-8896-4358-8130-30eac0271bae" />

<img width="975" height="567" alt="Image" src="https://github.com/user-attachments/assets/e43f356e-6057-4129-91b1-488287c8cdba" />

Fix:

<img width="975" height="717" alt="Image" src="https://github.com/user-attachments/assets/9b6bc972-8193-422b-a58f-83db73bb10f9" />

<img width="855" height="526" alt="Image" src="https://github.com/user-attachments/assets/618c9c31-e545-4732-bb8a-061147b12387" />

To note, the image shows giving full control, but best practice would be following the principle of least privilege.

---

### Ticket 1007 – No Audio (Disabled Audio Driver)

**Issue:** User had no sound on their device; a red X appeared on the speaker icon in the taskbar despite speakers being physically connected.

**Diagnosis:**

| Step | Action Taken | Purpose | Result |
|------|-------------|---------|--------|
| 1 | Verified the sound issue by attempting playback | Confirm the problem exists on the device | Audio confirmed non-functional |
| 2 | Checked for connected peripheral audio devices | Rule out external device conflicts (headphones, etc.) | No peripherals were connected or causing conflict |
| 3 | Opened Device Manager and inspected the audio driver | Identify if the issue was driver-related | Found High Definition Audio Device was disabled |

**Root Cause:** The High Definition Audio Device driver was disabled in Device Manager.

**Resolution:** Opened Device Manager, located the disabled audio driver, and re-enabled the device.

**Result:** Audio restored; user confirmed sound working correctly on YouTube playback.

<img width="1066" height="629" alt="Image" src="https://github.com/user-attachments/assets/34972f3b-36c7-4f61-8712-4f06fc2fcddc" />

---

## Key Takeaways

- Structured, step-by-step troubleshooting isolates root causes efficiently and avoids unnecessary fixes
- Many user-facing problems trace back to underlying service, permission, or driver misconfigurations rather than hardware failure
- Clear documentation — including what was checked and why — improves resolution speed and builds a reference for recurring issues
- Understanding both the user account layer and the system/service layer is essential for effective IT support
