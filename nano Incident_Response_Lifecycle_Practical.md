#  Incident Response Lifecycle — SSH Brute-Force Attack Simulation

  Objective
To simulate, detect, contain, and recover from an SSH brute-force attack using a real Linux environment.  
This lab demonstrates the **complete Incident Response Lifecycle**, from detection to documentation, using standard security tools and best practices.

**Skills Demonstrated:**  
- Log Analysis & Threat Detection  
- Network Containment (Firewall Rules)  
- Threat Eradication & Malware Scanning  
- System Recovery & Service Verification  
- Hardening & Automated Defense Configuration  
- Evidence Packaging & Integrity Verification  



Step 0 — Setup (Preparing Workspace)

In this lab, we first create a dedicated workspace to organize all incident response artifacts.


COMMAND USED
mkdir -p ~/cybersecurity-Lab/Incident_Response_Lifecycle/{logs,screenshots,evidence}
cd ~/cybersecurity-Lab/Incident_Response_Lifecycle

EXPLANATION
This creates three folders (logs, screenshots, evidence) where WE WIll store every output and proof for your report.

Step 1 — Detection Phase

1) COMMAND 
journalctl -u ssh.service --no-pager | tail -n 50

EXPLANATION
We used this command to review the latest SSH service logs and identify any suspicious or unauthorized access attempts, such as repeated failed logins, unfamiliar usernames, or connections from unknown IP addresses.
This helps us to detect early signs of a brute-force attack, unauthorized login, or misconfiguration on the SSH service.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_13_52" src="https://github.com/user-attachments/assets/7d11b40f-11d9-4182-b1bf-2a029698d360" />
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_14_02" src="https://github.com/user-attachments/assets/74fc2d51-9865-4cfc-84e3-e6fff2fcd6c3" />


2) COMMAND
journalctl | grep "Failed password"

 EXPLANATION
We used this command to quickly identify all failed SSH login attempts recorded on the system.
This helps us in detecting brute-force attacks, unauthorized access attempts, or users repeatedly trying incorrect credentials.
By filtering only “Failed password” entries, we can focus on suspicious authentication failures without unrelated log noise.

SCREENSHOT 
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_14_20" src="https://github.com/user-attachments/assets/631317b1-2d2b-4ae5-934b-785007668251" />

3)COMMAND
journalctl -fu ssh.service

EXPLANATION
this command will monitor the live SSH login activity in real time and instantly detect suspicious behavior such as repeated failed logins, unauthorized access attempts, or brute-force attacks as they occur.
This real-time observation helps security analysts respond immediately to threats instead of waiting for log reviews after the fact.


Step 2 — Simulate the Attack
(We will generate logs for learning)

1)COMMAND
for i in {1..3}; do ssh -o ConnectTimeout=3 wronguser@localhost exit || true; done

EXPLANATION
We used this to safely generate failed SSH login attempts on your own machine.
These artificial failures create log entries you can use to practice detection, alerting, and evidence collection without attacking other systems.
in my case the  sshd on the target system was not listening on the default SSH port (22). 
The service was configured to listen on port 2222, so connection attempts to port 22 were immediately refused by the OS.


SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_16_15" src="https://github.com/user-attachments/assets/efbf02c0-d5c5-44c6-beae-ed740586de77" />


2) COMMAND
journalctl -u ssh.service -n 20

EXPLANATION
We used this command to confirm that the failed SSH login attempts were logged.
This command shows the most recent SSH-related log entries so you can verify that your simulation produced Failed password (or invalid user) lines.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_16_23" src="https://github.com/user-attachments/assets/47f0285f-037f-4e55-a752-ae9899d88f21" />


Step 3  Containment Phase

1)COMMAND 
ufw status verbose


EXPLANATION
To inspect the current firewall state and rule set before taking containment actions.
This confirms whether the Uncomplicated Firewall (UFW) is enabled, which ports are open/blocked, and what pre-existing rules might affect containment decisions.


2) COMMAND
sudo ufw deny from 10.0.2.15
(NOTE IN PLACE OF THIS IP USE YOURS WHICH YOU SEE ON YOUR SCREEN)

 EXPLANATION
In this step we use this command to immediately block all incoming connections from the identified attacker’s IP address.
During an incident, quick containment is critical this command  prevents the malicious host from sending any more traffic to your system. 

 
3) COMMAND
sudo ufw status numbered

 EXPLANATION
 We used this command to verify that the attacker’s IP blocking rule has been successfully added to the firewall.
This step ensures that your containment action is properly enforced and visible in the current firewall configuration.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_16_28" src="https://github.com/user-attachments/assets/b666c16e-dd0a-4529-8707-abed2c88d7a5" />


Step 4  Eradication Phase

1) COMMAND 
cat /etc/passwd | grep home

EXPLANATION
this command is used to identify all user accounts that have local home directories, which helps in spotting unauthorized or suspicious accounts possibly created during the attack.
Attackers sometimes create hidden users or backdoor accounts to maintain access — checking the /etc/passwd file helps uncover these.


2) COMMAND
sudo userdel -r suspicious_user

 EXPLANATION
This command is used to remove a malicious or unauthorized user account that may have been created by an attacker to maintain persistent access.
Eliminating such accounts ensures that the attacker can no longer log in or execute actions on the system.


(TO REMOVE THREATS AND AND CLEAN THE SYSTEM)
3) COMMAND
sudo apt install clamav -y
sudo freshclam
sudo clamscan -r /home | tee logs/clamscan.txt

EXPLANATION
To detect and remove any malware, backdoors, or infected files that may have been left behind by the attacker.
This ensures your system is completely clean and no hidden malicious files remain that could reinfect it.

SCREENSHOTS
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_16_34" src="https://github.com/user-attachments/assets/7e98c8ca-79a7-49b8-a543-6fee648f523c" />
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_16_40" src="https://github.com/user-attachments/assets/2584f97b-313a-4f75-a3c8-4fd1a08c9399" />
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_16_46" src="https://github.com/user-attachments/assets/65dc5fda-dff3-464a-9bc8-7bd2b64f370e" />



Step 5  Recovery Phase

1) COMMAND
sudo systemctl start ssh

EXPLANATION
This command is used to restore the SSH service that was previously stopped or restricted during containment.
Once the system has been verified as clean, restarting SSH allows administrators to securely reconnect and resume normal remote management.

2) COMMAND
sudo systemctl status ssh --no-pager


  EXPLANATION
  This step is used to verify that the SSH service is running correctly and that it restarted successfully after containment and cleanup.
This step ensures the service is stable, active, and functioning normally without errors before you resume remote operations.


3) COMMAND
sudo apt update && sudo apt upgrade -y

EXPALANTION
This command is used to update the entire system and apply the latest security patches after recovery.
Keeping the system up to date ensures that known vulnerabilities are fixed, reducing the risk of the same or similar attacks happening again

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_17_11" src="https://github.com/user-attachments/assets/9d9be761-1274-4da3-a132-13d5acc7e521" />
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_17_04" src="https://github.com/user-attachments/assets/91380c22-f845-4cbc-8019-ce192ac52ea4" />



Step 6  Lessons Learned & Hardening
(To improve system defense)

1)COMMAND
sudo apt install fail2ban -y
sudo systemctl enable --now fail2ban

EXPLANATION
this command are used to enhance system security by automatically banning IP addresses that generate multiple failed login attempts.
This proactive measure helps prevent brute-force attacks and protects your SSH service from repeated unauthorized access attempts 


2) COMMAND
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
sudo nano /etc/ssh/sshd_config

EXPLANATION
These commands are used to strengthen  SSH security configuration by disabling unsafe settings and restricting remote access only to trusted users.
This step helps prevent unauthorized logins, brute-force attacks, and privilege misuse through the SSH service.


Step 7 Evidence & Documentation
(To save and verify your results)

COMMANDS
tar -czvf evidence_package.tar.gz logs screenshots evidence
sha256sum evidence_package.tar.gz > evidence_package.sha256
ls -la


EXPLANATION
These commands are used to collect, preserve, and verify all investigation artifacts  ensuring the integrity and authenticity of your work.
This step packages every piece of evidence (logs, screenshots, and analysis files) so that your findings can be safely shared, archived, or submitted as proof in a professional investigation report.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_22_58" src="https://github.com/user-attachments/assets/2f45c133-540c-4173-948e-43349a00f54a" />




 ALL SCREENSHOTS
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_13_52" src="https://github.com/user-attachments/assets/7d11b40f-11d9-4182-b1bf-2a029698d360" />
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_14_02" src="https://github.com/user-attachments/assets/74fc2d51-9865-4cfc-84e3-e6fff2fcd6c3" />

<img width="1366" height="662" alt="Screenshot_2025-11-01_22_14_20" src="https://github.com/user-attachments/assets/631317b1-2d2b-4ae5-934b-785007668251" />

<img width="1366" height="662" alt="Screenshot_2025-11-01_22_16_15" src="https://github.com/user-attachments/assets/efbf02c0-d5c5-44c6-beae-ed740586de77" />

<img width="1366" height="662" alt="Screenshot_2025-11-01_22_16_23" src="https://github.com/user-attachments/assets/47f0285f-037f-4e55-a752-ae9899d88f21" />

<img width="1366" height="662" alt="Screenshot_2025-11-01_22_16_28" src="https://github.com/user-attachments/assets/b666c16e-dd0a-4529-8707-abed2c88d7a5" />

<img width="1366" height="662" alt="Screenshot_2025-11-01_22_16_34" src="https://github.com/user-attachments/assets/7e98c8ca-79a7-49b8-a543-6fee648f523c" />
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_16_40" src="https://github.com/user-attachments/assets/2584f97b-313a-4f75-a3c8-4fd1a08c9399" />
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_16_46" src="https://github.com/user-attachments/assets/65dc5fda-dff3-464a-9bc8-7bd2b64f370e" />

<img width="1366" height="662" alt="Screenshot_2025-11-01_22_17_11" src="https://github.com/user-attachments/assets/9d9be761-1274-4da3-a132-13d5acc7e521" />
<img width="1366" height="662" alt="Screenshot_2025-11-01_22_17_04" src="https://github.com/user-attachments/assets/91380c22-f845-4cbc-8019-ce192ac52ea4" />

 <img width="1366" height="662" alt="Screenshot_2025-11-01_22_22_58" src="https://github.com/user-attachments/assets/2f45c133-540c-4173-948e-43349a00f54a" />



🏁 Final Summary  Incident Response Lifecycle Practical

This lab demonstrated the complete incident response process on a Linux system under simulated SSH brute-force attack conditions.
Each phase — from Detection to Documentation — was executed using real administrative tools like journalctl, ufw, clamav, and fail2ban.

Key Learnings:

How to detect and monitor failed SSH authentication attempts.

How to contain threats by isolating attacker IPs using ufw.

How to perform system cleanup, malware scanning, and user verification.

How to restore services securely after containment.

How to document, verify, and archive evidence with integrity verification.

Outcome:
A secure, hardened Linux environment was restored, with automated defenses (fail2ban, patched packages) and documented proof of all actions.
This exercise reinforces core SOC and Incident Response skills  detection, containment, eradication, recovery, and documentation — following industry best practices.


🧾 Author

kaleem ullah albaloshi
Cybersecurity Student | SOC & Incident Response Enthusiast
Practical project for GitHub cybersecurity portfolio.








 
