📄 RISK ASSESSMENT & MITIGATION PRACTICAL

Author: Kaleem Ullah Albaloshi

Topic: Risk Assessment & Mitigation (Global Approach)

1️⃣ Introduction

Risk assessment is a structured process used to identify, analyze, and evaluate cybersecurity risks that could affect an organization’s assets.
This approach follows ISO 27005 (Information Security Risk Management) and NIST SP 800-30 (Guide for Conducting Risk Assessments).

2️⃣ Risk Matrix Table
Asset	Threat	Vulnerability	Impact	Likelihood	Risk Level	Mitigation / Control
User Accounts	Password cracking	Weak password policy	High	High	High	Enforce MFA, strong password policy
Web Server	Remote exploitation	Unpatched software	High	Medium	High	Regular patching, vulnerability scanning
Employee Emails	Phishing attacks	Lack of awareness	High	High	High	Awareness training, phishing simulations
Database Server	Data breach	Misconfigured permissions	High	Medium	High	Role-based access control, encryption
Network Devices	DoS attack	Poor firewall configuration	Medium	Medium	Medium	Firewall tuning, DDoS protection
Endpoint Devices	Malware infection	Outdated antivirus	Medium	High	Medium	EDR tools, automatic updates
Backup Storage	Ransomware	Unsegmented backups	High	Low	Medium	Offline/offsite backups, test recovery
Cloud Accounts	Credential theft	No MFA	High	Medium	High	Enable MFA, monitor login locations
Physical Office	Unauthorized access	Weak access controls	Medium	Low	Low	CCTV, ID badges, visitor logs
Critical Applications	Insider misuse	Excessive privileges	High	Low	Medium	Principle of least privilege, audit logs
3️⃣ Risk Evaluation Scale
Likelihood	Description
High	Occurs frequently or easily exploitable
Medium	Possible under certain conditions
Low	Rare or difficult to exploit
Impact	Description
High	Major financial, reputational, or operational damage
Medium	Moderate disruption or loss
Low	Minor inconvenience, easily recoverable
Risk Level	Description
High (Red)	Immediate mitigation required
Medium (Orange)	Mitigation planned with monitoring
Low (Green)	Acceptable with standard controls
4️⃣ Example: Weak Password Policy → High Risk → Mitigation

Scenario:
An organization allows employees to set short or reused passwords.

Threat: Brute-force or credential stuffing attacks

Vulnerability: Weak password policy

Asset Affected: User accounts, cloud logins

Impact: Unauthorized access to sensitive data

Likelihood: High

Risk Level: High

Mitigation:

Enforce minimum 12-character password policy

Implement MFA (multi-factor authentication)

Schedule quarterly password audits

5️⃣ Global Relevance

This risk-based approach is applicable across any country or sector, including:

Banks: protect financial transactions and customer data

Telecoms: secure network infrastructure and SIM databases

Government: protect citizen information and critical systems

Healthcare: ensure patient data confidentiality (HIPAA, GDPR)

6️⃣ Key Takeaways

Risk = Threat × Vulnerability × Impact

Not all risks can be eliminated — but they can be mitigated or transferred

Regular risk reassessment keeps controls effective

Documenting risk shows compliance with ISO, NIST, or local standards
