# Phase 15 - Active Directory Security Policies and Auditing



## Objective



Configure and verify security policies, Group Policy settings, auditing, and Windows authentication events within the Enterprise SOC Lab.



The purpose of this phase is to improve endpoint security and provide the logging required for Security Operations Center monitoring and detection engineering.



\---



## Environment



| Component | Configuration |

|---|---|

| Domain Controller | DC01 |

| Domain | enterprise.local |

| Active Directory | Enabled |

| Group Policy | Enabled |

| Security Auditing | Enabled |

| Network | Enterprise isolated lab network |



\---



## Domain Verification



The Active Directory domain and Domain Controller were verified successfully.



Evidence:



\- 01-domain-verification.png

\- 02-domain-controller-verification.png



\---



## Active Directory Users



Active Directory users were reviewed to verify that the required enterprise accounts were present.



Evidence:



\- 03-ad-users.png



\---



## Security Groups



Enterprise security groups were reviewed as part of the access-control and auditing configuration.



Evidence:



\- 04-security-groups.png

\- 10 security group audit.png



\---



## Password Policy



Password policy settings were configured and verified to improve account security.



Evidence:



\- 5 password policy.png



\---



## Account Lockout Policy



Account lockout controls were configured to help reduce password-guessing and brute-force attacks.



Evidence:



\- 6 account lockout policy.png



\---



## Advanced Audit Policy



Advanced Windows auditing was configured to provide security-relevant event visibility for the SOC.



Evidence:



\- 8 advanced audit policy.png

\- 8 gpo appled.png



\---



## Audit Policy Verification



The configured audit policies were reviewed and verified after Group Policy application.



Evidence:



\- 10 audit policy verification.png

\- 10 b audit policy verification.png



\---



## Windows Authentication Events



Windows Security Event IDs were verified as part of the authentication monitoring process.



### Event ID 4624



Event ID 4624 represents a successful logon.



Evidence:



\- 11 event 4624 successfull logon.png



### Event ID 4625



Event ID 4625 represents a failed logon attempt.



Evidence:



\- 12 event 4625 failed logo.png



These authentication events provide the foundation for the brute-force detection use case documented in Phase 10.



\---



## SOC Monitoring Relevance



The security policies and auditing configuration improve the visibility available to the SOC.



The collected authentication events can be used to:



\- Identify successful logons

\- Identify failed authentication attempts

\- Investigate repeated login failures

\- Detect potential password-guessing activity

\- Support incident investigation

\- Provide evidence for detection engineering



\---



## Security Controls Implemented



The following controls were configured or verified during this phase:



\- Password Policy

\- Account Lockout Policy

\- Advanced Audit Policy

\- Group Policy application

\- Security Group auditing

\- Windows authentication auditing



\---



## Verification



The configuration was validated using Windows administrative and security-management tools.



The screenshots provide evidence of:



\- Domain configuration

\- Domain Controller configuration

\- Active Directory users

\- Security groups

\- Password policy

\- Account lockout policy

\- Advanced auditing

\- Applied Group Policy

\- Audit policy verification

\- Successful logon events

\- Failed logon events



\---



## Result



The Active Directory security policies and auditing configuration were successfully implemented and verified.



The environment now provides the authentication and security-event visibility required for subsequent SOC monitoring and detection activities.



\---



## Status



Completed



Phase 15 - Active Directory Security Policies and Auditing is complete.


