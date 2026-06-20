---
layout: default
title: "Your Page Title Here"
hero:
  heading: "US Cyber Open Challenge 2026 CTF Technical Writeup"
  text: "Selected CTF challenges, methodologies, and technical analysis from the Season VI: 2026 US Cyber Open, June 5 to 14, 2026."
---


# D7. Endpoints and Exfiltration

**Points:** 100  
**Level:** Not as Difficult  
**Category:** Endpoint Forensics 

---

## Description
In D5, we identified the backup server that is the source of the transfer, and the IP address that the threat actor is possibly sending data to. Now, what software on the backup server is responsible for the exfiltration? The data files you've been given contain the outputs of shell commands run directly on the endpoint. You'll be examining the outputs of the commands "lsof", "ps", and "history."

---

## Objective
Your task is to identify the OS process, user, and software that is performing the exfiltration, and where the software came from.

---

## Flag Format
The flag should be in the format: SVIUSCG{This_is_a_Flag}

---

## Tools Used
Data file (endpoint-outpoint.zip), Text Editor

---

## Methodology
There were three text files to review: bash-history.txt, lsof.txt, and ps.txt. The findings from challenge D5 revealed the IP source (10.75.34.13); IP destination (251.91.13.37); and Protocol used (DNS) which will come in handy to complete this challenge. I opened the lsof.txt file first, clicked “edit” and “find” and typed in the search box “251.91.13.37” to see what information appeared. Fortunately, there was only one hit, and this gave us the PID (64866) and the User (backupsys) which was part of the flag answer.

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d7-lsof-txt.png" alt="lsof text graphic" width="400">
</p>

To get the executable file name or the third part of the flag, the file ps.txt was opened and a search with 64866 from the lsof.txt revealed one matching entry and the command being executed is: /usr/bin/jot.

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d7-ps-txt.png" alt="ps text graphic" width="800">
</p>

I then opened the final file, bash-history.txt, conducted a search for “/usr/bin/jot,” which revealed the following:  

```bash
sudo rm /usr/bin/jot
ln -s /usr/bin/jot /usr/.local/bin/backupy
/usr/bin/jot
```

This tells me, the sudo line deletes the authentic “/usr/bin/jot” and ln -s creates a link from “backupy” to /usr/bin/jot, which means that’s the malicious file and the answer to the final part of the flag.

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d7-bash-history.png" alt="bash history graphic" width="800">
</p>

---

## Flag
`backupsys_backupy_64866`  

---

## MITRE ATT&CK
<span style="color:yellow; font-style:italic;">(What was the Attacker Doing? | Reflections | Suggestions)</span>

This challenge required reconstructing fragmented data and decoding an XOR protected payload to recover the hidden information.

| Field | Details |
|:--------|:---------|
| ID | T1140 |
| Tactic | Defense Evasion |
| Mitigation | Review scripts and encoded files for hidden or obfuscated content. Analyze suspicious files inn controlled environment before execution. |
| Detection Strategy | Monitor for tools, scripts, or processes that decode, deobfuscate, or reconstruct encoded information from files. |

Source: https://attack.mitre.org
