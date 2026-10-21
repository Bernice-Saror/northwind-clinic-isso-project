# 2. Roles and access

| Role | Can read | Can write or edit | Cannot access |
|---|---|---|---|
| Patient | Own vitals, diagnosis, medications, appointments, messages | Appointments, messages, ambulance request | Other patients’ records, staff data, system settings |
| Front desk | File exists, billing amount | Create file, record payments | Diagnosis, vitals, prescriptions, messages |
| Nurse | Vitals, doctor’s diagnosis and prescription | Vitals, record that a drug was given | Editing doctor’s notes, payment information |
| Doctor | Vitals, any patient file, patient messages | Diagnosis, prescription, message replies | Payment information |
| IT admin | System logs and system health; medical records only through break-glass | System settings, accounts | Payment information, routine access to medical content |

## Design decisions

- **Integrity of the clinical record.** Nurses cannot edit a doctor’s notes, so a diagnosis cannot be silently changed.
- **Need to know.** The front desk sees a billing amount but no clinical data. Billing data is kept separate from clinical data.
- **Continuity of care.** Any doctor may open any patient file, because elderly patients are seen by different doctors. Every file access is logged, and the ISSO reviews logs for access with no treatment relationship.
- **Separation of duties.** The IT admin has no routine access to medical record content. Emergency access is through break-glass (see [control statements](05-control-statements.md)). The ISSO, not the IT admin, reviews admin activity.
