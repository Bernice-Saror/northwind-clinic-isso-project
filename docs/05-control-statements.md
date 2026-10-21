# 5. Control implementation statements

Twenty statements across 13 NIST SP 800-53 control families (AC, AU, IA, CP, IR, SC, PS, CM, SI, RA, AT, CA/SA, MP). Each statement says who does what, how, and where, and how it is checked.

| # | Controls | Title |
|---|---|---|
| 1 | AC-6 | Least privilege: front desk role |
| 2 | AC-6, AU-6 | IT admin break-glass access |
| 3 | IA-2, IA-5, AC-7 | Authentication and MFA |
| 4 | AC-14, CP-2 | Ambulance request without login |
| 5 | AU-2, AU-3, AU-6, AU-9, AU-11 | Audit logging |
| 6 | IR-4, IR-5, IR-6, IR-8 | Incident response |
| 7 | CP-9, CP-10, CP-4 | Backup and recovery |
| 8 | SC-8, SC-28, SC-7 | Encryption and network protection |
| 9 | AC-2 | Account management |
| 10 | PS-4 | Personnel termination |
| 11 | CM-2, CM-6 | Baseline configuration and hardening |
| 12 | CM-3 | Change control |
| 13 | SI-2 | Patching |
| 14 | RA-5 | Vulnerability scanning |
| 15 | SI-3 | Malware protection |
| 16 | SI-4 | System monitoring |
| 17 | AT-2 | Security awareness training |
| 18 | CA-3, SA-9 | Outside connections and external services |
| 19 | MP-5, MP-6 | Media protection and disposal |
| 20 | RA-3 | Risk assessment |

---

## 1. AC-6 Least privilege: front desk role

Front desk staff are assigned the Front Desk role, which can search for a patient by name, create new patient files, and record payments. Front desk users cannot view vitals, diagnoses, prescriptions, or doctor-patient messages. The IT admin assigns roles to individual user accounts when staff are hired or change jobs. The ISSO reviews all role assignments every quarter, using an account list supplied by the IT admin, and investigates any front desk account that has accessed clinical data.

## 2. AC-6 Least privilege and AU-6 Audit review: IT admin break-glass access

The IT admin uses an administrator account for daily work (monitoring portal uptime and connectivity, applying patches, managing accounts, and checking logs). This account cannot view medical record content. When a failure or suspected breach cannot be resolved without viewing record content, the IT admin requests emergency access from the ISSO, or from the clinic manager if the ISSO is unavailable. Approved access is a temporary elevated account that expires after 3 hours and can be extended once with ISSO re-approval. All admin activity, including every break-glass session and every approval, is written to a log store the IT admin cannot edit or delete. The system alerts on suspicious activity, such as 10 failed logins in one minute. The ISSO reviews every break-glass session at the end of each workday, and reviews general admin logs monthly, because the IT admin must not review their own activity.

**Examples of emergencies that justify break-glass:**

1. The patient database fails or will not start, and it cannot be repaired without viewing record content.
2. A suspected breach in which patient information may have been stolen and used for extortion or scams, requiring investigation of what was accessed.

## 3. IA-2, IA-5, AC-7 Authentication and MFA

All portal users (doctors, nurses, front desk staff, the IT admin, and patients) must use multi-factor authentication. Staff and the IT admin use an authenticator app. Patients receive a one-time code by text message or email, so that patients with basic phones can still log in. This lower-strength method is an accepted usability tradeoff for elderly patients and is recorded as a residual risk. After 5 failed logins, the account is locked for 5 minutes. After 3 lockouts within one hour, the account is suspended and an alert is sent to the IT admin. The IT admin restores a suspended patient account only after verifying the patient’s identity by phone. Suspended staff accounts are restored only with ISSO approval. All failed logins and lockouts are logged and reviewed by the ISSO.

## 4. AC-14, CP-2 Ambulance request without authentication (documented IA-2 exception)

The ambulance request function is available without a login so that no patient is blocked in an emergency by a forgotten password. This is a documented exception to the MFA requirement. The form collects only the caller’s name, location, callback number, and a short note on the emergency, and shows no patient information to the caller. A simple anti-bot check protects the form from automated abuse. If the check fails or confuses the caller, the screen immediately offers the clinic’s emergency phone number. If the portal is unavailable, patients can request an ambulance by calling that number. The front desk answers during clinic hours. If a call is not answered within 20 seconds, or the clinic is closed, it is forwarded automatically to the ambulance service, and the clinic manager is notified. Every request is logged with time, location, and callback number. The system alerts the IT admin and ISSO when one phone number makes 3 or more requests within one hour, and the ISSO reviews all ambulance request logs every 2 days.

## 5. AU-2, AU-3, AU-6, AU-9, AU-11 Audit logging

The portal records clinical actions (file opens, vitals, diagnoses, prescriptions, and drug administration, including which nurse gave each drug), security events (logins, failed logins, lockouts, suspensions, role changes, break-glass sessions, ambulance requests), and every change to clinical data with its old and new value. Each entry records who, what, when, from where, and the result, and never the contents of a patient record. Logs are copied immediately to separate write-once storage, so an attacker who takes over the portal server cannot delete them. The IT admin and the ISSO can read logs, and nobody can edit or delete them during the retention period. The clinic manager does not read raw logs and receives summary reports from the ISSO. An outside auditor may be given temporary read-only access, approved by the ISSO, for example after an attack or for a periodic review. Every read of the logs is itself logged. Logs are retained for 7 years, and disposal after that period requires ISSO approval and is itself recorded. The ISSO reviews logs as described in the break-glass, login, and ambulance statements.

## 6. IR-4, IR-5, IR-6, IR-8 Incident response

Any staff member who suspects an attack (for example a phishing email, repeated failed logins, or unusual access) reports it to the IT admin, and alerts from the logging system go to the IT admin and the ISSO. The IT admin may immediately contain a single affected account or device (disable the account, disconnect the laptop from the network) and must tell the ISSO within 15 minutes. A reported phishing email is quarantined and removed from all mailboxes, and the device and account that received it are checked. The ISSO assesses the incident and informs the clinic manager, who decides on larger actions such as taking the portal offline. Containment preserves evidence: affected devices are isolated, not wiped, until the ISSO confirms the evidence has been captured. If the portal is taken offline, patients reach help through the emergency phone number described in the ambulance statement, and the ambulance service is informed. If patient data may have been exposed, the clinic manager and the ISSO notify the affected patients without unreasonable delay and notify the required regulators, following the applicable breach notification law. Every incident is documented with a timeline taken from the logs, the actions taken, and lessons learned, and the ISSO adds any control failures to the POA&M. The incident response plan is tested at least once a year with a tabletop exercise.

## 7. CP-9, CP-10, CP-4 Backup and recovery

The IT admin takes a full backup of the portal database and its configuration every day and keeps 3 months of backups. One copy is stored in a separate cloud storage account, and one copy is kept on encrypted physical drives held in a locked location away from the clinic. Backups are encrypted, and the portal’s administrator account cannot delete them, so an attacker who takes over the portal cannot destroy the backups. Backups exist for recovery, not as the long-term record: patient records stay in the live system. The IT admin tests a restore of a sample every month and a full restore once a year, records the result, and the ISSO reviews the results.

## 8. SC-8, SC-28, SC-7 Encryption and network protection

All data traveling between patient devices, staff laptops, and the portal is encrypted in transit with TLS, and the portal accepts no unencrypted connections. Patient data stored in the database, backups, and logs is encrypted at rest. Encryption keys are held in the cloud provider’s key management service, separate from the data, and only the IT admin’s protected administrator account can manage them. The portal sits behind a firewall that allows only the traffic it needs, and staff and admin access uses MFA. The detailed firewall rules and network zones will be added after the network lab (Project 2).

## 9. AC-2 Account management

The IT admin creates, changes, or disables an account only on a written request from the clinic manager. Each account belongs to one named person, and shared accounts are not allowed. The ISSO reviews all accounts and their roles every quarter, using a list supplied by the IT admin, and removes any account that is no longer needed.

## 10. PS-4 Personnel termination

When a staff member leaves or is dismissed, the clinic manager notifies the IT admin, who disables that person’s account the same day. Accounts held by the IT admin or any administrator are disabled by the ISSO within 1 hour of departure. Clinic laptops, keys, and drives are collected, and the ISSO confirms in writing that the account was disabled.

## 11. CM-2, CM-6 Baseline configuration and hardening

Every staff laptop and server is configured to the CIS Benchmark settings for its operating system. The IT admin records the approved configuration, checks each device against it every month, and documents any setting that cannot be applied. The ISSO accepts or rejects each documented exception.

## 12. CM-3 Change control

The IT admin proposes any change to the live portal, tests it first in a separate test copy, and applies it only after the ISSO approves it. Each change is recorded with what changed, who approved it, and how to undo it.

## 13. SI-2 Flaw remediation (patching)

The IT admin installs critical security patches within 7 days, high-severity patches within 14 days, and all other patches within 30 days. The IT admin keeps a list of pending patches, and the ISSO reviews it every month. A patch that cannot be applied on time is recorded on the POA&M with a reason and a new date.

## 14. RA-5 Vulnerability scanning

The IT admin scans the portal and all staff laptops for vulnerabilities every month. The ISSO reviews the results, ranks findings by severity and exposure, and adds unresolved findings to the POA&M with an owner and a due date.

## 15. SI-3 Malware protection

Antimalware software is installed on every staff laptop and updates itself automatically. The software reports to the IT admin, who investigates any detection and reports serious ones to the ISSO under the incident response statement.

## 16. SI-4 System monitoring

The logging system raises alerts for spikes in failed logins, break-glass use, unusual access to patient files, and repeated ambulance requests from one number. Alerts go to the IT admin and the ISSO, and the ISSO confirms each month that the alert rules are still working.

## 17. AT-2 Security awareness training

Every staff member completes security training when hired and once a year after that. The ISSO sends a practice phishing email to staff every quarter and records who reported it, who clicked it, and who needs further training.

## 18. CA-3, SA-9 Outside connections and external services

Each outside service (the lab, ambulance dispatch, the email service, and the payment processor) has a written agreement that states what data is shared, in which direction, and who is responsible for its security. The ISSO reviews each agreement once a year and when the service changes.

## 19. MP-5, MP-6 Media protection and disposal

Staff laptop disks and backup drives are encrypted. Backup drives are logged whenever they are moved, and the person carrying them signs for them. Any laptop or drive is securely wiped before it is reused, sold, or thrown away, and the IT admin records each disposal.

## 20. RA-3 Risk assessment

The ISSO reviews the risk assessment once a year and after any major incident or change to the system. The results update the POA&M and the System Security Plan, and the ISSO reports the key risks to the clinic manager.
