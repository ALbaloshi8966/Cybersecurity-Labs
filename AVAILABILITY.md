PRACTICAL: AVAILABILITY (CIA Triad)

# 🛡️ PRACTICAL: AVAILABILITY (CIA Triad)
---

## 🎯 OBJECTIVES
- Check system availability and uptime  
- Test, monitor, and protect system availability  
- Ensure services remain online and accessible to authorized users  

---



step 1
in the first step we will check the system conectivity is our system is online or not

COMMMAND
ping google.com

Explanation:
This command sends small packets of data to Google’s server and measures how long it takes to respond.
We run this command to test availability of the network and internet connection.
If you get replies, it means your system and internet are up and available.

Step 2
in this step test Localhost service availability

ping 127.0.0.1
 
Explanation:
this command will check if your own system network interface is working properly 
We do this to ensure your local system is available to process and respond to network requests.
If it fails, local networking is down — meaning your system is not “available.”

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_12" src="https://github.com/user-attachments/assets/d0b39c2e-7941-4929-a525-daec48622a68" />

Step 3
Check Website or Server Uptime Using curl

curl -v -I https://www.google.com

curl -I fetches only the HTTP headers from the website to see if it’s responding.and -v used for verbose

We use this command to confirm web server availability. If you get a “200 OK” or “301 Moved Permanently,” that means the site is available. 
If you get “404” or “timeout,” it’s unavailable.

SCREEENSHOT

<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_29" src="https://github.com/user-attachments/assets/33b8f80f-9293-4e9a-97b4-04f2744ec21d" />

Step 4
Check System Resource Availability (CPU, Memory)
in this step we will check the CPU  of our own system wether is running well or not 

COMMAND
top

Explanation:

This opens a real-time monitor showing CPU, memory, and process usage.
We run this to ensure the system has enough resources to stay available. 
If CPU or memory is 100%, the system could hang and become unavailable.

<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_36" src="https://github.com/user-attachments/assets/ebd6773d-8e96-4ea3-afe8-ca8b36aa965d" />


Step 5
in this step we will check the disk availability 

COMMAND

df -h
Explanation:
shows all disk partitions with their used and available space in human-readable format (GB/MB).
Disk full = system crash = loss of availability.
We run this to confirm there’s enough free space to keep services running.


Step 6
Simulate a Denial-of-Service Attempt (Safe Simulation)
⚠️ Do NOT run real DoS on public servers.
We’ll just simulate using your own system safely.

COMMAND USED

ping 127.0.0.1 -l 1000 -n 20

Explanation:
This sends 20 large ping packets to your own system to see how it handles traffic load.We simulate this safely to understand how network flooding affects availability.
If the system slows down, it shows how too many requests can make a service unavailable. just like a real DDoS attack.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_42" src="https://github.com/user-attachments/assets/f8c31bb7-8c70-4444-a81b-d564beb81c6d" />

Step 7
Enable a Simple Firewall Rule (Availability Protection)

COMMAND USED 
sudo ufw enable
sudo ufw status
NOTE=run the both commands separatly

Explanation:
ufw (Uncomplicated Firewall) helps control which network traffic is allowed.
We enable firewall protection to prevent unauthorized access or DDoS attacks that could harm availability of your system.
A firewall keeps your system up and reachable for legitimate users only.


SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_45" src="https://github.com/user-attachments/assets/d5e6db5e-fce9-4d15-9ba9-71975bdaf2ad" />

Step 8
Verify Service is Still Running

COMMAND USED

systemctl status ssh

Explanation:
In this step we checked  whether the SSH service is active and running
This confirms that a critical service (like remote access) is available and operational — ensuring uptime and accessibility.

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_42" src="https://github.com/user-attachments/assets/e1d31c78-847c-47e9-9789-d5ec54b9cd1d" />

Step 9
Backup Availability Verification

COMMADN USED
ls /backup
Explanation:
Lists files in the /backup directory.
We do this to verify availability of backup data, which is essential for business continuity if one system fails, backups keep the data available.
                                (this step is optional) 

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_45" src="https://github.com/user-attachments/assets/86ac4ff4-6fe1-4bd6-8938-eca0ad75656a" />

✅ RESULT / CONCLUSION

By performing these commands, you verified and protected Availability:
Your network is available (ping)
Your services are reachable (curl, systemctl)
Your resources are healthy (top, df -h)
Your system is protected from overload (ufw, simulation)


Summary:
This practical demonstrates how to monitor and maintain system availability using Linux tools.
It verifies network connectivity, resource health, and service uptime — key principles of the CIA Triad’s “Availability” component.



SCREENSHOTS

<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_12" src="https://github.com/user-attachments/assets/d0b39c2e-7941-4929-a525-daec48622a68" />
<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_29" src="https://github.com/user-attachments/assets/33b8f80f-9293-4e9a-97b4-04f2744ec21d" />
<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_36" src="https://github.com/user-attachments/assets/ebd6773d-8e96-4ea3-afe8-ca8b36aa965d" />
<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_42" src="https://github.com/user-attachments/assets/f8c31bb7-8c70-4444-a81b-d564beb81c6d" />
<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_45" src="https://github.com/user-attachments/assets/d5e6db5e-fce9-4d15-9ba9-71975bdaf2ad" />

<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_42" src="https://github.com/user-attachments/assets/e1d31c78-847c-47e9-9789-d5ec54b9cd1d" />
<img width="1366" height="662" alt="Screenshot_2025-10-29_14_24_45" src="https://github.com/user-attachments/assets/86ac4ff4-6fe1-4bd6-8938-eca0ad75656a" />
