# INC0001001 — Active Directory Domain Discovery and Domain Join Failures

## Sentinel Ridge Cybersecurity Labs

### 1. Incident Overview

| Field | Details |
|---|---|
| Incident number | INC0001001 |
| Affected system | Windows Server — SCCM01 |
| Environment | Nonproduction cybersecurity laboratory |
| Category | Active Directory / DNS |
| Status | Resolved — Closed |
| Resolution code | Solved — Workaround |

### 2. Executive Summary

A Windows Server intended to support Microsoft Configuration Manager experienced persistent Active Directory domain discovery and domain join failures.

The investigation involved network connectivity validation, DNS troubleshooting, Active Directory service discovery, LDAP connectivity testing, and operating system recovery.

Domain membership was successfully established following a server rebuild and an IPv6 configuration workaround.

### 3. Incident Description

The affected Windows Server was unable to discover the Active Directory domain controller or join the internal laboratory domain.

Domain controller discovery repeatedly returned:

`ERROR_NO_SUCH_DOMAIN (1355)`

The failure prevented completion of the planned server deployment.

### 4. Business and Technical Impact

- Active Directory domain membership could not be established.
- Microsoft Configuration Manager deployment preparation was delayed.
- Internal DNS resolution required further investigation.
- No production business systems were affected.

### 5. Investigation and Troubleshooting

| Investigation | Finding |
|---|---|
| Network connectivity | Connectivity to the domain controller was verified |
| DNS SRV records | Successfully retrieved through direct queries to the domain controller |
| Default DNS resolution | Failed despite the correct IPv4 DNS server configuration |
| IPv6 DNS configuration | An external DNS server was present and could not resolve the internal domain |
| LDAP connectivity | UDP port 389 communication verified using PortQry |
| Initial IPv6 workaround | Disabling IPv6 on the original installation did not resolve the issue |

### 6. Root Cause Assessment

The rebuilt server's domain discovery failure was associated with an external IPv6 DNS configuration that could not resolve the internal Active Directory domain.

However, the investigation did not conclusively establish why the original Windows Server installation continued to experience domain discovery failures after IPv6 was disabled.

Root cause classification: Partially established.

### 7. Remediation

The original Windows Server installation was rebuilt.

On the fresh installation, disabling the Ethernet adapter's IPv6 binding restored Active Directory domain controller discovery.

The following command was used to validate domain controller discovery:

`nltest /dsgetdc:<internal-domain> /force`

The rebuilt Windows Server subsequently joined the Active Directory domain successfully.

### 8. Resolution Validation

| Validation | Result |
|---|---|
| LDAP communication over UDP 389 | PASS |
| DNS SRV record lookup | PASS |
| Domain controller discovery | PASS |
| Active Directory domain join | PASS |
| Final server rename verification | Pending confirmation |
| Domain membership following final rename and restart | Pending validation |

### 9. Security and Operational Considerations

Active Directory relies heavily on DNS for service discovery and authentication-related operations.

Incorrect DNS configurations can prevent systems from locating domain controllers even when basic network connectivity is available.

Disabling IPv6 was used as a temporary workaround rather than a permanent architectural solution.

### 10. Preventive Recommendations

- Verify internal DNS configuration before attempting domain joins.
- Validate Active Directory DNS SRV records.
- Review both IPv4 and IPv6 DNS settings.
- Investigate the source of unexpected external DNS configuration.
- Restore IPv6 following validation of the corrected DNS configuration.
- Maintain server configuration and recovery documentation.

### 11. Technical Competencies Demonstrated

- Active Directory administration
- DNS troubleshooting
- IPv4 and IPv6 configuration analysis
- LDAP connectivity validation
- Windows Server administration
- Domain controller discovery
- Structured incident management
- Root cause assessment
- Resolution validation

### 12. Lessons Learned

Successful network connectivity does not guarantee successful Active Directory service discovery.

DNS configuration must be evaluated across both IPv4 and IPv6.

A successful workaround should not be represented as a fully established root cause or permanent remediation.

### 13. Incident Closure

The primary incident objective was achieved through successful Active Directory domain discovery and domain membership restoration.

Permanent IPv6 DNS remediation and final server configuration verification were retained as follow-up activities.

**Final status:** RESOLVED — CLOSED

**Resolution classification:** Workaround / Server Rebuild

---

Sentinel Ridge Cybersecurity Labs

*Investigate. Remediate. Validate. Document.*
