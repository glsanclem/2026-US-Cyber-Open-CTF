---
layout: default
title: "Your Page Title Here"
hero:
  heading: "US Cyber Open Challenge 2026 CTF Technical Writeup"
  text: "Selected CTF challenges, methodologies, and technical analysis from the Season VI: 2026 US Cyber Open, June 5 to 14, 2026."
---


# D6. Smuggled Away

**Points:** 500  
**Level:** More Difficult  
**Category:** Network Forensics, Data Decoding

---

## Description
Aye, ye be a smart one! Looks like we found where the stolen data is being smuggled out from. Since it looks like the pirates have already stolen some of our data, can we at least find out what they stole? If it's customer data, we may have an obligation to notify the affected parties. Use your best skills to discover and what they took.

---

## Objective
Now that we see where things are being exfiltrated, provide the credit card's expiration date, CVV, and the email of the client we saw in the PCAP.

---

## Flag Format
The flag is in the format: <CreditCardExpiration>_<CVVofCreditCard>_<email>

---

## Tools Used
PCAP file (previous challenge); Wireshark; CyberChef

---

## Methodology
This task is a continuation of the previous challenge. I looked at the pcap file from D5, WireShark, and ran it through Tshark: 

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d6-previous-pcap.png" alt="d6-previous-pcap graphic" width="400">
</p>

`tshark -r pirates.pcap -Y "ip.src == 10.75.34.13 and ip.dst == 251.91.13.37 and dns" -T fields -e dns.qry.name > extracted_queries.txt`  

Filtering the DNS query (dns.qry.name) extracted all domain names from the DNS queries in the pirates.pcap file into the domains.txt.

```bash
"C:\Program Files\Wireshark\tshark.exe" -r "C:\{Path_to}\pirates.pcap" -Y "dns.qry.name and ip.dst == {C2_IP}" -T fields -e dns.qry.name > domains.txt
```

The string of prefixes revealed lowercase letters and digits which was copied and pasted into CyberChef in the upper right quadrant. From the left side the following operations were dragged and dropped into the Recipe (To Upper case, From Base32, Gunzip) and the Output in the lower right quadrant revealed the flag answer.

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d6-cyberchef-quadrants.png" alt="d6-cyberchef-quadrants graphic" width="800">
</p>

---

## Flag
`11/30_215_alec@sbcglobal.net`  

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
