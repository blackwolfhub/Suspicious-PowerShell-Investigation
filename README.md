# Suspicious-PowerShell-Investigation
SOC investigation: analysing suspicious PowerShell activity triggered by a phishing payload.
SOC Investigation #5 — Suspicious PowerShell Activity
Alert Details
Alert Type: Suspicious PowerShell Execution
User: L.Roberts
Device: Windows 10 Laptop
Time: 11:03 AM
Detection Source: Microsoft Defender / SIEM

Command Executed:
Code  powershell.exe -nop -w hidden -enc SQBFAFgAIA...
Outcome: Execution blocked
Reason: Encoded command + hidden window = high‑risk behaviour

This is a classic malicious pattern.

What Happened? The user’s device attempted to run a Base64‑encoded PowerShell command with:
No profile (-nop)
Hidden window (-w hidden)
Encoded payload (-enc)

These flags are commonly used in:
malware
phishing payloads
credential theft
ransomware droppers
remote access trojans
The SIEM flagged it immediately.

SOC Questions
Did the user run PowerShell manually?
No — no evidence of manual execution.

Was the command launched by another process?
Yes — launched by Outlook.exe.

Was there a suspicious email?
Yes — user opened an attachment minutes before.

Did the encoded command attempt to download something?
Yes — attempted to fetch a remote script.

Did the script execute?
No — Defender blocked it.

This is a malicious phishing payload.

Log Analysis
Endpoint Logs Show:
Outlook opened attachment
PowerShell launched with encoded command
Script attempted to download remote payload
Execution blocked
No persistence created
Network Logs Show:
Attempted outbound connection to suspicious IP
Connection blocked
No data exfiltration

SIEM Shows: High‑risk PowerShell alert
No lateral movement
No privilege escalation
This confirms a blocked malware attempt.

Threat Intelligence
The IP address is linked to:
phishing campaigns
remote access trojans
credential theft
malware distribution
Risk level: High

Conclusion
This was a malicious PowerShell execution attempt triggered by a phishing email.
Payload blocked
No infection
No data stolen
No persistence
No lateral movement
The device is safe, but the user needs training.

Recommended SOC Actions
Quarantine the email
Block sender domain
Block the malicious IP
Reset user passwords
Run full antivirus scan
Notify the user
Provide phishing awareness training
Monitor device for 24 hours
Review email filtering rules

How I Investigated and Tackled the PowerShell Alert
1. Reviewed the SIEM Alert
I checked:
PowerShell flags
Encoded command
Parent process
Device details
This helped me understand the threat.

2. Analysed Endpoint Logs
I looked at:
Process tree
Script behaviour
Blocked events
This confirmed the payload was malicious.

3. Decoded the PowerShell Command
I decoded the Base64 string to see:
attempted download
remote script execution
malicious intent
This validated the threat.

4. Checked Network Logs
I verified: outbound connection attempt
IP reputation
block events
This showed the malware didn’t communicate externally.

5. Took SOC Actions
I recommended:
blocking sender
password reset
user notification
awareness training
This ensures the user and device remain safe.
