# Lab 02 — Authentication Event Analysis

## Goal

Analyze Windows authentication activity using Splunk and identify successful and failed logon events.

Authentication monitoring is a core responsibility of Security Operations Centers (SOCs) because login activity often provides early indicators of account misuse, brute-force attempts, and unauthorized access.

---

## What I Did

* Queried Windows Security logs in Splunk.
* Identified successful logon events.
* Identified failed logon events.
* Compared authentication outcomes.
* Reviewed event metadata associated with each authentication attempt.

---

## Tools Used

### Splunk Enterprise

Used to search and analyze Windows Security Event Logs.

### Windows Event Logs

Provided authentication events collected from the local Windows system.

---

## Search Queries

### Successful Logons

```spl
index=main EventCode=4624
```

### Failed Logons

```spl
index=main EventCode=4625
```

---

## What I Observed

### Event ID 4624

Represents a successful authentication event.

The search returned multiple successful logons originating from the local system.

### Event ID 4625

Represents a failed authentication event.

The search returned multiple failed authentication attempts that had been previously generated during account lockout testing.

---

## Evidence Collected

### Screenshots

Store screenshots in:

```text
screenshots/lab-02-authentication-event-analysis/
```

Files:

```text
successful-logon-events-4624.png
failed-logon-events-4625.png
```

---

## Investigation Findings

### Successful Authentication Activity

Multiple Event ID 4624 entries were observed indicating successful user logons.

### Failed Authentication Activity

Multiple Event ID 4625 entries were observed indicating failed logon attempts.

### Authentication Visibility

Splunk successfully ingested and indexed Windows Security events, allowing authentication activity to be quickly identified and analyzed.

### Security Relevance

Authentication logs are frequently reviewed by SOC analysts when investigating:

* Brute-force activity
* Credential misuse
* Unauthorized access attempts
* Account lockouts
* Privilege escalation investigations

---

## Key Takeaways

* Event ID 4624 indicates successful authentication.
* Event ID 4625 indicates failed authentication.
* Splunk can rapidly identify authentication activity across large datasets.
* Authentication monitoring is a foundational SOC analyst responsibility.

---

## Conclusion

Windows authentication events were successfully collected and analyzed using Splunk. Successful and failed logon activity was identified through Event IDs 4624 and 4625, demonstrating how SIEM platforms support security monitoring and incident investigations.

---

## Note

This lab was performed in a personal lab environment for educational and portfolio development purposes.
