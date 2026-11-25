# INC0001004 — Gatekeeper-01 Linux Administrative Access Recovery

## Sentinel Ridge Cybersecurity Labs

### 1. Incident Overview

| Field | Details |
|---|---|
| Incident number | INC0001004 |
| Incident date | November 25, 2026 |
| Resolution date | November 25, 2026 |
| Affected system | Gatekeeper-01 |
| Hardware | Dell Wyse 3040 Thin Client |
| Operating system | Debian GNU/Linux 13 |
| Affected service | Pi-hole DNS Administration |
| Category | Identity and Access Management |
| Subcategory | Linux Authentication |
| Impact | 3 — Low |
| Urgency | 3 — Low |
| Priority | 4 — Low |
| Assignment group | Linux Systems Administration |
| Environment | Nonproduction Cybersecurity Laboratory |
| Resolution code | Solved — Administrative Access Restored |
| Status | Resolved — Closed |

### 2. Executive Summary

While preparing a Debian-based Pi-hole DNS server for a security assessment, an administrative authentication failure was encountered.

The system had recently been returned to operation following an extended period of inactivity.

Attempts to authenticate through SSH and the physical console were unsuccessful, preventing administrative maintenance.

A structured investigation and authorized system recovery procedure were performed to restore access to the existing Linux account.

Following password recovery, local authentication, remote SSH authentication, privileged administrative access, Pi-hole service availability, and independent DNS resolution were successfully validated.

The incident was resolved without reinstalling the operating system or intentionally weakening existing administrative privilege restrictions.

### 3. Business and Technical Impact

#### Business Impact

The incident occurred within a controlled, nonproduction cybersecurity laboratory.

No production business impact was identified.

The authentication failure delayed planned vulnerability assessment, patch management, and secure remote access activities.

#### Technical Impact

- Local authentication was unsuccessful.
- Remote SSH authentication was unsuccessful.
- Administrative maintenance could not proceed.
- Security assessment activities were delayed.

No DNS service outage was established during the investigation.

### 4. Asset Information

| Attribute | Configuration |
|---|---|
| Manufacturer | Dell |
| Model | Wyse 3040 |
| Processor | Intel Atom x5-Z8350 |
| Architecture | x86_64 |
| Operating system | Debian GNU/Linux 13 |
| Primary application | Pi-hole |
| Primary function | DNS resolution and filtering |
| Remote administration | SSH |

Sensitive network addressing, account identifiers, and detailed configuration information have been omitted from this public report.

### 5. Investigation and Troubleshooting

#### Step 1 — Verify Remote Connectivity

Initial SSH connection attempts established that the system was reachable over the local network.

Authentication attempts were unsuccessful.

This allowed the investigation to distinguish network connectivity from authentication failure.

#### Step 2 — Verify Physical Console Access

A monitor and keyboard were connected directly to the affected system.

Local authentication attempts were also unsuccessful.

The investigation established that the authentication problem was not limited to SSH.

#### Step 3 — Identify the Operating System

The system boot environment was inspected.

The installed operating system was confirmed as Debian GNU/Linux.

This ensured that the recovery procedure was appropriate for the affected platform.

#### Step 4 — Evaluate Standard Recovery Options

The standard operating system recovery environment was attempted.

Authentication requirements prevented successful access through the initial recovery method.

An alternative authorized local recovery procedure was subsequently performed.

#### Step 5 — Establish an Authorized Recovery Environment

Physical access was used to obtain a temporary privileged recovery environment.

No permanent bootloader configuration changes were intentionally made.

The recovery procedure also highlighted the relationship between physical access security and operating system authentication controls.

Detailed recovery parameters are retained in the private operational incident record.

#### Step 6 — Identify the Existing Linux Account

Commands executed:

`ls /home`

`id <lab-user>`

The investigation confirmed that the existing user account was present.

The account's user ID, primary group, and supplementary group memberships were reviewed.

The existing account was retained rather than replaced.

#### Step 7 — Recover Account Authentication

Command executed:

`passwd <lab-user>`

Initial password-reset attempts were unsuccessful because the password confirmation did not match.

A subsequent attempt completed successfully.

Observed result:

`passwd: password updated successfully`

The existing account password was recovered without intentionally modifying group memberships or administrative permissions.

#### Step 8 — Restore Normal System Operation

The system returned to its normal operating environment.

Local authentication using the recovered account succeeded.

No operating system reinstallation was required.

#### Step 9 — Validate Network Configuration

Command executed:

`ip -br addr`

The network interface configuration was reviewed, and the system's local network connectivity was confirmed.

Additional network configuration observations were retained for a separate security assessment.

#### Step 10 — Validate Remote SSH Authentication

Command executed from Windows PowerShell:

`ssh <lab-user>@<lab-server-ip>`

Result: Successful.

The recovered account authenticated remotely using its updated password.

#### Step 11 — Review Administrative Authorization

Command executed:

`sudo -l`

The recovered account was not authorized to execute sudo commands.

This finding was treated as an existing privilege restriction rather than a confirmed configuration defect.

No additional sudo permissions were assigned.

#### Step 12 — Validate Privileged Administrative Access

Command executed:

`su -`

Privileged administrative access was successfully established using the existing root credentials.

The root password was not reset.

Existing privilege separation was preserved.

### 6. Root Cause Assessment

**Root cause status: Undetermined**

The investigation confirmed that the existing Linux account could not initially authenticate through either the physical console or SSH.

Resetting the account password restored authentication.

The exact reason the original credentials were unsuccessful was not conclusively established.

No evidence established that the authentication failure resulted from malicious activity.

A comprehensive security compromise assessment was outside the scope of this incident.

### 7. Remediation Actions

The following actions were completed:

1. Identified the affected Linux operating system.
2. Established an authorized recovery environment.
3. Identified the existing user account.
4. Successfully reset the account password.
5. Restored normal system operation.
6. Validated local authentication.
7. Validated remote SSH authentication.
8. Reviewed existing administrative authorization.
9. Restored privileged administrative access.
10. Validated Pi-hole service functionality.
11. Independently verified DNS resolution from a Windows workstation.

### 8. Service and Resolution Validation

#### Validation 1 — Pi-hole Service Status

Command executed:

`systemctl status pihole-FTL --no-pager`

Observed result:

`Active: active (running)`

The Pi-hole DNS service was operational.

**Result: PASS**

#### Validation 2 — Local DNS Resolution

Command executed from the Linux server:

`nslookup example.com <lab-server-ip>`

The DNS server successfully returned IPv4 and IPv6 address records.

**Result: PASS**

#### Validation 3 — Independent Remote DNS Resolution

Command executed directly from Windows PowerShell:

`nslookup example.com <lab-server-ip>`

Observed results:

- The Pi-hole DNS server responded successfully.
- IPv4 address records were returned.
- IPv6 address records were returned.
- The DNS query completed successfully.

This independently confirmed that another network device could communicate with the Pi-hole DNS service.

**Result: PASS**

#### Final Validation Matrix

| Validation requirement | Result |
|---|---|
| Existing Linux account identified | PASS |
| Password recovery | PASS |
| Normal operating system boot | PASS |
| Local authentication | PASS |
| Remote SSH authentication | PASS |
| Privileged administrative access | PASS |
| Pi-hole service availability | PASS |
| Local DNS resolution | PASS |
| Independent remote DNS resolution | PASS |
| Existing privilege restrictions preserved | PASS |

DNS filtering effectiveness and IPv6 transport connectivity were not independently validated during this incident.

### 9. Security Controls Preserved

| Security consideration | Remediation outcome |
|---|---|
| Existing Linux account | Retained |
| Account group memberships | No intentional changes |
| Sudo authorization | No additional permissions assigned |
| Root account password | Not reset |
| Operating system | No reinstallation |
| Bootloader configuration | No intentional permanent changes |
| Pi-hole configuration | No intentional changes |

### 10. Security Risk Considerations

The investigation identified additional security topics requiring further assessment.

| Security area | Recommended assessment |
|---|---|
| Remote administration | Review SSH authentication and access restrictions |
| Physical security | Evaluate bootloader protection and authorized recovery controls |
| Network security | Review IPv4 and IPv6 exposure |
| Remote access | Assess existing remote connectivity configurations |
| Vulnerability management | Evaluate installed software and patch currency |
| System resilience | Review backup and recovery procedures |

These observations represent areas for further investigation rather than confirmed exploitable vulnerabilities.

Detailed information concerning unremediated security conditions is retained in the private operational incident record.

### 11. NIST SP 800-53 Rev. 5 Control Mapping

| Control | Control area | Incident relevance |
|---|---|---|
| AC-2 | Account Management | Existing account identification and recovery |
| AC-6 | Least Privilege | Existing administrative privilege restrictions preserved |
| IA-2 | Identification and Authentication | Local and remote authentication restored |
| IA-5 | Authenticator Management | Authorized password recovery |
| PE-3 | Physical Access Control | Physical access security considerations identified |
| CM-6 | Configuration Settings | System configuration review |
| RA-5 | Vulnerability Monitoring and Scanning | Separate vulnerability assessment planned |
| SI-2 | Flaw Remediation | Separate patch assessment planned |
| IR-4 | Incident Handling | Investigation, recovery and validation |
| IR-5 | Incident Monitoring | Incident tracking and documentation |

This mapping identifies relevant security control areas for educational purposes and does not constitute a formal compliance assessment.

### 12. Preventive Recommendations

- Maintain secure administrative credential management.
- Document authorized account recovery procedures.
- Review SSH authentication and administrative access policies.
- Evaluate physical access and bootloader security controls.
- Establish regular vulnerability assessment and patch management procedures.
- Maintain system configuration backups.
- Review remote access configurations.
- Perform independent service validation following system recovery.
- Maintain accurate incident and change management records.

### 13. Technical Competencies Demonstrated

- Debian Linux administration
- Linux account management
- Authentication troubleshooting
- Authorized credential recovery
- Privileged access management
- Least privilege
- SSH administration
- Network configuration analysis
- DNS troubleshooting
- Pi-hole service administration
- Windows PowerShell
- Security risk identification
- NIST security control mapping
- Incident management
- Independent resolution validation

### 14. Lessons Learned

Authentication and authorization are separate security functions.

Successful network connectivity does not guarantee successful authentication.

Administrative recovery procedures must balance operational availability with security requirements.

Existing privilege restrictions should be preserved wherever practical during troubleshooting.

Local service validation should be supplemented with independent client testing.

Successful remediation does not automatically establish a definitive root cause.

Restoring system functionality does not establish that the system is free from security vulnerabilities.

### 15. Follow-Up Activities

The following activities will be addressed through separate security assessment and change management records:

- Asset and software inventory
- Network attack surface enumeration
- Vulnerability assessment
- Patch management
- Configuration backup
- System hardening
- Post-remediation validation
- DNS filtering validation
- Secure remote access assessment and implementation

These activities were not completed as part of this incident.

### 16. Incident Closure

The primary incident objective was achieved through successful administrative account recovery and restoration of privileged access.

Local authentication, remote SSH authentication, Pi-hole service availability, and independent remote DNS resolution were successfully validated.

Existing administrative privilege restrictions were preserved.

**Resolution:** Linux account password recovery and privileged access restoration.

**Resolution code:** Solved — Administrative Access Restored.

**Root cause:** Undetermined.

**Service validation:** Successful.

**Production impact:** None identified.

**Final status:** RESOLVED — CLOSED

---

Sentinel Ridge Cybersecurity Labs

Linux Systems Administration & Security Engineering

*Investigate. Remediate. Validate. Document.*
