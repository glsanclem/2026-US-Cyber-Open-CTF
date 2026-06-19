---
layout: default
title: "Your Page Title Here"
hero:
  heading: "US Cyber Open Challenge 2026 CTF Technical Writeup"
  text: "Selected CTF challenges, methodologies, and technical analysis from the Season VI: 2026 US Cyber Open, June 5 to 14, 2026."
---


# Noncesence

**Points:** 100  
**Difficulty:** Beginner
**Category:** Crypto

---

## Description
This encryption service will encrypt any plaintext you send it. It also encrypted our flag — can you recover it?

`nc challenge.ctf.uscybergames.com 55705`

---

## Objective
The objective was to recover a hidden flag encrypted by a remote server. The server provided an "encryption service" where users could send any plaintext and receive the encrypted version in return. The challenge provided the source code `server.py` to help analyze how the encryption was being handled.

---

## Flag Format
The flag format will either be: SVBRG{This_is_a_Flag} or SVIBGR{This_is_a_Flag}

---

## Tools Used
- TextEdit
- Netcat (nc)
- socat
- CyberChef

---

## Methodology


<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d8-commit-list.png" alt="d8-commit-list graphic" width="400">
</p>

I ran a terminal code (extraction command) to scan my suspicious_strings.txt file:

```bash
CopyEdit
grep -oE '[a-f0-9]{40}.*exec\(ute\(".*"\)\)' suspicious_strings.txt >  
```

I found 37 suspicious strings. Now, I was ready to decode those exec(ute(”…”)) Base64 strings. I opened the base64_matches.txt file, selected and copied everything inside that file and pasted into CyberChef inside the “Input” panel. I dragged in: From Base64 and repeated it again since it was still unreadable; then Extract IP Addresses. The output showed: 251.91.13.37 repeatedly and that was the flag.

---

## Flag
`251.91.13.37`  

---

## MITRE ATT&CK
<span style="color:yellow; font-style:italic;">(Suggested)</span>
-	**T1606 – Forge Web Credentials / Modify Software Repository:** The attacker gained access to an internal repository and modified code to allow exfiltration.
-	**T1071.001 – Application Layer Protocol:** Web Protocols: The compromised software was leveraged to send sensitive data externally over legitimate channels.
-	**T1027 – Obfuscated Files or Information:** Base64 encoding, and exec wrappers were used to hide the true nature of the malicious commit.
