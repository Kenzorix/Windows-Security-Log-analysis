# Investigation Screenshots

## Step 1 — Detect Failed Logon Attempts

![Failed Logon Investigation](winspl1.png)

Windows Security Event ID 4625 indicates a failed logon attempt.

**Key takeaway:** Multiple failed authentication attempts were detected.
## Step 2 — Analyze Source Network Address

![Source Network Analysis](winspl2.png)

Grouping Event ID 4625 events by Source Network Address helps identify where the attempts originated.

**Key takeaway:** 127.0.0.1 accounted for 19 attempts (47.5%).
## Step 3 — Examine Detailed Failed Logons

![Detailed Failed Logons](winspl3.png)

The events were examined using account name, source IP, failure reason, logon type, authentication package, and caller process.

*Key takeaway:** The failures showed "Unknown user name or bad password.

## Step 4 — Analyze Failure Reason

![Failure Reason](winspl4.png)

The investigation focused on repeated authentication failures.

**Key takeaway:** The primary failure reason was invalid credentials.
## Step 5 — Review Timeline

![Failed Logon Timeline](winspl5.png)

The timeline was reviewed to identify repeated authentication activity and possible patterns.

**Key takeaway:** Repeated Event ID 4625 activity was observed against the Kenzorix account.
