# Lab 05 – Detection Rule Creation

## Objective

The objective of this lab was to create a custom Splunk detection rule capable of identifying excessive failed logon attempts. Failed logon events are commonly associated with password spraying, brute-force attacks, credential stuffing, and unauthorized access attempts. This lab demonstrates how a SOC analyst can transform raw log data into an actionable security alert.

---

## Tools Used

- Splunk Enterprise
- Windows Security Event Logs
- Windows PowerShell

---

## Detection Scenario

Monitor Windows Security Event ID 4625 (Failed Logon) and generate an alert when an account exceeds a predefined threshold of failed authentication attempts.

---

## Lab Tasks

### 1. Identify Failed Logon Events

A search was performed to identify failed authentication events within Windows Security logs.

Search used:

```spl
index=main EventCode=4625
```

Result:

```text
116 Failed Logon Events
```

---

### 2. Analyze Failed Logon Activity

Failed logon events were grouped by account name to identify accounts generating the highest number of authentication failures.

Search used:

```spl
index=main EventCode=4625
| stats count by Account_Name
| sort - count
```

Result:

```text
ANGIE_PC 26
angel 15
```

This allowed identification of accounts experiencing the highest concentration of failed authentication attempts.

---

### 3. Build Detection Logic

A threshold-based detection rule was created to identify accounts exceeding an acceptable number of failed logon attempts.

Search used:

```spl
index=main EventCode=4625
| stats count by Account_Name
| where count >= 5
```

Detection Logic:

```text
Generate an alert when an account records five or more failed logon attempts.
```

This threshold helps identify suspicious authentication activity while reducing noise from isolated login failures.

---

### 4. Configure Alert

The detection was saved as a Splunk alert.

Alert Configuration:

```text
Alert Name: Excessive Failed Logon Attempts

Trigger Type: Scheduled

Schedule: Every 5 Minutes

Trigger Condition:
Number of Results > 0

Severity:
Medium

Trigger Action:
Add to Triggered Alerts
```

---

### 5. Save Detection Rule

The alert was successfully saved and verified within Splunk's Searches, Reports, and Alerts configuration menu.

This converted the search query into an automated security monitoring rule capable of notifying analysts when suspicious authentication behavior occurs.

---

## Findings

The investigation confirmed:

- Windows failed logon events were successfully collected within Splunk.
- Event ID 4625 provided visibility into authentication failures.
- Failed logons could be grouped and analyzed by account.
- Threshold-based detections can be created directly within Splunk.
- Security monitoring can be automated through alerting mechanisms.

---

## Security Relevance

Failed logon monitoring is a foundational SOC detection use case because it helps identify:

- Password spraying attacks
- Brute-force authentication attempts
- Credential stuffing activity
- Unauthorized access attempts
- Misconfigured authentication systems

Security analysts frequently use Event ID 4625 detections as an early warning indicator during investigations.

---

## Evidence

### Screenshot 1
**01_failed_logon_events.png**

Initial search displaying Windows Event ID 4625 failed logon events.

### Screenshot 2
**02_failed_logon_statistics.png**

Statistical analysis showing failed logon counts by account.

### Screenshot 3
**03_detection_threshold_query.png**

Threshold-based detection query identifying accounts with excessive failed logons.

### Screenshot 4
**04_alert_configuration.png**

Splunk alert configuration showing scheduled execution, trigger conditions, and severity settings.

### Screenshot 5
**05_saved_detection_rule.png**

Saved Splunk detection rule visible within Searches, Reports, and Alerts.

---

## Key Takeaway

This lab demonstrated how to transform raw Windows authentication logs into an actionable security detection. By creating a threshold-based alert for excessive failed logon attempts, the lab replicated a common SOC monitoring workflow and introduced core detection engineering concepts used in real-world security operations centers.
