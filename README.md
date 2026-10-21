# Northwind Clinic: Security Authorization Package

**Project 1 of 5 in my cybersecurity portfolio path (ISSO, networking, endpoint security, SOC).**

I built a mini security authorization package for a fictional outpatient clinic’s cloud-hosted patient portal, following the NIST Risk Management Framework (RMF) and NIST SP 800-53 Rev 5. It covers system description, categorization, boundary, 20 control implementation statements, baseline tailoring, a risk assessment, and a POA&M.

> Northwind Clinic is fictional. The repo contains no real data, IP addresses, or credentials.

## The scenario

Northwind Clinic is an outpatient clinic with 25 staff, specializing in care for patients in their late 40s and older. Its patient portal (hosted on Google Cloud) lets patients view vitals, diagnoses, medications, and appointments, book appointments, message their doctor, and request an ambulance. Staff use it to open files, record vitals, diagnose, prescribe, record drug administration, and take payments.

Why it is a good ISSO case: the data is sensitive health information, the patients are elderly and a target for scams, and the ambulance feature makes availability a safety issue.

## Read the package in order

| # | Document | What it shows |
|---|---|---|
| 1 | [System description](docs/01-system-description.md) | Purpose, users, data, hosting decision |
| 2 | [Roles and access](docs/02-roles-and-access.md) | Least privilege and separation of duties |
| 3 | [Categorization (FIPS 199)](docs/03-categorization-fips199.md) | C/I/A ratings per data type and the overall rating |
| 4 | [Boundary and connections](docs/04-boundary-and-connections.md) | Authorization boundary diagram, inside vs. outside |
| 5 | [Control statements](docs/05-control-statements.md) | 20 implementation statements across 13 control families |
| 6 | [Baseline and tailoring](docs/06-baseline-and-tailoring.md) | Deliberate tailoring decisions with residual risk |
| 7 | [Risk assessment](docs/07-risk-assessment.md) | 10 risks, likelihood × impact |
| 8 | [POA&M](docs/08-poam.md) | 9 remediation items with owners and dates |
| | [Evidence notes](evidence/README.md) | How inherited controls are supported |

## Design decisions I can defend

- **System rating (C: High, I: High, A: High).** Driven by health data and the ambulance feature.
- **The IT admin cannot read medical records day to day.** Break-glass access is approved by the ISSO, lasts 3 hours, and is logged to write-once storage the admin cannot edit.
- **Any doctor can open any file** (continuity of care), compensated by full access logging and ISSO review.
- **The ambulance request works without a login.** A documented exception, with data minimization, an anti-bot check, rate alerts, and a phone fallback.
- **Patients use text or email codes for MFA** instead of hardware keys. A deliberate usability tradeoff with the risk recorded.
- **No 24/7 night shift.** An on-call rotation replaces it, and the leftover risk is accepted by the clinic manager as authorizing official.

## Skills demonstrated

NIST RMF lifecycle, FIPS 199 categorization, NIST SP 800-53 control selection and tailoring, writing implementation statements, shared responsibility analysis (cloud), risk assessment, POA&M management, access control design (RBAC, separation of duties, break-glass), audit logging, incident response planning, backup and recovery design.

## Standards referenced

NIST SP 800-37 (RMF), NIST SP 800-53 Rev 5 (controls), FIPS 199 (categorization), NIST SP 800-61 (incident handling), HIPAA breach notification concepts.

## How this was built

I developed this with an AI tutor that guided me with hints and questions. The design decisions, ratings, and numbers are mine, and I can explain each one.

## What comes next

| Project | Focus | Status |
|---|---|---|
| 1 | Security authorization package (this repo) | Complete |
| 2 | Segmented network and traffic analysis lab (firewall, secure admin access) | Planned |
| 3 | Endpoint hardening and vulnerability management | Planned |
| 4 | Detection lab and alert triage | Planned |
| 5 | Capstone: incident response and continuous monitoring | Planned |

Project 2 will make the network controls in this package (firewall rules, network zones, secure admin access) real and update the statements to match.
