# Evidence notes: inherited controls

Northwind inherits the physical and environmental controls for the portal’s hosting from Google Cloud. This page explains how that inheritance is supported.

## Where the evidence comes from

Google Cloud publishes audit reports and certificates through its **Compliance Reports Manager** (https://cloud.google.com/security/compliance/compliance-reports-manager). It offers on-demand access to ISO/IEC certificates, SOC reports, and self-assessments at no additional cost. Some resources require signing in with a Google Cloud or Google Workspace account.

Google Cloud issues SOC 2 Type II reports, and the core reports are issued quarterly with bridge letters covering the gaps between reports.

## Documents to cite

| Evidence | Supports |
|---|---|
| SOC 2 Type II report | Physical security, availability, and operations controls of the data centers |
| ISO/IEC 27001 certificate | The provider’s information security management system |
| HIPAA documentation and business associate agreement (check the provider’s current process) | Handling of health data |

## How this package uses them

For each inherited control, the control statement or tailoring decision names the provider and the report. The date and version of each report is recorded here when it is downloaded.

| Report | Version or period | Date downloaded | Controls supported |
|---|---|---|---|
| (add after download) | | | PE family |

## Customer responsibilities

SOC 2 reports list the controls that customers are expected to implement themselves (often called complementary user entity controls). Each of those is mapped to a Northwind control statement in [section 5](../docs/05-control-statements.md).

## Important: do not upload the reports

Some Google Cloud documents are marked confidential. This repository records the report name, date, and link only. The files themselves are not stored here.
