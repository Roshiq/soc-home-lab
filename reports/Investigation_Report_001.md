SOC Investigation Report
DATE: 06-09-2026
Analyst: Mohamed Roshiq K
Severity: Medium-High
Source: test.log
Summary:
Log analysis revealed two suspicious login patterns. An external IP attempted brute force against the root account and failed. An internal IP successfully authenticated to the admin account after three failed attempts, indicating a possible compromised credential. 
Findings:
Findings 1 – Brute Force Attempt (Blocked)	
  •	Source IP: 203.45.67.89 (External)
  •	Target account: root
  •	Failed attempts: 5 in 12 seconds
  •	Outcome: No successful login
  •	Assessment: Automated brute force attempt. Blocked. Recommend adding this IP to the firewall blocklist.
Findings 2 – Suspicious Successful Login (Critical)
  •	Source IP: 192.168.1.105
  •	Target account: admin
  •	Failed attempts: 3
  •	Outcome: 1 successful login
  •	Assessment: Credential stuffing or insider threat. Admin account accessed after repeated failures. Recommend immediate password reset, account audit and review       of all actions taken during that session.
Findings 2 – Normal Activity
  •	User: roshiq from 192.168.1.101
  •	Single successful login, no failed attempts
  •	Assessment: No suspicious activity.
Recommended actions:
  1.	Block 203.45.67.89 at the firewall immediately 
  2.	Reset admin password and audit account activity
  3.	Enable account logout after 3 attempts
  4.	Monitor 192.168.1.105 for further suspicious behaviour


