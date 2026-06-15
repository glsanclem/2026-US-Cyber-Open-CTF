---
layout: default
title: "Your Page Title Here"
hero:
  heading: "2025 Target + WiCyS Cyber Defense Challenge CTF Write-Ups"
  text: "This page showcases my participation in the 2025 Target Cyber Defense CTF Challenge hosted by WiCyS, which ran from July 1 through August 14, 2025."
---


# D1. Mystery Mail

**Points:** 100   
**Level:** Not as Difficult  
**Category:** Cybersecurity, Forensic Analysis (E-mail)

---

## Description
What a way to start your day...you've just logged on as a member of Personalyz.io's Cybersecurity team and see the last thing any cyber professional wants to see: an extortion email at the top of your inbox. Looks like we've received a menacing message from an unknown sender, claiming that sensitive data has been stolen from the company. The email demands a ransom and threatens to release the data if the demand is not met within 48 hours. Given the nature of the data we process, this is a serious threat to us and our customers. You've been tasked with performing some analysis on the email itself to ensure our responding teams can respond appropriately.

---

## Objective
Identify the sender's IP address using the attached email file. Don't overthink it!

---

## Flag Format
The flag will be a valid IP address, for example: 242.229.211.211

---

## Tools Used
TextEdit

---

## Methodology
I opened the extortion email to review and examine by double clicking but it only revealed the actual message. 

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d1-extortion-email.png" alt="d1-extortion-email graphic" width="800">
</p>

To obtain the IP address, I right-clicked the document and opened it with TextEdit. The TextEdit file revealed more details such as that the email was received by three actors: mx3.personalyz.io; klaviyo.com; and gwagm.co. By process of elimination, I did not choose the first one since it had our client’s name (personalyz). That left me with klaviyo and gwagm. Since klaviyo ended with a “.com,” a common top-level domain (TLD), I felt it was the most common generic TLD and wasn’t completely suspicion. That left me with: Sun, 23 Mar 2025 10:10:15 +0900 Received: from 252.44.98.29 by gwagm.co which ended with an odd TLD, and I decided that had to be the flag. Since the flag was only asking for the IP address, I jotted down 252.44.98.29 submitted those numbers and it was correct.

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d1-textedit.png" alt="textedit graphic" width="800">
</p>

---

## Flag
`252.44.98.29`  

---

## MITRE ATT&CK 
<span style="color:yellow; font-style:italic;">(Suggested)</span>
-	**Phishing (T1566):** This challenge aligns with phishing under *Initial Access*, since the suspicious email represents an adversary’s attempt to trick or pressure a target through malicious communication.   

