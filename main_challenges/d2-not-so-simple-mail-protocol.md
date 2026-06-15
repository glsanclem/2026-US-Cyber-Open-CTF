---
layout: default
title: "Your Page Title Here"
hero:
  heading: "2025 Target + WiCyS Cyber Defense Challenge CTF Write-Ups"
  text: "This page showcases my participation in the 2025 Target Cyber Defense CTF Challenge hosted by WiCyS, which ran from July 1 through August 14, 2025."
---


# D2. Not-so-Simple Mail Protocol

**Points:** 100  
**Level:** Not as Difficult  
**Category:** Log Analysis, Forensic Analysis (E-mail)

---

## Description
A menacing extortion email was received from an unknown sender, claiming that sensitive data has been stolen from the company. The email demands a ransom and threatens to release the data if the demand is not met within 48 hours. It's clear based on the [extortion email] that the sender attempted to send this email before since the demand's due date is relative. Find the first email sent so we can estimate a lower bound on the deadline for the legal and finance teams to plan around.

---

## Objective
Use the log dashboard server, *Insightful Horizon* (https://target-osd.chals.io/) to find the first extortion email from this incident. Username: analyst | Password: *******. 

Use the email address that sent the email as the flag. If the server is not loading there are two additional servers that host the exact same data:
-	https://target-osd-2.chals.io
-	https://target-osd-3.chals.io

---

## Flag Format
An email address, for example: example@wicys.example. The flag IS NOT case-sensitive.

---

## Tools Used
Web Browser, OpenSearch Dashboards

---

## Methodology
The objectives provided the credentials to log into Insightful Horizon. 

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d2-insightful-horizon-login.png" alt="d2-insightful-horizon-login graphic" width="400">
</p>

From challenge D1, the sender’s information was noted: date, time, and to whom it was sent as March 22, 2025; 252.44.98.29; 9:10 PM; security@personalyz.io. A query was performed on Insightful Horizon based on the sender’s IP address (252.44.98.29) to locate the email logs. 

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d2-query-sender-ip.png" alt="d2-query-sender-ip graphic" width="800">
</p>

Additional filters were applied based on the results of this search, such as security@personalyz.io and data that would reference potential data theft. 

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d2-second-filter-search.png" alt="d2-second-filter-search graphic" width="800">
</p>

I reviewed the data and noticed that one entry dated, March 21, 2025, included the following subject line, “Warning: We have acquired sensitive data,” which sounded similar to the extortion email from D1. Therefore, this entry log was the first extortion email sent by the threat actor. I found two ways to obtain the sender’s email address. Either reading directly inside the log entry or by expanding the log:

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d2-entry-log-expanded.png" alt="d2-entry-log-expanded graphic" width="800">
</p>

---

## Flag
`tharris456@tgwnaagm.co`  

---

## MITRE ATT&CK
<span style="color:yellow; font-style:italic;">(Suggested)</span>
-	**Phishing (T1566):** Under *Initial Access* this technique aligns in this challenge, since the threat actor attempted to deliver a malicious message to pressure the target.
-	**Indicator Removal on Host (T1070):** It’s relevant because analyzing the log required understanding potential obfuscation or hiding of sender information within email records.
-	**Exfiltration Over Alternative Protocol (T1048):** It applies indirectly, as the extortion email represents the adversary’s attempt to extract value by coercing the organization based on stolen or sensitive data.

