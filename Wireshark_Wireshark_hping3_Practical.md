Wireshark Packet Capture Practical

Author: Kaleem Ullah Albaloshi
Lab: Wireshark & hping3 Packet Capture and DoS Simulation
Environment: Kali Linux (attacker), Metasploitable / DVWA (target)


 Introduction

This practical demonstrates packet capture and basic network attack simulation using Wireshark and hping3 on a Kali Linux lab. The goal is to learn how to capture, analyze, and interpret ICMP packets, spoof source addresses, scan ports, and observe the effects of flooding (DoS-like) traffic against a web service (DVWA). All testing was performed in a contained lab environment on local IP addresses — do not run these techniques against unauthorized targets.

⚠️ Disclaimer

This lab was conducted in a controlled and authorized lab environment only (Kali Linux as attacker and Metasploitable/DVWA as target). The commands and techniques shown here can be disruptive and are illegal if used against systems without explicit permission. Use these skills only for learning, defensive research, or authorized penetration testing.

 Objectives

Capture network traffic with Wireshark.
Generate and analyze ICMP traffic using ping and hping3.
Observe SYN/SYN-ACK patterns and ICMP packets in Wireshark.
Perform source spoofing and randomized source tests.
Conduct basic port scans with hping3.
Demonstrate flood behavior and observe service degradation.

 Lab Environment & Prerequisites

Kali Linux (latest) with wireshark and hping3 installed.
Target VM: Metasploitable or DVWA running at 192.168.1.112 (replace with your target IP).
User has sudo privileges on Kali.

🔧 Tools Used

Wireshark — GUI packet capture and analysis.
hping3 — packet crafting and testing tool (ICMP, TCP flags, scans, floods).
ping — basic ICMP echo requests.

 Lab Steps (Detailed)
Step 1 — Start Kali & Launch Wireshark

Boot your Kali Linux VM.
Open Wireshark from Applications or run sudo wireshark in a terminal.
Select the correct network interface (e.g., eth0, enp0s3, or wlan0) and click Start to begin capturing.
Screenshot: <img width="1366" height="662" alt="Screenshot_2025-08-27_02_09_04" src="https://github.com/user-attachments/assets/b819264d-7727-4a45-b193-f04c3f246087" />


Step 2 — Generate Basic ICMP Traffic with ping

Open a new terminal in Kali.

Run:
ping 192.168.1.112

Let it run for a few seconds to generate traffic, then stop with Ctrl+C.
In Wireshark, you should see ICMP Echo (request) and Echo Reply packets between your Kali IP and the target IP.

What to look for in Wireshark: Source/Destination IPs, Type (Echo request/reply), packet timestamps.

Screenshot:<img width="1366" height="662" alt="Screenshot_2025-08-27_00_15_22" src="https://github.com/user-attachments/assets/aa70e63b-02be-499d-949a-0a750fbefeb1" />


Step 3 — Get hping3 Help & Basic Usage

In the terminal, view help to understand flags:

hping3 --help

Screenshot placeholder:<img width="1366" height="662" alt="Screenshot_2025-08-27_01_57_26" src="https://github.com/user-attachments/assets/cdaf4f02-415a-4633-8945-bfd438b6008e" />


Step 4 — Send a Small Number of ICMP Packets with Spoofed Flags

Send two ICMP packets:

sudo hping3 -1 -c 2 192.168.1.112

-1 selects ICMP mode.
-c 2 sends 2 packets.

Open Wireshark and observe the corresponding ICMP packets and source/destination behavior.

Screenshot:
<img width="1366" height="662" alt="Screenshot_2025-08-27_01_58_30" src="https://github.com/user-attachments/assets/152f5850-920a-4488-accc-c45ac8b73017" />
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_02_40" src="https://github.com/user-attachments/assets/a8a46d2b-5867-444b-baf5-4d1c2128a556" />


Step 5 — Intervaled ICMP Packets

Send ICMP packets with an interval:

sudo hping3 -1 -c 10 -i 10 192.168.1.112

-i 10 sets an interval of 10 seconds between packets.
Observe in Wireshark the spaced packets — useful to analyze intermittent traffic patterns.

Screenshot placeholder: 
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_15_56" src="https://github.com/user-attachments/assets/9a86016e-4edf-49cb-94a7-471d53a7f2af" />
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_18_12" src="https://github.com/user-attachments/assets/fae56ca0-6f72-497a-b6c6-e05fd5d0030d" />
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_18_09" src="https://github.com/user-attachments/assets/c1c8b6b7-6073-4b11-9ec9-b5e14bf8ac8b" />
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_18_07" src="https://github.com/user-attachments/assets/03df54f6-ba2d-442d-a59e-44e5b45dd018" />



Step 6 — Search & Filter in Wireshark

Use the Wireshark display filter to show ICMP packets:
icmp
To search packet contents or protocols, type in the filter box (e.g., icmp or tcp.flags.syn == 1).

icmp — shows ICMP packets.

tcp.flags.syn == 1 — shows packets with SYN flag.
tcp.flags.syn == 1 && tcp.flags.ack == 1 — SYN-ACK packets.

Screenshot
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_18_01" src="https://github.com/user-attachments/assets/dff6c0ac-d1f4-4377-a5fa-d4e2364bbd9e" />

Step 7 — Observe Service Impact: Repeated Ping & DVWA Downtime

Repeated/fast pings or crafted packets can overload the web service (DVWA) on the target.
When you increased traffic, the DVWA web page became unresponsive — this demonstrates the effect of high request volume on a service.

Screenshot 
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_20_37" src="https://github.com/user-attachments/assets/8028907f-1698-4128-a42f-d8916459e175" />
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_21_22" src="https://github.com/user-attachments/assets/8067391f-1b15-4f14-8673-55af503eedef" />
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_22_07" src="https://github.com/user-attachments/assets/b0f8873a-769f-4d60-adf2-fadb9202e2a0" />


Step 8 — Flooding Test (Use with Caution)

WARNING: The --flood option sends packets as fast as possible. Use it only on an authorized lab target.
Run a flood (only in lab):

sudo hping3 --flood -1 192.168.1.112

Monitor both the DVWA page (it should hang or become very slow) and Wireshark (packets will appear rapidly).

Screenshot 
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_24_54" src="https://github.com/user-attachments/assets/5283303e-40c5-4df0-8f93-12bb125261a3" />
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_24_59" src="https://github.com/user-attachments/assets/7d8548ab-4af7-48ed-9b64-6cd39c3d123f" />
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_25_23" src="https://github.com/user-attachments/assets/398b45b6-3ace-4f48-9f81-6491f004b4a1" />



Step 9 — Source Address Spoofing

Send ICMP with a forged source address:

sudo hping3 -1 -a 192.168.1.112 -c 3 192.168.1.1

-a <ip> sets the forged (spoofed) source address.
Here 192.168.1.112 was used as the fake source, targeting 192.168.1.1 (adjust to your environment).
In Wireshark, examine source/destination fields to see the spoofed addresses and how the target responds (or fails to respond correctly because of spoofing).

Screenshot
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_50_47" src="https://github.com/user-attachments/assets/266ab99c-e17f-4d6f-a837-89e2aa16986c" />
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_50_55" src="https://github.com/user-attachments/assets/062c0966-a2e9-4d20-adde-5cf10f5c5689" />



Step 10 — Randomized Source Addresses

Use --rand-source to randomize source IPs:

sudo hping3 -1 --rand-source -c 3 192.168.1.112

Observe in Wireshark the packets coming from randomized source addresses — useful for learning how attackers attempt to obfuscate origins.

Screenshot
<img width="1366" height="662" alt="Screenshot_2025-08-27_02_55_26" src="https://github.com/user-attachments/assets/45c9fb81-7f65-483c-9e90-990e3ce9349a" />


Step 11 — Port Scanning with hping3

Basic scan over ports 1–100:

sudo hping3 --scan 1-100 192.168.1.112

Scan with service/version probing (verbose):

sudo hping3 --scan 1-100 192.168.1.112 -Sv

TCP SYN scan on port range:

sudo hping3 --scan 1-100 192.168.1.112 -S

Observe responses in terminal and cross-reference with Wireshark to see SYN/SYN-ACK/RST patterns.

Screenshot
<img width="1366" height="662" alt="Screenshot_2025-08-27_03_09_53" src="https://github.com/user-attachments/assets/8199b853-e3d0-4e40-9151-8f8569a832c9" />
<img width="1366" height="662" alt="Screenshot_2025-08-27_03_10_56" src="https://github.com/user-attachments/assets/95577236-9bca-4053-ad27-c19d43569daa" />



Observations & Results

ICMP behavior: ping and hping3 -1 show expected Echo Request and Echo Reply packets.
SYN / SYN-ACK: TCP handshake flags were visible using Wireshark filters, confirming open and closed ports.
Flood impact: The DVWA service became unresponsive under heavy traffic — useful demonstration of DoS-like effects.
Spoofing / Rand-source: Packets with forged or randomized sources were visible; these techniques complicate attribution in real-world attacks.
Port scanning: hping3 --scan produced replies for responsive ports; cross-checked in Wireshark for packet detail.

✅ Conclusion

This lab reinforced practical skills in packet capture, traffic generation, and basic attack simulation.
You learned how to use Wireshark filters, craft ICMP packets with hping3, spoof sources, perform randomized-source tests, and scan ports.
Remember to use these techniques responsibly and only in authorized environments.
