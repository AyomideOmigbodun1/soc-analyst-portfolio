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
---
Step | Action	| Who	| How	| Why
2.1	| Disconnect affected devices from internet	| Affected employees (guided by Office Manager)	| Turn off Wi-Fi or internet immediately	| To stop ransomware from spreading or communicating with attacker
2.2	| Temporarily isolate Google Workspace access |	Office Manager	| Force logout of all sessions and reset passwords for affected users	| To prevent account-based spread
2.3	| Pause access to shared drives (Google Drive/AWS)	| Office Manager	| Restrict permissions or temporarily disable access | To protect shared data from encryption
2.4	| Establish alternative communication channel	| Manager + Leadership |	Use WhatsApp or phone calls instead of Slack | To prevent attackers from monitoring internal communication
2.5	| Enforce immediate password resets company-wide	| Office Manager	| Require all users to reset passwords, prioritising critical accounts | To reduce risk of compromised credentials

My reasoning:
My focus here is stopping the spread as quickly as possible, even with limited tools. Since there is no central control, I relied on user actions and account-level controls. I also made a call to move communication off Slack because it could be compromised.

### PHASE 3: Eradicate
---
Step | Action	| Who	| How	| Why
3.1 | Identify likely entry point	| Office Manager + external support (if possible)	| Review email activity, phishing attempts, login logs	| To understand how the attack started
3.2	| Wipe and rebuild affected devices	| Employees (guided)	| Factory reset devices or reinstall OS	| To completely remove ransomware
3.3	| Enforce MFA across all systems	| Office Manager	| Enable MFA on AWS, CRM, payroll immediately	| To prevent further unauthorized access
3.4	| Scan unaffected devices	| Employees	| Run antivirus scans and check for unusual activity	| To ensure other devices are not silently infected

Ransom decision:
SecureNow Ltd should not rush to pay the ransom. In the UK, paying ransomware is not illegal, but it is discouraged and may have legal implications if the attacker is linked to sanctioned entities. Payment does not guarantee that files will be restored, and it may encourage further attacks. Since AWS backups exist, recovery may be possible without paying. The better approach is to focus on containment, eradication, and recovery while seeking legal and professional advice.

### PHASE 4: Recover
---
Step | Action	| Who	| How	| Why
4.1	| Restore AWS data from backups	| Office Manager + AWS support	| Use latest clean backup	| To recover critical financial data
4.2	| Rebuild and secure devices before reconnecting	| Employees	Reinstall OS and apply updates	| To ensure devices are clean
4.3	| Verify systems before reconnecting	| Office Manager	| Test access and monitor for unusual behaviour	| To avoid reinfection
4.4	| Restore business operations gradually	| Leadership + Office Manager	| Prioritise critical services like Google Workspace	| To resume operations safely
4.5	| Notify customers and regulators if needed	| Leadership	| Prepare communication based on impact assessment	| To maintain transparency and comply with regulations

Your reasoning:
I prioritised restoring AWS data first because it contains customer financial data. I also ensured systems are verified before reconnecting to avoid reinfection. Communication is delayed until there is clarity to avoid misinformation.

### PHASE 5: Lessons Learned
Root cause identified:
Most likely entry point is a phishing attack or compromised credentials due to weak MFA enforcement. The lack of MFA on AWS and other systems made unauthorized access easier.

What went well:
AWS backups being available is a strong point and may allow recovery without paying ransom. Also, early reporting by employees helped detect the issue quickly.

What failed:
-No MFA enforcement across all systems
-No security monitoring or SIEM
-No incident response plan
-Use of Slack as single communication channel
-No MDM for device control
-Untested backups for payroll system

Recommendations:
-Enforce MFA on all systems within 30 days
-Implement endpoint security and MDM solution
-Set up basic logging and monitoring (e.g., SIEM or AWS logging tools)
-Create and test an incident response plan
-Establish backup communication channels
-Regularly test backup restoration processes

Regulatory considerations:
Yes, this likely falls under UK GDPR reporting requirements if personal data is affected. SecureNow Ltd must report to the ICO within 72 hours of becoming aware of the breach. Missing the deadline can result in fines and regulatory penalties, as well as reputational damage.

### CRITICAL THINKING
Question 1:
SecureNow Ltd should immediately move communication off Slack to a secure alternative like phone calls or WhatsApp. If attackers have access, they could monitor internal discussions and adjust their attack. This matters because it could delay response or worsen the damage. Using a separate channel ensures confidentiality during the response.

Question 2:
This shows the company has a weak security posture and lacks proper incident preparedness. Relying on one person for IT and security is a major risk. They should implement a structured security function, even if small, and have external incident response support available. Having predefined roles and escalation paths is critical for future incidents.

Question 3:
I would advise the CEO to acknowledge awareness of the situation without confirming details prematurely. This avoids misinformation while showing responsibility. It is important not to disclose sensitive details until the situation is fully understood.
