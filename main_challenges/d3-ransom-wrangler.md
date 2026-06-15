---
layout: default
title: "Your Page Title Here"
hero:
  heading: "2025 Target + WiCyS Cyber Defense Challenge CTF Write-Ups"
  text: "This page showcases my participation in the 2025 Target Cyber Defense CTF Challenge hosted by WiCyS, which ran from July 1 through August 14, 2025."
---


# D3. Ransom Wrangler

**Points:** 100  
**Level:** Not as Difficult  
**Categories:** Negotiation, Social Engineering, Incident Response, Conflict Resolution

---

## Description
Personalyz.io received an extortion demand claiming that sensitive customer data has been stolen and demanding 45 BTC within 48 hours or the attackers will publish all the allegedly stolen data publicly. Your security team cannot confirm whether any data was actually exfiltrated or if it’s an empty threat. As the lead incident responder, you’re tasked with engaging the threat actor to verify their claims by requesting a sample of the supposedly stolen data; confirm the attacker genuinely possesses customer data; and negotiate the terms to be more favorable.

---

## Objective
To complete this challenge, you must:
1.	**Verify the Breach:** Request and obtain a sample of the allegedly stolen data to verify if a breach actually occurred; look for a specific customer email address as proof (*Flag 1*)
2.	**Negotiate Ransom Reduction:** Successfully convince the attacker to reduce the ransom demand from 45 BTC to below 30 BTC (*Flag 2: CTF-RAN-XXXX*)
3.	**Extend the Deadline:** Negotiate an extension from the initial 48-hour deadline to 96 hours to give your team more time (*Flag 3: CTF-DEA-XXXX*)

---

## Flag Format
Submit all three flags in the following combined format:
email@example.com:CTF-RAN-XXXXXXXX:CTF-DEA-XXXXXXXX

---

## Tools Used
-	Web Browser - to access email
-	Basic understanding of social engineering and negotiation tactics

---

## Methodology
The challenge provided the link (https://target-email.chals.io/) which was accessed to obtain the company’s email interface. I began crafting a response after a review of the initial ransom email. 


<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d3-orig-email-adversary.png" alt="d3-orig-email-adversary" width="800">
</p>


I initialized contact with threat actor by asking for a confirmation of customer data. The threat actor responded by sending proof of customer data which included the email for the first flag:

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d3-confirmation-customer-data.png" alt="d3-confirmation-customer-data graphic" width="800">
</p>


- **Verification:** Belinda UNDERWOOD of Wilkes Barre, PA 
- **Email:** belinda.goose_b@skynet.be.
- **Credit Card Number:** 5129913213705954
- **CVV:** 585, Expiration: 11/28


I commenced negotiating the ransom reduction with an aim below 30 BTC. Initially, I lowered the amount to 20 BTC. I knew the threat actor would not take the bait as the amount was way too low,  but I wanted to see just what type of individual I was dealing with and their style. After a few back-and-forth emails, by the end of the chain conversation, I was able to reduce the ransom down to 29.5 BTC—good enough for me! The goal was to get it below the 30-point mark and mission accomplished. I also received the verification code (CODE: CTF-RAN-10AF9199) for the second flag: 


<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d3-ransom-reduction-1.png" alt="d3-ransom-reduction graphic" width="800">
</p>

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d3-ransom-reduction-2.png" alt="d3-ransom-reduction graphic" width="800">
</p>


Next, I continued communication with the threat actor to extend the deadline. I was able to accomplish the goal and received the verification code (CODE: CTF-DEA-CB4B9245) for the third flag:

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/d3-extending-deadline.png" alt="d3-extending-deadline graphic" width="800">
</p>


Lastly, I combined all three flags in the combined flag format noted in the objectives.

---

## Flag
`belinda.goose_b@skynet.be:CTF-RAN-10AF9199:CTF-DEA-CB4B9245`  

---

## MITRE ATT&CK
<span style="color:yellow; font-style:italic;">(Suggested)</span>
-	**Phishing for Information (T1598):** This applies under Reconnaissance since the defender actively requested proof of data and the adversary supplied stolen records to establish credibility.
-	**Data Manipulation / Extortion (T1657):** Here, this technique is relevant since the attacker’s whole tactic is about psychological leverage. They claimed to have customer data, dangles a sample to prove credibility, and threatened financial harm unless the money was paid. This is a classic example of extortion under MITRE. 
-	**Exfiltration Over Web Services (T1567):** It’s relevant here because the attacker demonstrated possession of customer data that was likely stolen and shared via email to pressure the target.

