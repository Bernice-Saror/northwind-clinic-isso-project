# 1. System description

**System:** Northwind Clinic Patient Portal
**Owner:** Clinic manager (authorizing official)
**Security officer:** ISSO
**Version:** 1.0

## Overview

Northwind Clinic is an outpatient clinic of 25 staff that specializes in care for patients in their late 40s and older. The patient portal is a cloud-hosted web application.

## Users and functions

- **Patients** view their vitals, diagnosis, medications, and appointments, book and reschedule appointments, message their doctor, and request an ambulance.
- **Staff** open patient files, record vitals, diagnose, prescribe, record administered drugs, and take payments.

## Data

The portal holds health data, identity and contact details, login credentials, doctor-patient messages, ambulance pickup location, and payment confirmation only. Card numbers are not stored; payments are handled by a third-party processor.

## Clinical workflow

Front desk opens the file and takes payment, the nurse records vitals and forwards them, the doctor diagnoses and prescribes, and the nurse administers the prescribed drugs.

## Hosting decision

Hosting is on Google Cloud, under the shared responsibility model. A small clinic cannot realistically run and defend its own server room. The provider secures the physical infrastructure. Northwind secures the application, accounts, settings, backups, logging, and staff devices. Remaining cloud risks (misconfiguration, account compromise, provider dependency, compliance and data location) are carried into the [risk assessment](07-risk-assessment.md).
