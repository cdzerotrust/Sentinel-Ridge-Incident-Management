# Sentinel Ridge Cybersecurity Labs

## Master Incident Register

### 1. Purpose

This register maintains a centralized record of technical incidents investigated within Sentinel Ridge Cybersecurity Labs.

It supports incident tracking, ticket number management, resolution accountability, security risk identification, and historical reference.

### 2. Incident Register

| Incident ID | Description | Affected System | Category | Status |
|---|---|---|---|---|
| INC0001001 | Active Directory Domain Discovery and Domain Join Failures | SCCM01 | Active Directory / DNS | Closed |
| INC0001002 | Windows Server 2022 Evaluation-to-Standard Conversion Failure | SCCM01 | Operating System / Licensing | Resolved |
| INC0001003 | Microsoft Entra ID Authentication Incident | Microsoft Entra ID | Identity and Access Management | Closed |
| INC0001004 | Linux Administrative Access Recovery | Gatekeeper-01 | Linux / Identity and Access Management | Closed |

### 3. Resolution Register

| Incident ID | Resolution | Root Cause Status |
|---|---|---|
| INC0001001 | Server rebuild and IPv6 DNS workaround | Partially established |
| INC0001002 | Windows servicing, edition conversion and permanent activation | Undetermined |
| INC0001003 | Additional security information registration and verification | Immediate cause confirmed |
| INC0001004 | Linux account password recovery and privileged access restoration | Undetermined |

### 4. Outstanding Follow-Up Activities

| Incident ID | Follow-up activity | Status |
|---|---|---|
| INC0001001 | Permanent IPv6 DNS remediation and final server configuration verification | Pending verification |
| INC0001002 | Maintain operating system servicing and backup procedures | Preventive recommendation |
| INC0001003 | Emergency access account resilience assessment | Pending verification |
| INC0001004 | Vulnerability assessment, system hardening and remote access security review | Pending |

### 5. Ticket Number Management

| Record | Value |
|---|---|
| Ticket prefix | INC |
| Latest assigned incident | INC0001004 |
| Next available incident | INC0001005 |

Incident numbers must be verified against the master register before assignment.

Incident management and change management maintain separate numbering sequences.

Assigned incident numbers must not be reused.

### 6. Incident Closure Requirements

Before an incident is formally closed:

- Confirm that the primary incident objective has been achieved.
- Validate restored functionality.
- Document investigation and remediation activities.
- Distinguish confirmed root causes from suspected contributing factors.
- Record residual risks and outstanding follow-up activities.
- Update the master incident register.
- Retain appropriate supporting evidence.

### 7. Register Maintenance

The register must be updated whenever an incident is opened, resolved, reopened, or closed.

Public documentation must be reviewed and sanitized before publication.

All recorded incidents originate from authorized, nonproduction laboratory environments.

---

**Register owner:** Sentinel Ridge Cybersecurity Labs

**Last updated:** November 25, 2026

*Investigate. Remediate. Validate. Document.*
