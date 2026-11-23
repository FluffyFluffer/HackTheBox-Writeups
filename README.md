# 🧪 HackTheBox — Writeups

![Platform](https://img.shields.io/badge/HackTheBox-Writeups-9FEF00?style=flat-square&logo=hackthebox&logoColor=black)
![Machines](https://img.shields.io/badge/Machines-7-blue?style=flat-square)
![Focus](https://img.shields.io/badge/Focus-Web%20%26%20AD%20Exploitation-informational?style=flat-square)

Personal HackTheBox writeups — part **portfolio**, part **study notes for CWEE prep**.
Each writeup is organized around the machine's original tasks, focusing on the *attack chain* and the tools used.

---

## 📂 Machines

| Machine | Platform | OS | Key topics | Status |
|---|---|:---:|---|:---:|
| [**Archetype**](./Archetype/Writeup.md) | Starting Point | 🪟 Windows | SMB, MSSQL `xp_cmdshell`, Impacket, PS history, WinRM | ✅ |
| [**Oopsie**](./Oopsie/Writeup.md) | Starting Point | 🐧 Linux | IDOR, cookie tampering, file upload, SUID / `$PATH` hijack | ✅ |
| [**Unified**](./Unified/Writeup.md) | Starting Point | 🐧 Linux | Log4Shell (CVE-2021-44228), JNDI/LDAP, MongoDB | ✅ |
| [**BountyHunter**](./BountyHunter/Writeup.md) | Retired · Easy | 🐧 Linux | XXE, PHP filters, credential reuse, `eval()` injection | ✅ |
| [**Friendzone**](./Friendzone/Writeup.md) | Retired · Easy | 🐧 Linux | DNS zone transfer, SMB, LFI → RCE, credential reuse, Python library hijack | ✅ |
| [**Cronos**](./Cronos/Writeup.md) | Retired · Medium | 🐧 Linux | DNS zone transfer, vhost enum, SQLi, command injection, Laravel cron privesc | ✅ |
| [**Shibboleth**](./Shibboleth/Writeup.md) | Retired · Medium | 🐧 Linux | vhost enum, IPMI RAKP hash dump, Zabbix RCE, password reuse, MariaDB `wsrep_provider` (CVE-2021-27928) | ✅ |

> ✅ completed

---

## 🛠️ Tools used

`nmap` · `smbclient` · `impacket` · `evil-winrm` · `gobuster` / `ffuf` · `burp suite` · `cyberchef`
`msfvenom` · `metasploit` · `john` · `marshalsec` / `rogue-jndi` · `tcpdump` · `mongo` · `mysql` / `mariadb` · `smbmap` · `dig` · `sqlmap` · `gcc` · `linpeas`

---

## 📑 Writeup structure

Every writeup follows the same layout:

- **TL;DR** — the attack chain in a few bullet points
- **Tags** — techniques and vulnerabilities
- **Walkthrough** — the machine's tasks + commands
- **Flags** — summary

---

<sub>⚠️ For educational purposes. All machines are from <a href="https://www.hackthebox.com/">HackTheBox</a> and solved in a legal, lab environment.</sub>
