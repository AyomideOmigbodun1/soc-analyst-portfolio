# soc-analyst-portfolio
A practical SOC Analyst portfolio highlighting my experience in threat detection, incident investigation, and security monitoring through hands-on labs, and real-world scenarios.
# Incident Response Playbook
**Document Type:** Security Operations Center Playbook  
**Incident Type:** Ransomware Attack  
**Author:** Ayomide Omigbodun  
**Date:** 01/05/2026 
**Organisation:** SecureNow Ltd (Fictional)

---

## About Incident Response
Incident response is the process of identifying, managing, and recovering from cybersecurity incidents like breaches or malware attacks. Organisations need a formal playbook because it provides clear, step-by-step actions, roles, and communication plans, which helps teams respond quickly and consistently under pressure. In the first 60 minutes of a serious attack, a company without a plan may panic, delay decisions, and worsen the damage due to confusion. In contrast, a company with a playbook can quickly contain the threat, assign responsibilities, and reduce impact. Ultimately, having a playbook turns a chaotic reaction into a controlled and effective response.

## About This Incident Type
Ransomware is a type of malicious software that encrypts a company’s files or systems and demands payment to restore access. It typically enters an organisation through phishing emails, malicious attachments, compromised websites, or unpatched vulnerabilities. It is especially dangerous for a company like SecureNow Ltd because it can block access to critical financial data and disrupt operations. With 40,000 customers affected, the impact could include data loss, financial damage, legal consequences, and loss of customer trust.

## SecureNow Ltd - Company Profile

**Company:** SecureNow Ltd  
**Size:** 52 employees, fully remote  
**Sector:** Financial technology (fintech), UK based  
**Infrastructure:** Google Workspace, AWS (hosts customer financial data), Slack, a third party payroll system, a CRM tool  
**Devices:** Mix of company issued laptops and personal devices. No MDM (Mobile Device Management) software is in place, meaning the company cannot remotely wipe or lock devices  
**Security team:** None. The Office Manager handles IT requests. There is no SOC, no SIEM, no dedicated security monitoring  
**Backups:** AWS data is backed up daily. Google Workspace data is not backed up separately outside of Google's own retention. The payroll system vendor manages its own backups but SecureNow has never tested a restore  
**MFA:** Enabled on Google Workspace but optional, 60 percent adoption. No MFA on AWS, CRM, or payroll system  
**Incident history:** A phishing email last year led to one employee clicking a malicious link. No malware was found but the company is not certain because no forensic investigation was done. The employee was asked to change their password  
**Communication:** The company uses Slack for almost all internal communication. There is no alternative communication channel if Slack is compromised  
**Current situation:** It is 7:30am on a Tuesday. The Office Manager has just arrived at her desk and received a message from three employees saying their laptops are showing a red screen with a message demanding payment in Bitcoin to unlock their files. A fourth employee's laptop appears to be unaffected. The Office Manager calls you, the SOC analyst  

---
Step |	Action |	Who |	How	| Why
1.1	| Confirm ransomware on affected laptops	| Office Manager + affected employees	| Ask employees to send pictures/screenshots of the red screen message via phone/email	| To verify this is a real ransomware incident and not a glitch
1.2	| Identify scope of affected devices | Office Manager	| Send a message (via Slack + backup like phone calls) asking all staff to report device status without clicking anything suspicious	| To understand how widespread the attack is quickly
1.3	| Instruct affected users to stop using devices immediately	| Office Manager | Call or message affected users directly and tell them not to interact with the system	| To prevent further spread
1.4	| Check Google Workspace admin logs	| Office Manager	| Log into Google Admin Console → review login activity, suspicious access, and recent changes	| To identify unusual access or compromised accounts
1.5	| Notify leadership	| CEO/Leadership | Call or message leadership immediately	| To ensure decision-makers are aware early and can support response

**Your reasoning:** My approach here is to first confirm the incident is real and quickly understand how far it has spread without causing panic or further damage. Since there is no SIEM or SOC, I relied on available tools like user reports and Google Workspace logs. I also prioritised early communication with leadership because decisions may escalate quickly.

### Phase 2: Contain
**Objective:** Stop the ransomware from spreading to more systems and data.
Step | Action	| Who	| How	| Why
2.1	| Disconnect affected devices from internet	| Affected employees (guided by Office Manager)	| Turn off Wi-Fi or internet immediately	| To stop ransomware from spreading or communicating with attacker
2.2	| Temporarily isolate Google Workspace access |	Office Manager	| Force logout of all sessions and reset passwords for affected users	| To prevent account-based spread
2.3	| Pause access to shared drives (Google Drive/AWS)	| Office Manager	| Restrict permissions or temporarily disable access | To protect shared data from encryption
2.4	| Establish alternative communication channel	| Manager + Leadership |	Use WhatsApp or phone calls instead of Slack | To prevent attackers from monitoring internal communication
2.5	| Enforce immediate password resets company-wide	| Office Manager	| Require all users to reset passwords, prioritising critical accounts | To reduce risk of compromised credentials
