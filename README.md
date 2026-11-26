# 🧪 HackTheBox — Writeups

![Platform](https://img.shields.io/badge/HackTheBox-Writeups-9FEF00?style=flat-square&logo=hackthebox&logoColor=black)
![Machines](https://img.shields.io/badge/Machines-10-blue?style=flat-square)
![Focus](https://img.shields.io/badge/Focus-Web%20%26%20AD%20Exploitation-informational?style=flat-square)

Personal HackTheBox writeups — part **portfolio**, part **study notes for CWEE prep**.
Each writeup is organized around the machine's original tasks, focusing on the *attack chain* and the tools used.

---

## 📂 Machines

Sorted by **difficulty** first — machine lifecycle (Starting Point / Retired) is secondary.

| Machine | Difficulty | OS | Platform | Key topics |
|---|:---:|:---:|:---:|---|
| [**Archetype**](./Archetype/Writeup.md) | 🟢 Very Easy | 🪟 Windows | Starting Point | SMB, MSSQL `xp_cmdshell`, Impacket, PS history, WinRM |
| [**Oopsie**](./Oopsie/Writeup.md) | 🟢 Very Easy | 🐧 Linux | Starting Point | IDOR, cookie tampering, file upload, SUID / `$PATH` hijack |
| [**Unified**](./Unified/Writeup.md) | 🟢 Very Easy | 🐧 Linux | Starting Point | Log4Shell (CVE-2021-44228), JNDI/LDAP, MongoDB |
| [**Alert**](./Alert/Writeup.md) | 🟩 Easy | 🐧 Linux | Retired | vhost enum, stored XSS → LFI chain, htpasswd cracking, cron / writable-include privesc |
| [**Cap**](./Cap/Writeup.md) | 🟩 Easy | 🐧 Linux | Retired | IDOR, PCAP analysis, cleartext FTP creds, password reuse, Linux capabilities (`cap_setuid`) |
| [**BountyHunter**](./BountyHunter/Writeup.md) | 🟩 Easy | 🐧 Linux | Retired | XXE, PHP filters, credential reuse, `eval()` injection |
| [**Friendzone**](./Friendzone/Writeup.md) | 🟩 Easy | 🐧 Linux | Retired | DNS zone transfer, SMB, LFI → RCE, credential reuse, Python library hijack |
| [**GoodGames**](./GoodGames/Writeup.md) | 🟩 Easy | 🐧 Linux | Retired | SQLi (sqlmap), MD5 cracking, vhost enum, SSTI (Jinja2) → RCE, Docker breakout via bind mount, SUID, password reuse |
| [**Cronos**](./Cronos/Writeup.md) | 🟧 Medium | 🐧 Linux | Retired | DNS zone transfer, vhost enum, SQLi, command injection, Laravel cron privesc |
| [**Shibboleth**](./Shibboleth/Writeup.md) | 🟧 Medium | 🐧 Linux | Retired | vhost enum, IPMI RAKP hash dump, Zabbix RCE, password reuse, MariaDB `wsrep_provider` (CVE-2021-27928) |

---

## 🛠️ Tools used

`nmap` · `smbclient` · `impacket` · `evil-winrm` · `gobuster` / `ffuf` · `burp suite` · `cyberchef`
`msfvenom` · `metasploit` · `john` · `marshalsec` / `rogue-jndi` · `tcpdump` · `mongo` · `mysql` / `mariadb` · `smbmap` · `dig` · `sqlmap` · `gcc` · `linpeas` · `wireshark`

---

## 📑 Writeup structure

Every writeup follows the same layout:

- **TL;DR** — the attack chain in a few bullet points
- **Tags** — techniques and vulnerabilities
- **Walkthrough** — the machine's tasks + commands
- **Flags** — summary

---

<sub>⚠️ For educational purposes. All machines are from <a href="https://www.hackthebox.com/">HackTheBox</a> and solved in a legal, lab environment.</sub>
