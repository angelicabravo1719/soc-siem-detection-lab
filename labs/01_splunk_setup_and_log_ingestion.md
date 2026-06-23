# Lab 01 — Splunk Setup and Log Ingestion

## Goal

Install and configure Splunk Enterprise, ingest Windows Security Event Logs, and verify that security events can be collected, indexed, and searched through a SIEM platform.

Centralized log collection is a foundational SOC capability because investigations, detections, and alerts all depend on accessible log data.

---

## What I Did

* Installed Splunk Enterprise 10.4.0 on Windows.
* Configured an administrative account.
* Accessed the Splunk web interface.
* Navigated to the Search & Reporting application.
* Added Windows Event Logs as a data source.
* Ingested Windows Security events into Splunk.
* Verified successful indexing and event visibility.

---

## Tools Used

### Splunk Enterprise 10.4.0

Used to collect, index, search, and analyze Windows Security Event Logs.

### Windows Event Logs

Provided the security telemetry ingested into Splunk.

---

## Search Query

### Verify Log Ingestion

```spl
index=main
```

---

## What I Observed

Splunk successfully ingested Windows Security logs from the local host.

The search query returned indexed Windows Security events, confirming that log collection and indexing were functioning properly. Event IDs, host information, source details, and timestamps were visible and searchable.

---

## Evidence Collected

### Screenshots

Store screenshots in:

```text
screenshots/lab-01-splunk-setup-and-log-ingestion/
```

Files:

```text
splunk-home-dashboard.png
windows-events-ingested.png
```

---

## Investigation Findings

### SIEM Deployment

Splunk Enterprise was successfully installed and configured on a Windows workstation.

### Log Collection

Windows Security Event Logs were successfully collected and indexed within Splunk.

### Event Visibility

Indexed events contained useful investigation data including:

* Event IDs
* Timestamps
* Host information
* Security log sources
* Windows authentication activity

### Security Relevance

Centralized log collection allows analysts to:

* Investigate suspicious activity
* Monitor authentication events
* Search historical logs
* Build detections and alerts
* Perform incident response activities

---

## Key Takeaways

* Splunk successfully collected and indexed Windows Security logs.
* Security events became searchable through the Search & Reporting application.
* SIEM platforms provide centralized visibility across security data sources.
* Log ingestion is the first step in building detection and monitoring capabilities.

---

## Conclusion

Splunk Enterprise was successfully deployed and configured to ingest Windows Security Event Logs. Indexed events were searchable through Splunk's Search & Reporting application, demonstrating the core functionality of a SIEM platform and establishing the foundation for future detection and investigation labs.

---

## Note

This lab was performed in a personal lab environment for educational and portfolio development purposes.

