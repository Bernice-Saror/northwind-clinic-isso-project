# 3. Categorization (FIPS 199)

| Data type | Confidentiality | Integrity | Availability |
|---|---|---|---|
| Health data | High | High | High |
| Identity and contact | High | Moderate | Moderate |
| Credentials | High | High | Moderate |
| Messages | High | High | Low |
| Ambulance location | Moderate | High | High |
| Payment confirmation | Low | Moderate | Moderate |

## Rationale for key ratings

| Rating | Reason |
|---|---|
| Health data, all High | Exposure harms patients, a silently altered dose or blood group could injure them, and care depends on access to it. |
| Identity and contact, C High | The data identifies elderly patients of a health clinic and could enable fraud and scams. |
| Credentials, C and I High | A stolen password gives access to a patient’s record, and an admin password exposes everything. |
| Credentials, A Moderate | If login is down patients cannot reach their records, but the ambulance request works without a login. |
| Messages, C and I High | Patients describe symptoms in messages, so they are effectively health data, and a changed message could change medical advice. |
| Ambulance location, C Moderate | Sensitive in the moment but short-lived. |
| Ambulance location, I and A High | A wrong address sends help to the wrong place, and the feature must work when needed. |
| Payment confirmation, C Low | Only paid or unpaid is stored, with no card data, so exposure gives an attacker little. |

## Overall system categorization

Using the high-water mark of each column:

**(Confidentiality: High, Integrity: High, Availability: High)**

- Confidentiality is High because of health data, identity, credentials, and messages.
- Integrity is High because altered health data, messages, or ambulance addresses could harm patients.
- Availability is High because patients must reach care and the ambulance feature when needed.

The High baseline of NIST SP 800-53 applies, tailored in [section 6](06-baseline-and-tailoring.md).
