# 7. Risk assessment

Ten risks remain after the controls in [section 5](05-control-statements.md). Each is rated on likelihood and impact (Low = 1, Moderate = 2, High = 3). The two numbers are multiplied: 6 to 9 is High, 3 to 4 is Moderate, and 1 to 2 is Low.

| ID | Threat | Weakness | Consequence | Likelihood | Impact | Level | Existing controls | Response |
|---|---|---|---|---|---|---|---|---|
| R1 | A scammer posing as the clinic tricks an elderly patient into giving a login or MFA code | Elderly patients are common scam targets, and codes can be handed over | Patient account takeover, exposed health data, fraud against the patient | High | High | High | MFA, lockout, login alerts | Reduce: scam warnings in every message and patient education (POA&M 1) |
| R2 | The ambulance connection fails (dispatch outage, portal outage, or attack) | Dispatch is an outside service, and the portal cannot always confirm receipt | Delayed help and possible harm to a patient | Low | High | Moderate | Phone fallback, forwarding to the ambulance service, request logging | Reduce: regular failover tests (POA&M 4) |
| R3 | A doctor opens a patient file with no treatment reason | Any doctor can open any file by design | Privacy violation, loss of trust, legal trouble | Moderate | High | High | Access logging, ISSO log review | Reduce: monthly report of file opens with no matching appointment (POA&M 3) |
| R4 | An attacker intercepts a patient’s code or takes over the patient’s email | Text and email codes are weaker than an authenticator app (accepted tailoring decision) | Patient account takeover | Moderate | High | High | Lockout, suspicious-login alerts, phone identity check | Reduce and partly accept: offer a stronger option to willing patients (POA&M 2) |
| R5 | Ransomware or extortion attack on the portal or staff laptops | Phishing can reach staff, and stolen data can be used for blackmail even when backups work | Outage, stolen patient data, blackmail | Moderate | High | High | MFA, backups, malware protection, incident response | Reduce: restore test and tabletop exercise (POA&M 5) |
| R6 | Ransomware destroys the backups | Backups are stored online | Records cannot be recovered | Low | High | Moderate | Two separate copies, off-site encrypted drives, portal admin cannot delete backups, monthly restore test | Accept, monitored through restore tests |
| R7 | The lab sends a wrong or tampered result | Results arrive from an outside system Northwind does not control | Wrong diagnosis or dose | Low | High | Moderate | Written agreement with the lab, change logging | Reduce: clinician verifies a result before release (POA&M 6) |
| R8 | An attack at night is noticed late | The clinic is closed and there is no 24/7 monitoring | Longer attacker access and more data exposed | Moderate | Moderate | Moderate | Automated alerts, on-call rotation, escalation order | Accept (clinic manager) and test after-hours escalation (POA&M 7) |
| R9 | Phishing steals a staff member’s password | Staff training is annual, with quarterly practice emails | Unauthorized access to clinical data | High | High | High | MFA, training, email quarantine | Reduce: start quarterly practice phishing (POA&M 8) |
| R10 | Cloud settings are misconfigured and expose data | Misconfiguration is the top cloud risk, and a small IT office manages the settings | Public exposure of patient data | Moderate | High | High | Change control, monthly scans, hardened baseline | Reduce: ISSO review of cloud settings (POA&M 9) |

## Summary

| Level | Count | Risks |
|---|---|---|
| High | 6 | R1, R3, R4, R5, R9, R10 |
| Moderate | 4 | R2, R6, R7, R8 |
| Low | 0 | |
