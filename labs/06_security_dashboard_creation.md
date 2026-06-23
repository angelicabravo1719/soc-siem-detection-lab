# Lab 06 – Security Dashboard Creation

## Objective

The objective of this lab was to create a centralized security monitoring dashboard within Splunk to visualize Windows authentication activity. Dashboards allow security analysts to quickly identify trends, monitor authentication events, and investigate suspicious behavior without manually reviewing individual log entries.

---

## Tools Used

- Splunk Enterprise
- Windows Security Event Logs
- Windows Authentication Logs

---

## Dashboard Overview

A security dashboard was created to provide visibility into:

- Successful Logons (Event ID 4624)
- Failed Logons (Event ID 4625)
- Failed Logons by Account
- Authentication Activity Over Time

The dashboard consolidates multiple searches into a single monitoring interface commonly used within Security Operations Centers (SOCs).

---

## Dashboard Configuration

### Dashboard Name

```text
Windows Security Monitoring Dashboard
```

### Description

```text
Security monitoring dashboard displaying Windows authentication activity, failed logon attempts, and account-based login trends collected through Splunk.
```

### Visibility

```text
Private
```

---

## Panel 1 – Successful Logons

Purpose:

Monitor successful authentication activity within the environment.

Search Used:

```spl
index=main EventCode=4624
| stats count
```

Visualization:

```text
Single Value
```

---

## Panel 2 – Failed Logons

Purpose:

Monitor failed authentication attempts that may indicate user mistakes or suspicious activity.

Search Used:

```spl
index=main EventCode=4625
| stats count
```

Visualization:

```text
Single Value
```

---

## Panel 3 – Failed Logons by Account

Purpose:

Identify which accounts are generating the highest number of failed authentication attempts.

Search Used:

```spl
index=main EventCode=4625
| stats count by Account_Name
| sort - count
```

Visualization:

```text
Bar Chart
```

---

## Panel 4 – Authentication Activity Timeline

Purpose:

Visualize authentication activity over time and compare successful versus failed logon events.

Search Used:

```spl
index=main (EventCode=4624 OR EventCode=4625)
| timechart count by EventCode
```

Visualization:

```text
Line Chart
```

---

## Findings

The dashboard successfully provided:

- Visibility into successful user authentication activity.
- Visibility into failed authentication attempts.
- Account-level authentication analysis.
- Historical authentication trends.
- A centralized security monitoring view.

The dashboard demonstrated how Windows Security Events can be transformed into actionable security metrics through SIEM visualization.

---

## Security Relevance

Authentication monitoring is one of the most common use cases within a Security Operations Center.

Security teams routinely monitor:

- Successful logons
- Failed logons
- Brute-force attempts
- Password spraying attacks
- Credential abuse
- Unauthorized access attempts

Dashboards provide analysts with a rapid method of identifying anomalies and prioritizing investigations.

---

## Evidence

### Screenshot 1

**01_dashboard_creation.png**

Creation of the Windows Security Monitoring Dashboard.

### Screenshot 2

**02_successful_logons_panel.png**

Single-value visualization showing successful logon activity.

### Screenshot 3

**03_failed_logons_panel.png**

Single-value visualization showing failed logon activity.

### Screenshot 4

**04_failed_logons_by_account.png**

Bar chart displaying failed logon attempts grouped by account.

### Screenshot 5

**05_authentication_activity_timeline.png**

Timeline visualization comparing successful and failed authentication events.

### Screenshot 6

**06_complete_security_dashboard.png**

Completed Windows Security Monitoring Dashboard displaying all panels.

---

## Key Takeaway

This lab demonstrated how security analysts can transform raw Windows Security Event logs into meaningful dashboards that provide real-time visibility into authentication activity. By combining multiple searches into a centralized monitoring view, the dashboard replicated a common SOC workflow used for security monitoring, threat detection, and incident investigation.
