---
layout: default
title: "Your Page Title Here"
hero:
  heading: "2025 Target + WiCyS Cyber Defense Challenge CTF Write-Ups"
  text: "This page showcases my participation in the 2025 Target Cyber Defense CTF Challenge hosted by WiCyS, which ran from July 1 through August 14, 2025."
---


# P2. Hidden Challenges

**Points:** 30  
**Level:** Simple  
**Category:** Tutorial  

---

## Description
<span style="color:orange; font-weight:bold;">F</span>ollowing a narrative means some challenges could spoil earlier ones, so most challenges will be hidden at the beginning. <span style="color:orange; font-weight:bold;">L</span>etting yourself bounce between the offensive and defensive challenges should prevent you from getting stuck. <span style="color:orange; font-weight:bold;">A</span>s you complete challenges, more will be unlocked - this also helps you get a feel for how an attack would actually unfold!

---

## Objective
<span style="color:orange; font-weight:bold;">G</span>et the flag by finding the hidden message spelled out by combining the first letter in each sentence.

---

## Tools Used
Cognitive tools: CEO of the brain, working memory, selective attention

---

## Methodology
This was another challenge that required carefully reading instructions, paying close attention to details, and analyzing information. I noticed that the first letter of each sentence was bold and highlighted. I thought that was a bit odd and kept that minor detail in mind.  After reading the instructions, I immediately knew the bold letters was the flag.  **Lesson**: Follow your intuition. If something feels off, take note of it, as it just might be the answer to your flag.  

---

## Flag
`FLAG`  

---

## MITRE ATT&CK
<span style="color:yellow; font-style:italic;">(Suggested)</span>
- **Tactics:** Reconnaissance (TA0043); Discovery (TA0007); Collection (TA0009). 
- **Techniques:** In **Reconnaissance**, we actively scanned the target’s message to identify any messages that appear a bit off. In **Discovery**, we discovered files that may have sensitive data. In **Collection**, we captured and stored the data obtained from the message. 
- **Procedures:** As part of the defense team, we performed analysis to gather intelligence to prevent the attack. Our discovery process entailed revealing the artifacts (individual letters) and collecting the evidence to understand its full scope and perform forensics.

 

 
