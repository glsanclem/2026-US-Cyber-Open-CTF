---
layout: default
title: "Your Page Title Here"
hero:
  heading: "2025 Target + WiCyS Cyber Defense Challenge CTF Write-Ups"
  text: "This page showcases my participation in the 2025 Target Cyber Defense CTF Challenge hosted by WiCyS, which ran from July 1 through August 14, 2025."
---


# D8. Shadow Commit

**Points:** 100  
**Level:** Not as Difficult  
**Category:** Forensics Investigation (Git)

---

## Description
We've identified the piece of software that's responsible for the exfiltration, and it's one of Personalyz.io's internally developed apps. We reach out to the developer of the software and they report back that their repository was compromised. Looks like all we received was a .git directory—no source files, no README, just the version history. Somewhere in the commit log, a change was made that allowed the threat actor to use it to exfiltrate data.

---

## Objective
-	Find the commit hash where the malicious change was introduced. 
-	Obtain the malicious IPv4 address.

---

## Flag Format
###.###.###.###

---

## Tools Used
git

---

## Methodology
The zip file contained a .git directory with no actual source code, just the commit logs and object history. I unzipped the file via Terminal, opened “Terminal” and typed this command:

```bash
CopyEdit
cd ~/Desktop
unzip shadow.zip -d shadow_repo
```  

I found a list of commits which appeared to be 102 files. I needed to find the commit that introduced the malicious IPv4 address 251.91.13.37 (from the previous challenge). It wasn’t hard to find the smoking gun because the commit hash listed a bunch of numbers with lowercase letters (40-character hash) that uniquely identifies the Git commit. 

Now, I was looking for something out of the ordinary, a mix of upper-case letters with symbols and numbers. Upon skimming through the document, the following appeared:

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
