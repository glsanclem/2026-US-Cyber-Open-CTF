---
layout: default
title: "Your Page Title Here"
hero:
  heading: "US Cyber Open Challenge 2026 CTF Technical Writeup"
  text: "Selected CTF challenges, methodologies, and technical analysis from the Season VI: 2026 US Cyber Open, June 5 to 14, 2026."
---


# Broken Envelope

**Points:** 162
**Level:** Medium 
**Category:** Forensics, Data Recovery

---

## Description
Blue Mountain Geotechnical is a Denver-based soils and rock-mechanics consultancy. A cryptolocker affiliate passed through the firm's file shares and partly corrupted several project archives before IT lead Bela Srivastava pulled the plug. Project engineer Adalyn Proteau needs the site dispatch read before Monday's client meeting.

---

## Objective
The Cryptolocker (ransomware) corrupted files, which means the file structure is broken. The objective is to recover the site dispatch before a client meeting. 

---

## Flag Format
The flag should be in the format: SVIUSCG{This_is_a_Flag}

---

## Tools Used
CyberChef

---

## Methodology
I double clicked the zip file to unzip and found two files (dispatch file and readme file). Inside the unzipped folder, I clicked on the first file, `project_dispatch.txt` to review and analyze the document. I noticed the following string:

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/6-broken-envelope-project-dispatch.png" alt="Project Dispatch graphic" width="400">
</p>

`tag: U1ZJVVNDR3tibHVlbW91bnRhaW5femlwX2VvY2RfcmVidWlsZH0=`

The tag was a combination of uppercase letters and numbers, which I was familiar with from a previous challenge. I remember that CyberChef would be able to help decode the string. I opened CyberChef, copied and pasted the string inside the Input box and added the Base64 Operation.

**Base64** is a notation that encodes arbitrary byte data using a restricted set of symbols which can be used by humans and processed by computers.

This operation decodes data from an ASCII Base64 string back into its raw format. For example, `aGVsbG8` becomes `hello`.

As soon as I addeded the operation **Base64**, the flag appeared in the Output box:

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/6-broken-envelope-cyberchef-flag.png" alt="CyberChef flag reveal graphic" width="400">
</p>

---

## Flag
`SVIUSCG{bluemountain_zip_eocd_rebuild}`

---

## MITRE ATT&CK
<span style="color:yellow; font-style:italic;">(What was the Attacker Doing? | Reflections | Suggestions)</span>

Based on the challenge description, "A cryptolocker affiliate passed through the firm's file shares and partly corrupted several project archives...", the potential attacker behavior is ransomware impacting files and this MITRE ATT&CK came to mind:

| Field | Details |
|:--------|:---------|
| ID | T1486 |
| Tactic | Impact |
| Technique | Data Encrypted for Impact |
| Mitigation | Maintain regular offline backups, implement endpoint protection, and restrict unauthorized access to file shares to reduce the impact of ransomware attacks. |
| Detection Strategy | Monitor for unusual file encryption activity, unexpected file modifications, and the creation of ransom notes or suspicious processes accessing multiple files in a short period of time. |

Source: https://attack.mitre.org
