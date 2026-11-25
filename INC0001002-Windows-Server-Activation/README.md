# INC0001002 — Windows Server 2022 Activation and Edition Conversion Failure

## Sentinel Ridge Cybersecurity Labs

### 1. Incident Overview

| Field | Details |
|---|---|
| Incident number | INC0001002 |
| Affected system | SCCM01 |
| Operating system | Windows Server 2022 |
| Environment | Proxmox Virtualization / Cybersecurity Home Lab |
| Category | Software |
| Subcategory | Operating System / Licensing |
| Impact | 3 — Low |
| Urgency | 3 — Low |
| Priority | 4 — Low |
| Assignment group | Windows Server Administration |
| Status | Resolved |
| Resolution code | Solved — Permanently |

### 2. Executive Summary

During the preparation of a Windows Server 2022 virtual machine intended for Microsoft Configuration Manager, an operating system activation and edition conversion failure was encountered.

The server was running Windows Server 2022 Standard Evaluation. Attempts to activate the operating system and convert it to the full Standard edition initially failed.

A structured investigation was conducted using Windows licensing utilities, DISM, PowerShell, operating system integrity checks, and Windows Update servicing.

Following the installation of available Windows updates, the edition conversion completed successfully, and permanent operating system activation was verified.

### 3. Incident Description

The initial Windows activation attempt returned:

`0xC004F069`

Subsequent attempts to convert the operating system from the Evaluation edition to the Standard edition returned:

- DISM Error: 50
- HRESULT: 0x80070032

The operating system rejected the requested edition conversion despite reporting Standard as a supported target edition.

### 4. Business and Technical Impact

- Windows Server remained on the Evaluation edition.
- Permanent operating system activation could not initially be completed.
- The Evaluation license was limited to a 180-day period.
- Microsoft Configuration Manager deployment preparation was delayed.
- No production systems or business services were affected.

### 5. Investigation and Troubleshooting

#### Step 1 — Verify the Current Windows Edition

Command:

`DISM /Online /Get-CurrentEdition`

Result:

`ServerStandardEval`

Confirmed that the server was running Windows Server 2022 Standard Evaluation.

#### Step 2 — Identify Supported Target Editions

Command:

`DISM /Online /Get-TargetEditions`

Supported target editions:

- ServerStandard
- ServerDatacenter

Confirmed that Windows reported support for conversion to the Standard edition.

#### Step 3 — Attempt Edition Conversion

DISM was executed using the Set-Edition parameter and an appropriate product key.

The conversion failed with Error 50 and HRESULT 0x80070032.

#### Step 4 — Review DISM Logs

Log file reviewed:

`C:\Windows\Logs\DISM\dism.log`

The logs confirmed that the requested edition conversion had been rejected.

#### Step 5 — Review Installed Windows Features

PowerShell command:

`Get-WindowsFeature | Where-Object Installed -eq $true`

No obvious installed server role restrictions were identified.

Active Directory Domain Services was not installed on the affected server.

#### Step 6 — Verify Windows Licensing Status

Command:

`slmgr /dlv`

Findings:

- Edition: ServerStandardEval
- Licensing channel: TIMEBASED_EVAL
- License status: Licensed
- Evaluation period remaining: 180 days

The Evaluation license was functioning correctly.

#### Step 7 — Verify Component Store Integrity

Command:

`DISM /Online /Cleanup-Image /ScanHealth`

Result: No component store corruption detected.

#### Step 8 — Verify System File Integrity

Command:

`sfc /scannow`

Result: Windows Resource Protection did not identify any integrity violations.

#### Step 9 — Perform Windows Update Servicing

Available Windows updates were identified through PowerShell.

Updates included:

- Windows Server cumulative updates
- .NET Framework cumulative updates
- Microsoft Defender security intelligence updates
- Windows Malicious Software Removal Tool updates

Windows updates were installed, followed by a system restart.

#### Step 10 — Retry Edition Conversion

The DISM edition conversion operation was repeated following Windows servicing.

Target edition:

`ServerStandard`

Result: Successful.

#### Step 11 — Verify Windows Activation

Commands:

`slmgr /ipk <REDACTED_PRODUCT_KEY>`

`slmgr /ato`

`slmgr /xpr`

Final result:

Windows Server Standard edition was permanently activated.

### 6. Root Cause Assessment

**Root cause status: Undetermined**

The investigation established that:

- The requested target edition was supported.
- No obvious installed server role prevented conversion.
- Component store integrity checks passed.
- System file integrity checks passed.
- The Evaluation license was functioning normally.

The edition conversion succeeded following Windows servicing.

The initial operating system build or servicing state was identified as a suspected contributing factor.

However, the available evidence did not conclusively establish that missing Windows updates caused the original conversion failure.

### 7. Remediation

The incident was resolved through:

1. Installation of applicable Windows updates.
2. System restart.
3. Successful conversion from Windows Server Standard Evaluation to Windows Server Standard.
4. Operating system activation.
5. Verification of permanent activation.

### 8. Resolution Validation

| Validation | Result |
|---|---|
| Supported target edition identified | PASS |
| Component store integrity | PASS |
| System file integrity | PASS |
| Edition conversion | PASS |
| Windows Server Standard edition | Confirmed |
| Permanent activation | Confirmed |
| Server availability | PASS |

### 9. Preventive Recommendations

- Install applicable operating system updates before significant configuration changes.
- Verify supported edition conversion paths.
- Confirm product-key compatibility and licensing requirements.
- Review DISM logs when servicing operations fail.
- Perform component store and system file integrity checks where appropriate.
- Create a virtual machine backup or snapshot before significant operating system changes.
- Document licensing changes and activation verification.

### 10. Technical Competencies Demonstrated

- Windows Server 2022 administration
- PowerShell administration
- Windows licensing management
- DISM troubleshooting
- Operating system integrity validation
- Windows Update servicing
- Log analysis
- Virtualized infrastructure administration
- Root cause assessment
- Incident management
- Resolution validation

### 11. Lessons Learned

A supported operating system conversion path does not guarantee that the conversion will complete successfully.

Operating system servicing, licensing compatibility, installed server roles, and system integrity should be evaluated systematically.

Successful remediation must not be confused with definitive root cause identification.

Permanent activation should be independently verified before an incident is resolved.

### 12. Incident Closure

Windows Server 2022 Standard Evaluation was successfully converted to Windows Server 2022 Standard.

Permanent activation was independently verified using the Windows licensing utility.

The server remained available for continued Microsoft Configuration Manager deployment preparation.

**Final status:** RESOLVED

**Resolution classification:** Solved — Permanently

**Root cause:** Undetermined; operating system servicing state suspected as a contributing factor.

**Production impact:** None.

---

Sentinel Ridge Cybersecurity Labs

*Investigate. Remediate. Validate. Document.*
