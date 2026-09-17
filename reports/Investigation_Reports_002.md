SOC Investigation Report
DATE: 07-09-2026
Analyst: Mohamed Roshiq K
Severity: High
Source: attack_simulation.log
Summary: Log analysis revealed multiple login attempts and data manipulation. The attacker performed port scanning before a brute-force attack. Obtained key files, transferred files, obtaining root access.

Findings:
Finding 1 – Port scan (Reconnaissance)
  •	Source IP: 203.45.67.89 (External)
  •	Time: 08:00:01
  •	Action: Scanned 5 internal IPs
  •	Assessment: Attacker mapping the network before launching an attack.
  
Finding 2 – Brute force + Full system compromise (Critical)
  •	Source IP: 203.45.67.89 (External)
  •	Target: admin account
  •	Failed attempts: 7 in 90 seconds
  •	Successful login: 09:15:22
  •	Post-access actions:
    o	Read /etc/passwd and /etc/shadow (credential harvesting)
    o	Deleted /var/log/auth.log twice
    o	Escalated Privileges to root 
    o	Transferred 524MB to 185.23.44.10
  •	Assessment: Complete cyber kill chain executed. Full system compromise. Severity: Critical
  
Findings 3 – Insider Threat
  •	Source IP: 192.168.1.108
  •	Files accessed: salary.xlsx, contracts.pdf, employees.xlsx
  •	Time between access and transfer: 90 seconds
  •	Transfer destination: 185.23.44.10
  •	Assessment: Same external destination as admin attacker. Coordinated attack or compromised account.
  
Findings 4 – Lateral Movement 
  •	John’s registered IP: 192.168.1.102
  •	Suspicious IP: 192.168.1.108 (Sarah’s machine)
  •	Assessment: John’s credentials used from sarah’s device. Possible lateral movement or shared credentials

Findings 5 – After-hours access 
  •	Login time: 23:45
  •	Action: Accessed salary.xlsx, transferred 2MB to 8.8.8.8
  •	Assessment: After-hours login is suspicious. Transfer to the Google DNS server suggests a DNS exfiltration technique.
  
Recommended Actions:
  1.	Block 203.45.67.89 at the firewall immediately
  2.	Block 185.23.44.10 
  3.	Reset admin, sarah, john, mike passwords immediately
  4.	Restore deleted auth logs from backup
  5.	Audit all actions taken by the admin account after 09:15
  6.	Investigate Sarah’s account – insider threat or compromised
  7.	Implement account lockout after 3 failed attempts
  8.	Enable after-hours login alerts in SIEM
  

