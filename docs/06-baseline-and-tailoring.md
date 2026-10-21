# 6. Baseline and tailoring decisions

The system is categorized (C: High, I: High, A: High), so the High baseline of NIST SP 800-53 applies. The baseline is tailored for a 25-person clinic with a small IT office. Each decision below is deliberate, written down, and carries a residual risk that the clinic manager, acting as the authorizing official, accepts.

| Area | Decision type | What was decided | Reason | Residual risk |
|---|---|---|---|---|
| Physical security (PE family) | Hybrid: inherited and implemented | Google Cloud secures its data center, and the SSP cites Google Cloud’s compliance reports as the source. Northwind secures its own IT room and backup drives with a locked door, an access list, a sign-in log, and escorted visitors. | Northwind has no data center of its own, but it does have an IT room and physical backup drives. | Low. Depends on the provider’s controls, which are reviewed once a year. |
| Patient MFA (IA-2) | Tailored | Patients use a one-time code by text or email instead of hardware keys. Face verification is a possible later option. | Elderly patients mostly have basic phones, and hardware keys would block access to care. | Codes can be intercepted or an email account can be hacked. Reduced by lockout, suspicious-login alerts, and phone identity checks. Accepted by the clinic manager. |
| Round-the-clock monitoring (SI-4) | Tailored | No night shift and no outside monitoring service. Automated alerts go to an on-call rotation of IT staff, who respond within 25 minutes. The escalation order is on-call IT staff, then the ISSO, then the clinic manager. | A night shift and an outside service cost more than a 25-person clinic can pay. The ISSO must stay independent and cannot do daily operations. | An attack at night may be noticed late. Accepted by the clinic manager and listed on the POA&M with a note to revisit outside monitoring if the clinic grows. |

**Authorizing official:** the clinic manager. The ISSO recommends and documents risks, and the clinic manager decides which residual risks to accept and funds the fixes.

**On-call staffing:** the on-call rotation is shared by the IT admin and the IT assistant. If neither can respond in a real emergency, the ISSO acts as a backup responder only, and the clinic manager reviews every action the ISSO takes in that role, because the ISSO must not review their own actions.
