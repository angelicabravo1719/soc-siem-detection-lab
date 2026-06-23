# Lab 03 – Failed Logon Detection

## Objective

Investigate failed Windows authentication attempts using Splunk and Security Event ID 4625. The goal was to identify failed logon activity, determine which accounts were affected, and identify the source of the authentication failures.

---

## Tools Used

- Splunk Enterprise
- Windows Security Event Logs
- SPL (Search Processing Language)

---

## Data Source

```text
WinEventLog:Security
```

---

## Step 1 – Locate Failed Logon Events

Security Event ID 4625 records failed Windows logon attempts.

### SPL Query

```spl
index=main EventCode=4625
```

### Evidence

`failed-logon-events-table.png`

### Result

Splunk returned multiple failed authentication events from the Windows Security log.

---

## Step 2 – Review Failed Authentication Details

Extracted key fields from the failed logon events to review account names, source addresses, and failure information.

### SPL Query

```spl
index=main EventCode=4625
| table _time Account_Name Source_Network_Address Failure_Reason
```

### Evidence

`failed-logon-events-table.png`

### Result

The failed logon events contained account information and source network details useful for authentication investigations.

---

## Step 3 – Count Failed Logons by Account

Aggregated failed authentication attempts by account name.

### SPL Query

```spl
index=main EventCode=4625
| stats count by Account_Name
| sort - count
```

### Evidence

`failed-logons-by-account.png`

### Result

| Account Name | Failed Logons |
|--------------|--------------|
| ANGIE_PC$ | 26 |
| angel | 15 |
| - | 11 |

The local account **angel** generated multiple failed authentication attempts during testing activities.

---

## Step 4 – Count Failed Logons by Source Address

Aggregated failed logon events by source IP address.

### SPL Query

```spl
index=main EventCode=4625
| stats count by Source_Network_Address
| sort - count
```

### Evidence

`failed-logons-by-source-ip.png`

### Result

| Source Address | Failed Logons |
|---------------|--------------|
| 127.0.0.1 | 15 |
| - | 11 |

Most failed authentication attempts originated from **127.0.0.1 (localhost)**, indicating locally generated logon activity.

---

## Analysis

Failed logon events are commonly monitored by SOC analysts because they may indicate:

- Brute-force attacks
- Password spraying attempts
- Unauthorized access attempts
- Credential misuse
- User authentication failures

In this lab, the failed authentication events were generated through controlled testing and successfully identified within Splunk.

---

## Key Takeaways

- Identified failed authentication events using Security Event ID 4625.
- Used SPL queries to investigate authentication failures.
- Aggregated failed logons by account and source IP address.
- Verified locally generated failed authentication attempts.
- Practiced a basic SOC investigation workflow using Splunk.

