DVWA Penetration Testing Lab

This repository contains a penetration testing walkthrough of **DVWA (Damn Vulnerable Web Application)**.  
The project demonstrates practical exploitation techniques commonly used in web application security assessments.  
It is intended **for educational and portfolio purposes only**.

 Overview
DVWA is a deliberately insecure PHP/MySQL web application designed to help security professionals test their skills and tools.  
This lab demonstrates step-by-step exploitation of common vulnerabilities and provides mitigation recommendations.

 Tools & Environment:
 
Operating System: Kali Linux  
Target Application: DVWA (Damn Vulnerable Web Application)  
Tools Used:
 nmap (network scanning)  
gobuster (directory brute forcing)  
hydra  (brute force attack)  
curl (manual requests)  
netcat  (reverse shell listener)  
python3 (shell upgrade)  

Exploitation Steps
1. Information Gathering**  
   - Port scanning with `nmap`  
   - Service enumeration
  
   - Authentication Bypass Attempts
   - 
   - Default credentials test  
   - SQL Injection (`' OR '1'='1 --`)
  
   - 
Brute Force Attack
   - Used hydra to brute force admin credentials  

Directory Enumeration

   - Used `gobuster` to find hidden directories  

Command Execution Vulnerability

   - Exploited to read `/etc/passwd`  

Reverse Shell
   - Payload executed to gain shell access  
   - Upgraded shell using Python  

Privilege Escalation

   - Converted limited shell into a fully interactive bash shell
===============================================================================================================================
Learning Outcome
This project demonstrates how attackers exploit weak web applications and emphasizes the importance of implementing proper **security controls**.  
It is a hands-on showcase of penetration testing methodology for my **cybersecurity portfolio**

=====================================================================================================
**Disclaimer:**  
This project is for **educational purposes only**.  




((STEP BY STEP GUIDE ARE PROVIDED BELOW IN THE PDF FILE ))


[penetration_testing_DVWA_edited.docx](https://github.com/user-attachments/files/21940049/penetration_testing_DVWA_edited.docx)




