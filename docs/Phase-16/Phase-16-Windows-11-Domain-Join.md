# Phase 16 - Windows 11 Domain Join

## Objective

Join the Windows 11 endpoint to the Enterprise SOC Lab Active Directory domain and verify that the endpoint can communicate with and authenticate against the Domain Controller.

The purpose of this phase is to introduce a domain-joined Windows endpoint into the enterprise environment so that centralized authentication, Group Policy, security auditing, and SOC monitoring can be applied.

---

## Environment

| Component | Configuration |
|---|---|
| Domain Controller | DC01 |
| Domain | enterprise.local |
| Client | WIN11-CLIENT01 |
| Operating System | Windows 11 |
| Active Directory | Enabled |
| DNS | DC01 |
| Network | Enterprise isolated lab network |

---

## Network Configuration

The Windows 11 client was configured to communicate with the Domain Controller over the Enterprise SOC Lab network.

The client uses the Domain Controller as its DNS server because Active Directory relies on DNS for domain discovery and authentication services.

The following connectivity checks were performed before attempting the domain join:

- IP connectivity to DC01
- DNS resolution of `enterprise.local`
- DNS resolution of `DC01`
- Domain Controller discovery
- LDAP connectivity

---

## Domain Join

The Windows 11 endpoint was joined to the following Active Directory domain:

`enterprise.local`

The domain join process required valid domain credentials with permission to join computers to the domain.

After entering the domain credentials, Windows successfully contacted the Domain Controller and completed the domain join process.

The endpoint was then restarted to complete the domain membership configuration.

---

## Domain Membership Verification

After restarting the Windows 11 endpoint, the computer's domain membership was verified.

The endpoint was confirmed as:

- Computer Name: `WIN11-CLIENT01`
- Domain: `enterprise.local`
- Domain Controller: `DC01`

The client was also verified from the Domain Controller using Active Directory Users and Computers.

The computer account for `WIN11-CLIENT01` was visible within Active Directory, confirming that the endpoint had successfully registered with the domain.

---

## Authentication Verification

Domain authentication was tested after the endpoint joined the domain.

The Windows 11 client was able to authenticate using an Active Directory account.

This confirmed communication between:

`WIN11-CLIENT01 -> DC01 -> Active Directory`

The authentication process demonstrated that the endpoint was successfully integrated into the enterprise identity infrastructure.

---

## Secure Channel Verification

The secure relationship between the Windows 11 client and the Active Directory domain was verified.

A healthy secure channel confirms that the client can securely communicate with the Domain Controller for domain authentication and other Active Directory operations.

---

## Active Directory Integration

The Windows 11 endpoint is now part of the Enterprise SOC Lab Active Directory environment.

This allows the endpoint to participate in centralized:

- Authentication
- Group Policy
- Security configuration
- User management
- Computer management
- Security auditing
- Event logging
- SOC monitoring

---

## Security and SOC Relevance

Domain-joining the endpoint is an important step in building the Enterprise SOC Lab because Windows endpoints generate security telemetry that can be monitored by the SOC.

The domain environment provides a realistic enterprise authentication model where security events can be investigated centrally.

Examples of events that can later be monitored include:

- Successful logons
- Failed logons
- Account lockouts
- Privilege use
- Group membership changes
- Process execution
- PowerShell activity
- Policy changes
- Endpoint security events

These events can support detection engineering and incident investigation.

---

## Validation

The following validation checks were completed:

| Validation | Result |
|---|---|
| Client can reach DC01 | Verified |
| DNS resolution | Verified |
| Domain Controller discovery | Verified |
| LDAP connectivity | Verified |
| Domain join | Successful |
| Client restart | Completed |
| Computer account in AD | Verified |
| Domain authentication | Verified |
| Secure channel | Verified |

---

## Result

`WIN11-CLIENT01` was successfully integrated into the `enterprise.local` Active Directory domain.

The Windows 11 endpoint is now ready to receive centralized security policies and generate authentication and endpoint telemetry for the Enterprise SOC Lab.

This establishes the endpoint layer required for subsequent security monitoring, detection engineering, and incident response activities.

---

## Evidence

The following screenshots document the Windows 11 domain-join process and validation performed during this phase.

### Network and Connectivity

#### Windows 11 Network Adapters

![Windows 11 Network Adapters](../../screenshots/Phase-16/2%20win11%20network%20adapters.png)

#### Windows 11 Dual Network Adapter Configuration

![Windows 11 Dual Network Adapter Configuration](../../screenshots/Phase-16/3%20win11%20dual%20network%20adapter.png)

#### DC01 Network Configuration

![DC01 Network Configuration](../../screenshots/Phase-16/4%20dc01-dual-network-config.png)

#### Windows 11 to DC01 Connectivity

![Windows 11 to DC01 Connectivity](../../screenshots/Phase-16/5%20win11-dc01-connectivity.png)

### DNS and Domain Controller Discovery

#### Windows 11 Network Configuration

![Windows 11 Network Configuration](../../screenshots/Phase-16/14-WIN11-Network-Configuration.png)

#### DNS Configuration

![Windows 11 DNS Configuration](../../screenshots/Phase-16/15-WIN11-DNS-Configuration.png)

#### Ping DC01

![Ping DC01 Success](../../screenshots/Phase-16/16-WIN11-Ping-DC01-Success.png)

#### LDAP Port 389 Connectivity

![LDAP 389 Connectivity](../../screenshots/Phase-16/17-WIN11-LDAP-389-Success.png)

#### Enterprise Domain DNS Resolution

![Enterprise Domain DNS Resolution](../../screenshots/Phase-16/18-WIN11-Domain-DNS-Resolution.png)

#### DC01 DNS Resolution

![DC01 DNS Resolution](../../screenshots/Phase-16/19-WIN11-DC01-DNS-Resolution.png)

#### LDAP SRV Record

![LDAP SRV Record](../../screenshots/Phase-16/20-WIN11-LDAP-SRV-Record.png)

#### Pre-Join Domain Controller Discovery

![Pre-Join Domain Controller Discovery](../../screenshots/Phase-16/21-WIN11-DC-Discovery-PreJoin.png)

### Domain Join

#### Pre-Join System Properties

![Before Domain Join](../../screenshots/Phase-16/22-WIN11-Before-Domain-Join-System-Properties.png)

#### Domain Join Configuration

![Domain Join Configuration](../../screenshots/Phase-16/23-WIN11-Domain-Join-Configuration.png)

#### Domain Join Successful

![Domain Join Successful](../../screenshots/Phase-16/25-WIN11-Domain-Join-Success.png)

### Post-Join Validation

#### Domain User Authentication

![Domain User Authentication](../../screenshots/Phase-16/26-WIN11-Domain-User-Authentication.png)

#### Post-Join Domain Controller Discovery

![Post-Join Domain Controller Discovery](../../screenshots/Phase-16/27-WIN11-DC-Discovery-PostJoin-Success.png)

#### DC01 Computer Account

![DC01 WIN11 Computer Account](../../screenshots/Phase-16/29-DC01-WIN11-Computer-Account.png)

#### Active Directory Users and Computers

![WIN11-CLIENT01 Computer Account in Active Directory](../../screenshots/Phase-16/30-ADUC-WIN11-CLIENT01-Computer-Account.png)

#### Secure Channel Verification

![Windows 11 Secure Channel Verification](../../screenshots/Phase-16/31-WIN11-Secure-Channel-Verification.png)

---

## Phase 16 Conclusion

The evidence confirms that `WIN11-CLIENT01` was successfully integrated into the `enterprise.local` Active Directory environment.

Network connectivity, DNS resolution, LDAP communication, Domain Controller discovery, domain membership, domain authentication, Active Directory computer-account registration, and secure-channel communication were validated successfully.

The Windows 11 endpoint is therefore ready to participate in centralized enterprise security monitoring and future SOC detection and incident-response activities.
