phishing Email Analysis

# 🧩 Phishing Email Analysis (Mock / Safe Lab)
## 🎯 Objective
## 🧰 Tools Used
## 🧠 Steps & Explanation
### Step 1 — View Email Headers
### Step 2 — Extract Links
...
## 🧾 Summary


## 🧩 Project Overview
This project demonstrates practical cybersecurity skills in:
- Phishing email analysis and URL forensics
- Ransomware detection, containment, and recovery
- DDoS simulation and mitigation using firewall rules
- Defensive system hardening and SSH security configuration

All experiments were conducted in a controlled lab environment (Kali Linux, Ubuntu VM) using safe mock data.


## 🧰 Tools & Technologies Used
- Linux CLI utilities (grep, sed, dig, whois, curl, strings, tar, find)
- ClamAV antivirus
- UFW (Uncomplicated Firewall)
- Fail2Ban intrusion prevention
- SSH (key-based authentication)

### ✅ Key Learnings
- Identified phishing URLs safely using grep and sed.
- Understood how to inspect WHOIS and DMARC for email authenticity.
- Learned safe attachment inspection methods (hashing, file type detection).



for this practical we created a fake email to perform our lab on that email we created that email for our own practice and we apply the all methods so safely investiget the phishing email.the same processes whill apply for all phishing email if anyone recives any email they can go with the same method to investigate the email for their safety.

suspect.eml Phishing Email Analysis (Mock / Safe Sample)

Introduction

This repository contains suspect.eml, a deliberately crafted mock email message created for training and demonstration purposes.
It looks and behaves like a real phishing message but contains no live malicious payloads or working exploit links — it is safe to inspect and analyze.

Use this sample to practice common email-forensics workflows, demonstrate investigation steps in a portfolio, or teach others how to spot phishing indicators without ever exposing anyone to real threats.


Why this exercise matters

Phishing remains one of the most effective attack vectors. Security professionals must be able to:

Identify suspicious headers and senders

Spot mismatched or obfuscated URLs

Recognize social-engineering cues in message text

Safely inspect attachments and embedded content

This mock file gives you a realistic but safe artifact to build those skills and show off your analysis process.

What’s inside suspect.eml

The file is a safe mock. It contains realistic-looking email headers, body text, placeholder URLs, and a fake attachment marker no executable attachments, no live links, and no malicious code.

Typical items included (for learning purposes only):

Standard email headers (From, To, Subject, Received, Message-ID) with subtle anomalies to analyze

An attention-grabbing social-engineering message body (urgent language, call-to-action)

Placeholder URLs that look real but are non-functional (for spotting mismatches)

A fake attachment marker to practice safe attachment handling procedures


you can also apply the same method to create the same email only for performing the lab

step 1
the first step is to create the phishing email.type so run the following commands to create it safely 

COMMANDS

cat > suspect.eml <<'EOF'
From: "Support" <support@google-secure-example.com>
To: kaleem@example.com
Subject: Urgent: Verify Your Account Now
Return-Path: <bounce@phishingsrv.example>
Received: from unknown (HELO phish.example) (192.0.2.55)
Authentication-Results: mx.example.com; dkim=none; spf=neutral
DKIM-Signature: v=1; a=rsa-sha256; d=example.com; s=default;
Reply-To: support-security@example-login.com
Date: Tue, 28 Oct 2025 08:00:00 +0000
MIME-Version: 1.0
Content-Type: multipart/mixed; boundary="abc123"

--abc123
Content-Type: text/plain; charset="UTF-8"
Hello,

Please verify your account immediately by visiting:
https://secure-login-example.com/verify?user=kaleem

Or click this alternate:
http://phishingsrv.example/redirect

Thank you,
Support Team

--abc123
Content-Disposition: attachment; filename="invoice.pdf"
Content-Type: application/octet-stream
[SIMULATED-BINARY-DATA: DO NOT EXECUTE]
--abc123--
EOF

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_08_39" src="https://github.com/user-attachments/assets/f8f8ce95-e05b-4a6b-92a8-717ed5fd8f9c" />

EXPLANATION
It Creates a file suspect.eml in the current folder with sample headers, body, URLs, and a fake attachment marker.
Reason:
Beacuse we  don’t have a real .eml file to analyze, so this safe mock file lets us to practice the exact analysis commands without risk.
A suspect.eml will be created; no visible output if successful (you return to the prompt).


A — PHISHING (analysis)

Command Used
sed -n '1,120p' suspect.eml

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_08_53" src="https://github.com/user-attachments/assets/c2fa4a16-dc71-4f43-afee-ed0fcf323ff6" />

EXPLANATION

This command will display the first 120 lines of the phishing email file to safely view key headers and part of the body.
this is used to quickly inspect sender details, subject lines, and mail paths without opening the email in a risky viewer.a safe way to spot forged addresses, fake domains, and suspicious routing during phishing analysis.

STEP 2

COMMAND USED
grep -E '^(From|To|Subject|Return-Path|Received|DKIM-Signature|Authentication-Results|Reply-To):' suspect.eml

EXPLANATION 
it filts only the key email headers the sender, receiver, subject, and authentication details  from the phishing email file.
and helps helps analysts focus on crucial routing and verification headers (SPF, DKIM, Received chains) to detect spoofing, forged domains, or unauthorized senders quickly.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_08_59" src="https://github.com/user-attachments/assets/cea6e728-bca3-4933-aa9e-e89c3e28ec8f" />

STEP 3

COMMAND USED
grep -Eo 'https?://[^ >]+' suspect.eml | sort -u > suspect_urls.txt

EXPLANATION
This command used to Scan the email and extracts every HTTP/HTTPS link, saving all unique URLs into suspect_urls.txt.
Allows safe collection of all embedded links for further inspection helping identify malicious or phishing URLs without ever clicking them.


STEP 4
COMMAND USED 
head -n1 suspect_urls.txt

EXPLANATION 
this command will displays the hidden URL from the list for focused, safe analysis.
Lets you inspect one suspicious link at a time, reducing risk and preventing accidental access to multiple potentially malicious domains.

STEP 5
COMMAND USED
first_url=$(head -n1 suspect_urls.txt); echo "$first_url"

EXPLANATION 
This command is used to capture the first suspicious URL from the extracted list and stores it in a variable named first_url.
It then displays the stored link on the screen, ensuring you know exactly which URL you’ll be investigating next.
By saving the URL into a variable, analysts can reuse it safely and efficiently in multiple commands without the risk of retyping errors. 
It keeps the workflow clean, organized, and professional
a smart move when handling potentially malicious links during phishing investigations.

STEP 6
COMMAND USED
domain=$(echo "$first_url" | sed -E 's#https?://([^/]+).*#\1#'); echo "$domain"

Explanation:
This command will isolate and displays the domain name from the captured phishing URL  for example, extracting phish.example.com from a full link. 
It helps narrow your focus to the core source of the suspicious activity.
Analyzing the domain itself is a crucial step in phishing investigations. Through WHOIS and DNS lookups, analysts can uncover details like domain age, registration data, and ownership
strong clues that often expose newly created or suspicious domains used in cyberattacks.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_08_59" src="https://github.com/user-attachments/assets/fe1c4954-1a07-4ced-afbd-0b397442981a" />

STEP 7
COMMAND USED
whois "$domain" | sed -n '1,20p'

Explanation
We used this command perform a WHOIS lookup on the extracted domain and displays the first 20 lines of its registration record. These lines often reveal the registrant’s name, organization, creation date, and registrar details, which help trace the domain’s origin.
Phishing domains are often newly registered, short-lived, or use hidden identities to avoid detection. By reviewing WHOIS data, analysts can quickly spot red flags such as recent creation dates, suspicious registrars, or anonymized ownership — strong indicators of a potentially malicious site.

STEP 8
dig +short TXT "_dmarc.$domain" || true

Explanation:
This command checks the domain’s DMARC (Domain-based Message Authentication, Reporting & Conformance) record by querying its DNS TXT entry. DMARC records show how the domain handles email authentication, helping verify whether the sender’s domain is properly protected.
Legitimate organizations usually have strong DMARC policies to prevent email spoofing. A missing or weak DMARC record is a major red flag, often indicating that attackers may be impersonating the domain to deliver phishing emails. Checking this record helps identify whether the domain follows proper email security practices.


STEP 9
COMMAND USED
sha256sum attachment.bin

Explanation
This command generates a SHA-256 cryptographic hash (a unique digital fingerprint) of the suspicious email attachment. 
It allows analysts to identify and reference the file safely without opening or executing it a vital step in secure malware analysis.
By sharing or checking this hash value,We can compare it against threat intelligence databases to see if the file matches known malware samples.
It’s a safe, professional, and evidence-based method to confirm whether an attachment is malicious — without risking system infection.

STEP 10
COMMAND USED
file attachment.bin

EXPLANATION
This command safely identifies the file type and format of the suspicious attachment without opening or executing it.
It examines the file’s internal signature, not just its extension, revealing whether it’s a PDF, executable, Word document, ZIP archive, or any other format.
here we used this command to Knowing the true nature of the file helps analysts choose the right and safest investigation path.
For example, a .pdf may lead to embedded JavaScript exploits, while a .exe could indicate a trojan.
This step ensures smart, secure, and controlled malware analysis before deeper inspection. 

STEP 11
COMMAND USED
strings -a -n 8 attachment.bin | sed -n '1,80p'

EXPLANATION
This command runs strings to extract readable text sequences (minimum 8 characters) from the binary attachment, then shows the first 80 lines of those results. 
It surfaces any human-readable content buried inside the file—like URLs, file paths, commands, or error messages—without executing the file.
Inspecting embedded strings reveals hidden clues (links, IPs, registry keys, suspicious commands) that help classify the sample and plan safe next steps. 
It’s a low-risk, high-value technique you get intelligence from the file while keeping your environment protected.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_09_04" src="https://github.com/user-attachments/assets/b983f451-f357-464a-a8d4-808e1751c4e1" />

STEP 12
COMMAND USED
curl -I --max-time 10 --silent "$first_url" || echo "curl failed or timed out"

EXPLANATION
This command quietly requests only the HTTP headers from the suspicious URL, with a 10-second timeout.
It shows how the server responds (like redirects, security headers, or errors)  all without actually visiting or downloading the web page.
Analyzing just the headers helps identify malicious redirects, fake login pages, or spoofed servers while staying completely safe.
It’s a smart, low-risk way to gather intelligence about phishing links in a controlled lab.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_09_04" src="https://github.com/user-attachments/assets/b983f451-f357-464a-a8d4-808e1751c4e1" />
NOTE
(here in our case it showing failed beacuse we created this email just for testing so it didnt contain any http headers)

PART 2 
PART 2. STEP 1

B — RANSOMWARE (detection, quarantine & backups)

in this part we will identify suspicious file activity and protecting important data.

COMMAND USED
sudo find /home -type f -mtime -2 -printf '%TY-%Tm-%Td %TH:%TM %p\n' | sort -r | sed -n '1,40p'

EXPLANATION
Scans your /home directory for files modified in the last 2 days, listing the most recent 40 changes. This helps spot unusual file activity.
Ransomware rapidly alters or encrypts files  detecting sudden mass changes can be an early warning sign of an active attack.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_09_11" src="https://github.com/user-attachments/assets/370d5d9d-23ea-4e1b-baa6-5a61948f5124" />

STEP 2

COMMOND USED

sudo find /home -type f -name '*.locked' -print | sed -n '1,40p'

Explanation:
this command will scans the /home directory for any files ending with “.locked”, a common sign of encryption during ransomware attacks.
Ransomware often appends unique extensions to encrypted files so by using these command which will be detecting these early helps confirm infection and trigger immediate containment action

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_09_11" src="https://github.com/user-attachments/assets/4d6e697b-d3a1-4380-9125-a894341c1248" />

STEP 3
COMMAND USED 
file suspicious_binary

EXPLANATION
Identifies the type and structure of a suspicious file without running it. showing if it’s an executable, archive, or script.
Knowing the file type helps determine how dangerous it might be and guides safe analysis or quarantine steps before deeper inspection.
IdentifY the file type helps decide safe analysis steps and prevents accidental execution of potentially malicious code.

STEP 4
COMMAND USED 
sha256sum suspicious_binary


EXPLANATION
It will generates a unique SHA-256 hash (digital fingerprint) of the suspicious binary, allowing us to secure identification and tracking.
than this hash can be safely shared with threat intelligence platforms to check if the file is known malware no need to upload or expose the actual sample.

STEP 5
COMMAND USED
mkdir -p ~/quarantine && sudo mv suspicious_binary ~/quarantine/ && sudo chmod 000 ~/quarantine/suspicious_binary

EXPLANATION
This command will creates a secure quarantine folder, moves the suspicious file into it, and locks all permissions so it can’t be opened or executed.
after running this command it will creates a secure quarantine folder, moves the suspicious file into it, and locks all permissions so it can’t be opened or executed.
This isolates the potential ransomware safely  preventing accidental execution while keeping the sample intact for forensic analysis.


step 6
COMMAND USED
sudo apt update && sudo apt install -y clamav

EXPLANATION
This commands will updates your system’s package list and installs ClamAV, a trusted open-source antivirus scanner for Linux.
we used this command because ClamAV allows safe, signature-based detection of known ransomware and malware samples — ideal for quick, non-destructive local scans.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_09_18" src="https://github.com/user-attachments/assets/2ccb22fb-2559-46c1-9e9d-eda138c6db61" />

STEP 7
COMMAND USED
sudo freshclam

This command will updates the ClamAV virus signature database to the latest version, ensuring the scanner recognizes newly discovered threats.
Regular updates keep your malware definitions current  boosting the accuracy of ransomware and virus detection during scans.

STEP 8
COMMAND USED
sudo clamscan -r --bell -i /home | sed -n '1,200p'

EXPLANATION
this command will perform  a deep recursive scan of the /home directory, alerting (with a bell sound) when infected files are found and showing only the infected results.
this will helps you detect and document ransomware or malware infections safely  focusing on confirmed malicious files without overwhelming output.

SCREENSHOTS
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_09_35" src="https://github.com/user-attachments/assets/7ae9cfd6-4d17-41a7-89e6-dc1849f5e47e" />


STEP 9
COMMAND USED
sudo tar -cvpzf /backup/home_snapshot_$(date +%F).tar.gz --exclude=/backup /home/kaleem | sed -n '1,20p'

EXPLANATION
This will creates a compressed, timestamped backup of your home directory and stores it safely in /backup, showing only the first few lines of progress.
Regular offline backups are the strongest protection against ransomware  they let you restore clean data even after an attack or encryption event.

step 10
COMMAND USED
 sha256sum /backup/home_snapshot_$(date +%F).tar.gz

EXPLANATION
This will generates a SHA-256 checksum of your newly created backup file to confirm its integrity and authenticity.
so a verified hash ensures your backup is complete, untampered, and ready for secure restoration  a crucial step in any ransomware recovery plan.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_09_40" src="https://github.com/user-attachments/assets/c2825e5f-1f55-4436-bb75-5c0bf09c9e12" />

C — DDoS (Local Simulation on Loopback + Mitigation)
 PART 4 
 
STEP 1

COMMAND USED
ss -tulpn

EXPLANATION
This command will displays all active TCP and UDP sockets, along with their listening ports and associated processes.
it will also establishes a baseline view of which services are active, helping identify which ones might be impacted during a simulated flood or attack.


STEP 2

COMMAND USED
uptime

EXPLANATION
This command shows how long the system has been running along with the average CPU load over the last 1, 5, and 15 minutes
it will provides a baseline performance snapshot,  useful to compare before and after a simulated DDoS flood to assess system impact.


STEP 3
COMMAND USED
top -b -n1 | head -n 12

EXPLANATION
It runs  top in batch mode for a single update and shows the top 12 lines of output, including CPU and memory usage per process.
this command will Provides a quick snapshot of active processes and resource usage, helping identify which services or processes are being stressed or impacted during a simulated DDoS scenario.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_09_46" src="https://github.com/user-attachments/assets/5b51a11d-6c3f-46b7-a15a-086507239c54" />


STEP 4
COMMAND USED 
ping -f -c 500 127.0.0.1

EXPLANATION
After running this command it will Sends 500 rapid-fire ICMP echo requests (-f flag) to the local loopback interface (127.0.0.1), effectively flooding it for a short duration.
This command will help us to  performs a safe, contained stress test to simulate a DDoS-like flood on your own system,  useful for observing how the network stack and CPU respond under heavy packet load without harming external systems.


STEP 5
COMMAND USED
watch -n 1 "ss -s; uptime; free -h"

EXPLANATION
This command will runs a live dashboard that updates every second, showing a compact socket summary (ss -s), system load/uptime (uptime), and memory usage (free -h). 
It’s displayed in a single terminal so you can watch network, CPU load, and RAM change in real time.
we run this to alongside the local flood test to observe immediate system effects — spikes in socket counts, rising load averages, or memory pressure will appear within seconds. 
It gives analysts a fast, continuous view for correlating cause (the flood) with system impact, making your experiment and findings easy to document.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_09_52" src="https://github.com/user-attachments/assets/c0708fb6-6934-4074-8013-355b4e53803f" />

STEP 6
COMMAND used
sudo ufw allow OpenSSH

EXPLANATION
This command will allow  SSH traffic through the system firewall, ensuring port 22 remains open for secure remote connections.
It will prevents accidental lockout while tightening other firewall settings — keeping remote management accessible during security testing or rule updates.

STEP 7
COMMAND USED
sudo ufw limit OpenSSH

EXPLANATION
This will use to activates rate-limiting for SSH connections, automatically blocking IPs that attempt too many logins in a short time.
And Protects against brute-force attacks and SSH flood attempts, keeping access stable and available for genuine administrators

STEP 8
COMMAND USED
sudo iptables -A INPUT -p tcp --dport 80 -m connlimit --connlimit-above 50 -j DROP

EXPLANATION
This adds  a firewall rule that drops incoming traffic to port 80 (HTTP) if a single IP opens more than 50 simultaneous connections.
And helps to mitigate DDoS-style floods by limiting abusive clients, ensuring your web server remains responsive for legitimate users.

STEP 9
COMMAND USED
sudo apt update && sudo apt install -y fail2ban

EXPLANATION
We used this command to updates system repositories and installs Fail2Ban, a security tool that monitors log files for suspicious login attempts and automatically blocks offending IP addresses.
and provides automated protection against brute-force and repeated attack attempts, helping maintain system stability and availability.

SCREENSHOTS
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_09_57" src="https://github.com/user-attachments/assets/7ac9db1e-4625-484c-b2bb-97714974a748" />



C — DDoS (local simulation on loopback + mitigation)
In this lab we will try to Securing access, maintaining backups, and keeping the system hardened against attacks. 

PART 4 STEP 1
COMMAND USED
ssh-keygen -t ed25519 -C "kaleem_lab" -f ~/.ssh/id_ed25519 -N ''

EXPLANATION
This command will creates a new Ed25519 SSH keypair (modern, secure, and lightweight) and stores it safely in your ~/.ssh directory no passphrase required for quick lab use.
it Key-based authentication strengthens SSH security by removing password logins, significantly reducing the risk of brute-force or credential theft attacks.

SCREEENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_10_08" src="https://github.com/user-attachments/assets/961a8625-da24-4234-af2f-65ef98301dcd" />

STEP 2
COMMAND USED
mkdir -p ~/.ssh && cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys

EXPLANATION
It will creates the .ssh directory (if missing), adds your public key to authorized_keys, and applies strict permissions to keep it secure.
This enables key-based SSH login while preventing unauthorized edits or tampering  a core step in hardening remote access.

STEP 3

COMMAND USED
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak

EXPLANATION
this command will creates a safe backup of your SSH server configuration file before making any changes, preserving the original settings.
Backing up critical configs ensures you can quickly restore SSH access if a misconfiguration or lockdown accidentally blocks connections.

STEP 4

COMMAND USED
sudo sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication no/' /etc/ssh/sshd_config

EXPLANATION
after potting this command it will modifies the SSH configuration file to disable password-based logins, allowing access only through secure SSH keys.
This prevents brute-force and credential-based attacks, strengthening SSH security and ensuring only trusted key holders can connect.

STEP 5
COMMAND USED
sudo systemctl restart ssh

EXPLANATION
This restarts the SSH service to activate your new configuration settings after modifying sshd_config.
This applies the updated key-only authentication policy  always confirm key-based access works before ending your current session to avoid lockout.

STEP 6
COMMAND USED
sudo apt install -y unattended-upgrades && sudo dpkg-reconfigure --priority=low unattended-upgrades

EXPLANATION
This will installs and configures automatic security updates, allowing your system to download and apply patches silently in the background.
Here we want to keeps our system continuously protected by ensuring critical security fixes are applied promptly — minimizing vulnerability windows and exposure to exploits

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-31_09_10_13" src="https://github.com/user-attachments/assets/c676a154-85b5-4dce-8989-bfc6eb0e4df1" />

Finally after putting this command than you will see the interface which is shown below the screenshot just click on yes the changes will appear.

<img width="1366" height="662" alt="Screenshot_2025-10-31_09_04_25" src="https://github.com/user-attachments/assets/5bc13451-e51a-424d-ba1a-8dd6e1739bc0" />

## 🧾 Conclusion
This lab provided hands-on experience with real-world cybersecurity analysis and defense techniques.  
By completing it, I gained practical skills in:
- Email forensics and phishing detection  
- Early ransomware detection and data recovery  
- DDoS simulation, monitoring, and mitigation  
- System hardening and automated updates  

This demonstrates readiness for SOC, IR, or cybersecurity analyst roles.


