


## 📚 Resources to Learn Active Directory And Mastering The CRTA EXAM 

### 1. Microsoft Official Documentation  
- [Active Directory Documentation](https://learn.microsoft.com/en-us/windows-server/identity/active-directory-domain-services)  
  *Comprehensive official guides on AD architecture, administration, and features.*

### 2. Hack The Box Academy (Free Courses)  
- [Active Directory (Full Module)](https://academy.hackthebox.com/course/preview/active-directory)  
- [Active Directory LDAP (Free)](https://academy.hackthebox.com/course/preview/active-directory-ldap)  
- [Active Directory PowerView (Free)](https://academy.hackthebox.com/course/preview/active-directory-powerview)  
- [Active Directory BloodHound (Free)](https://academy.hackthebox.com/course/preview/active-directory-bloodhound)  
  *Hands-on modules focusing on AD enumeration and attack paths.*

### 3. TryHackMe (Free Rooms)  
- [Active Directory Fundamentals](https://tryhackme.com/room/activedirectoryfundamentals)  
- [BloodHound & AD Enumeration](https://tryhackme.com/room/bloodhound)  
  *Interactive labs with step-by-step guides and practical exercises.*

### 4. YouTube Channels & Playlists  
- **IppSec** – Excellent walkthroughs of HTB AD machines  
- **John Hammond** – Tutorials on AD exploitation and post-exploitation  
- **NetworkChuck** – Basics and practical AD explanations  

### 5. Blog Tutorials  
- [Adsecurity.org](https://adsecurity.org/?cat=7) – In-depth AD attack techniques and tutorials by Sean Metcalf  
- [PentestLab](https://pentestlab.blog/category/active-directory/) – Practical AD pentesting labs and guides  

### 6. Tools Documentation  
- [PowerView (PowerShell AD Enumeration)](https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1)  
- [BloodHound](https://bloodhound.readthedocs.io/en/latest/)  

## 🧩 Windows Active Directory Machines for CRTA Practice (Easy–Medium)

Here’s a curated list of Hack The Box machines that simulate Active Directory environments. All are ranked **Easy** or **Medium**, making them ideal for CRTA preparation.

---

### 🟢 Easy

| Machine Name | Link | Focus |
|--------------|------|-------|
| 🧠 Active | [HTB – Active](https://app.hackthebox.com/machines/9) | Basic AD enumeration, password reuse, SAM database |
| 🕵️‍♂️ Escape | [HTB – Escape](https://app.hackthebox.com/machines/501) | Token impersonation, privilege abuse |
| 🧰 Escape Two | [HTB – Escape Two](https://app.hackthebox.com/machines/548) | Services abuse, lateral movement |
| 🧮 Resolute | [HTB – Resolute](https://app.hackthebox.com/machines/152) | Password reuse, enum4linux, WinRM access |

---

### 🟡 Medium

| Machine Name | Link | Focus |
|--------------|------|-------|
| 🛠 Support | [HTB – Support](https://app.hackthebox.com/machines/467) | Credential dumping, enumeration, RCE |
| 🗂 Cascade | [HTB – Cascade](https://app.hackthebox.com/machines/221) | LDAP abuse, file share traversal, escalation |
| 🧾 Manager | [HTB – Manager](https://app.hackthebox.com/machines/358) | AD CS abuse, certificate auth, escalation to Domain Admin |

---

### ✅ Recommendation

Complete them in this order for a smooth learning curve. Be sure to:
- Document each step with screenshots.
- Practice enumeration and lateral movement.
- Aim to extract secrets like `secrets.xml` on each machine.


By @blindma1den

