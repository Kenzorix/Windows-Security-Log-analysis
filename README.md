# Windows-Security-Log-analysis
# Windows Security  Event-Log Analysis Using Splunk

## 📌 Project Overview

This project documents a hands-on Security Operations Center (SOC) investigation involving Windows Security Event Logs and Splunk.

The objective was to ingest Windows authentication logs into Splunk, investigate failed authentication activity, identify useful investigation fields, and interpret the results from a security monitoring perspective.

This project demonstrates a practical workflow used by SOC analysts when investigating authentication-related security events.
## 🎯 Objectives

The main objectives of this investigation were to:

- Collect Windows Security Event Logs
- Export and prepare Windows log data for analysis
- Ingest the log data into Splunk
- Search and filter Windows security events
- Investigate failed authentication attempts
- Identify relevant fields for further investigation
- Analyze source network information
- Document observations and findings
- Practice basic SOC investigation methodology
## 🧪 Lab Environment

| Component | Purpose |
|---|---|
| Windows 10 | Source of Windows Security Event Logs |
| Ubuntu | Splunk environment |
| Splunk Enterprise | SIEM / log analysis platform |
| CSV | Exported Windows log data |
| Windows Security Logs | Primary investigation data |

## 🔄 Data Collection & Ingestion

Windows Security Event Logs were exported into CSV format and transferred from the Windows environment to the Ubuntu Splunk environment.

The log data was then ingested into Splunk for analysis.

### Investigation Workflow
Windows Security Logs
        ↓
CSV Export
        ↓
Transfer to Ubuntu
        ↓
Splunk Ingestion
        ↓
Search & Filtering
        ↓
Event Investigation
        ↓
Findings & Documentation
🔎 Investigation

Event ID 4625 — Failed Logon

The primary focus of this investigation was Windows Event ID 4625, which represents a failed logon attempt.

The following Splunk query was used to identify the total number of Event ID 4625 events:

index=main EventCode=4625
| stats count

Result

The search returned:

65 failed logon events

This established the initial volume of failed authentication activity within the available dataset.

📊 Investigating Authentication Activity

After identifying the failed logon events, additional fields were examined to understand the activity in greater detail.

Fields of interest included:

_time

EventCode

host

user

Source Network Address

Source IP, where available


The purpose of examining these fields was to determine:

Which account was involved

When the authentication failures occurred

Which system generated the events

Where the authentication attempts originated

Whether repeated failures were present
🌐 Source Network Address Analysis

The Source Network Address field was examined as part of the investigation.

The address:

127.0.0.1

appeared repeatedly in the results.

127.0.0.1 is the IPv4 loopback address, meaning the traffic originated from the local system rather than a remote network host.

Analyst Interpretation

The presence of 127.0.0.1 alone does not establish malicious activity.

Additional context would be required before classifying the activity as suspicious, including:

Account involved

Authentication type

Failure reason

Timestamp correlation

Related Windows events

Process information

Other network indicators


This demonstrates an important SOC principle:

> An indicator should be investigated in context rather than automatically classified as malicious.
🧰 Splunk Investigation Queries

Count Event ID 4625

index=main EventCode=4625
| stats count

Purpose: Determine the total number of failed logon events.
Investigate Failed Logons

index=main EventCode=4625
| table _time, host, user, EventCode

Purpose: Examine individual failed authentication events and their timestamps.

Analyze Events by Host and User

index=main EventCode=4625
| stats count by host, user
| sort -count

Purpose: Identify accounts and systems associated with repeated failed logons.
🧠 Investigation Findings

The investigation identified:

65 Event ID 4625 failed logon events

Repeated authentication failures within the dataset

127.0.0.1 appearing as a Source Network Address in the observed results

Several useful fields that can be used to investigate authentication activity
The available evidence was not sufficient by itself to classify the observed activity as a confirmed attack.

Further correlation with additional Windows Security events would improve the investigation.
🚨 SOC Analyst Perspective

In a real SOC environment, repeated Event ID 4625 activity could warrant further investigation depending on the surrounding context.

An analyst would typically correlate the failed logons with:

Successful logons (Event ID 4624)

Account creation events

Account deletion events

Privilege-related events

Log clearing activity

Source addresses

Usernames

Authentication types

Event timestamps


A high number of failed authentication attempts could potentially indicate scenarios such as:

Incorrect credentials

Misconfigured applications or services

User password issues

Automated authentication attempts

Password spraying

Brute-force activity


However, these possibilities should be validated against the available evidence before reaching a final conclusion.
📸 Investigation Evidence

Screenshots from the Splunk investigation are included in this repository.

The screenshots demonstrate:

Splunk searches

Event ID 4625 investigation

Event counts

Source Network Address analysis

Log investigation workflow
🛠️ Skills Demonstrated

Through this project, I practiced:

Windows Security Event Log Analysis

SIEM Investigation

Splunk Enterprise

Splunk Search Processing Language (SPL)

Authentication Event Analysis

Failed Logon Investigation

Log Ingestion

Security Monitoring

SOC Investigation Methodology

Security Findings Documentation
📚 Key Learning Outcomes

This investigation provided practical experience with the process of turning raw security logs into actionable security information.

Key lessons included:

1. Understanding Windows authentication events


2. Searching and filtering logs with Splunk


3. Identifying relevant investigation fields


4. Investigating repeated failed authentication attempts


5. Understanding the importance of source network information


6. Avoiding premature conclusions when analyzing security events


7. Documenting investigation findings clearly
🔮 Future Improvements

Future versions of this project will include:

Correlation between Event IDs 4624 and 4625

Investigation of account-management events

Detection of suspicious authentication patterns

Splunk dashboards

Automated alerts

Time-based authentication analysis

Additional Windows Event IDs

Sysmon telemetry integration

More advanced SOC detection techniques
✅ Conclusion

This project demonstrates a practical Windows authentication log investigation using Splunk.

Starting from raw Windows Security Event Logs, the investigation progressed through log collection, ingestion, searching, event filtering, authentication analysis, source network investigation, and security-focused interpretation.

The project also demonstrates an important SOC analyst principle: security events should be investigated using context and correlation rather than isolated indicators.
👤 Author

Kennisbright

Aspiring SOC Analyst | Cybersecurity | DFIR | SIEM
