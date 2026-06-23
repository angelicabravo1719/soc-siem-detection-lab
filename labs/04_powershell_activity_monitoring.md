# Lab 04 – PowerShell Activity Monitoring

## Objective

The objective of this lab was to investigate PowerShell activity within Splunk and validate whether PowerShell Script Block Logging events (Event ID 4104) could be collected and analyzed. PowerShell is commonly abused by attackers for reconnaissance, execution, persistence, and post-exploitation activities, making visibility into PowerShell activity an important component of SOC monitoring.

---

## Tools Used

- Splunk Enterprise
- Windows PowerShell
- Windows Registry
- Windows Event Logs

---

## Lab Tasks

### 1. Search for PowerShell Activity

A Splunk search was performed to identify PowerShell-related events.

Example search:

```spl
index=main powershell
```

The search returned events showing execution of `powershell.exe` on the system.

---

### 2. Enable Script Block Logging

Script Block Logging was enabled through the Windows Registry using an elevated PowerShell session.

Commands used:

```powershell
New-Item -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Force

Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Name EnableScriptBlockLogging -Value 1
```

Verification:

```powershell
Get-ItemProperty "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging"
```

Result:

```text
EnableScriptBlockLogging : 1
```

---

### 3. Generate Test PowerShell Activity

Several PowerShell commands were executed to generate activity for monitoring.

Commands executed:

```powershell
Get-Process
Get-Service
Get-ChildItem C:\Users
```

---

### 4. Search for Event ID 4104

A search was conducted to identify PowerShell Script Block Logging events.

Search used:

```spl
index=main EventCode=4104
```

Result:

```text
0 Events Returned
```

Additional searches for PowerShell Operational logs also returned no results.

---

## Findings

The investigation confirmed that:

- PowerShell activity was visible within Splunk.
- Script Block Logging was successfully enabled through the Windows Registry.
- Test PowerShell commands executed successfully.
- Event ID 4104 was not observed within Splunk.
- Splunk was ingesting Windows Security logs but was not collecting the PowerShell Operational log channel required for Event ID 4104 visibility.

---

## Security Relevance

PowerShell is frequently used by threat actors because it provides direct access to system administration functionality and can execute malicious commands without requiring additional tools.

SOC analysts commonly monitor PowerShell activity to identify:

- Suspicious command execution
- Reconnaissance activity
- Script-based malware
- Living-off-the-land techniques (LOLBins)
- Post-exploitation behavior

This lab demonstrated the process of validating logging configurations, generating activity, and investigating missing telemetry within a SIEM environment.

---

## Evidence

### Screenshot 1
**01_initial_4104_search_no_results.png**

Initial search for Event ID 4104 showing no results.

### Screenshot 2
**02_4104_validation_after_configuration.png**

Post-configuration validation showing no Event ID 4104 events after enabling Script Block Logging and generating PowerShell activity.

### Screenshot 3
**03_enable_script_block_logging.png**

Registry configuration used to enable PowerShell Script Block Logging.

### Screenshot 4
**04_verify_script_block_logging.png**

Verification showing `EnableScriptBlockLogging = 1`.

### Screenshot 5
**05_powershell_test_commands.png**

PowerShell commands executed to generate activity.

### Screenshot 6
**06_powershell_activity_detected_in_splunk.png**

Splunk search showing PowerShell process activity observed through Windows Security logs.

---

## Key Takeaway

This lab demonstrated how to monitor PowerShell activity within Splunk, validate logging configurations, and investigate missing telemetry sources. Although Event ID 4104 was not collected, the investigation identified a logging visibility gap and highlighted the importance of ensuring that PowerShell Operational logs are forwarded to the SIEM for complete PowerShell monitoring.
