# Project Title
 Hydra FTP Brute-Force Attack 
 

---
## Introduction

This project demonstrates a controlled brute-force attack against an intentionally vulnerable host (Metasploitable2) using **Hydra**. The exercise highlights how weak authentication (common/weak passwords) can be discovered and exploited, and it illustrates the role of network reconnaissance (Nmap) in planning attacks.
---

## 📌 Objective

- Learn practical password-cracking techniques using Hydra.  
- Assess password strength and the risks associated with weak credentials.  
- Demonstrate defensive measures such as strong password policies, account lockouts, and multi-factor authentication (MFA).

---

## ⚙️ Tools & Environment
- **Attacker OS:** Kali Linux 2025.2 (VirtualBox)  
- **Target:** Metasploitable2 (VM)  
- **Tools:** Nmap, Hydra

---

## 🚀 Setup & Methodology

1. **Lab setup**  
   - Configure Kali Linux as the attacker VM and Metasploitable2 as the target VM on an isolated virtual network.

2. **Verify connectivity**  
   ping 192.168.102

3. **Reconnaissance — Nmap scan**
    Performed a service and OS detection scan:
    
    nmap -sS -sV -O 192.168.56.102
    
    -sS : TCP SYN (stealth) scan

    -sV : Service/version detection

    -O : OS detection
    Observed output:
    
    PORT   STATE SERVICE VERSION
    20/tcp open  ftp     vsftpd 2.3.4
    
    
4. Attack — Hydra brute-force (FTP)
   Executed Hydra against the discovered FTP service using a password wordlist:
   
   hydra -l msfadmin -P /home/kali/Documents/msfpasslist.txt ftp://192.168.56.102
   
   Observed output:
   
   [21][ftp] host: 192.168.56.102   login: msfadmin   password: msfadmin


---

## 📊 Results
1. **Nmap Scan**

   A network scan was conducted using Nmap to identify open ports and services running on the target machine. The scan revealed multiple open ports and the associated services, including the FTP service, which  was later targeted with Hydra. This step provided crucial information for planning the brute-force attack.

2. **Hydra FTP Brute-Force Attack**

   Using Hydra, a brute-force attack was performed against the FTP service on the Metasploitable target machine. The attack iterated through the provided password list and successfully discovered valid     login credentials for the FTP account. This demonstrates that weak or commonly used passwords can be exploited to gain unauthorized access.
---

## 🔎 Analysis

**Nmap Scan**

Nmap provided a service inventory and probable OS fingerprint, which helped focus subsequent testing on exposed, high-risk services (FTP in this case).

Detecting service versions is useful because specific versions may have known weaknesses or be commonly targeted by automated tools.

**FTP Brute-Force (Hydra)**

The success of the brute-force attack indicates the target account used weak or commonly used passwords that were present in the wordlist.

Factors that enabled the attack:

   Absence of account lockout policies.

   No rate limiting or anomaly detection on authentication attempts.

   Use of easily guessable or commonly reused passwords.

   Security Implications & Recommendations

   Enforce strong password policies (length, complexity, and uniqueness).

   Implement account lockout or exponential backoff after repeated failed attempts.

   Deploy multi-factor authentication (MFA) where possible.

   Monitor and alert on unusual authentication patterns and brute-force indicators.

   Regularly scan and inventory services to reduce unnecessary exposed attack surface.
---

## ✅ Conclusion
This controlled exercise demonstrates that weak authentication can be exploited with readily available tools (Hydra) when reconnaissance (Nmap) reveals exposed services. The findings underscore the importance of strong password policies, authentication hardening, and proactive monitoring to mitigate brute-force risks.
---

## 🔮 Future Work

Future Work

Test countermeasures (implement lockouts, rate limiting, and MFA) and measure their effectiveness against the same wordlists and attack patterns.

Expand testing to additional services (SSH, web authentication) with responsible, permissioned scope.

Integrate log-analysis and IDS/IPS tools to detect and block automated brute-force attempts.

Use larger and more realistic password lists (including passphrases) to understand time-to-compromise under different conditions.
---

## 📚 References
Nmap documentation — nmap.org

Hydra documentation — https://github.com/vanhauser-thc/thc-hydra

Metasploitable project documentation — https://sourceforge.net/projects/metasploitable/

## Disclaimer
Disclaimer: All testing was conducted in a controlled lab environment (Metasploitable2). Unauthorized scanning, brute-force attacks, or exploitation of systems you do not own or have explicit permission to test is illegal and unethical.
