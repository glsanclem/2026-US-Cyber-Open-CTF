---
layout: default
title: "Your Page Title Here"
hero:
  heading: "US Cyber Open Challenge 2026 CTF Technical Writeup"
  text: "Selected CTF challenges, methodologies, and technical analysis from the Season VI: 2026 US Cyber Open, June 5 to 14, 2026."
---


# Manifest

| Points | Difficulty | Category |
| :----- | :--------- | :------- |
| 205 | Hard | Network Forensics |


## Description
Lakeshore Threat Lab confirmed an attacker pivoted from `FIN-WS-07` to `NAS-MARITIME-01`, the Wabash Marine NAS that hosts the internal Lakefront Fleet Manager web app on port 8088. Imani Boateng captured a short east-west slice of that pivot. Her capture is attached.


## Objective
Identify and reconstruct the exfiltrated data from an unauthorized HTTP GET request during an east-west network pivot to recover the hidden flag.


## Flag Format
The flag should be in the format: SVIUSCG{This_is_a_Flag}


## Tools Used
Wireshark, CyberChef


## Methodology
Saved `.pcap` file on desktop, and opened it with Wireshark. 

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/7-manifest-image-one.png" alt="Image one graphic" width="400">
</p>

I reviewed the platform to see if anything jumped out at me and noticed in the Info column the entry `HTTP/1.1 200 OK (text/plain)` which looked different from the other entries. _Why did the entry say “OK”_? _Could it be some sort of communication between two sources (i.e. a hacker trying to get information)_?

I clicked on the entry and in the bottom left panel, I noticed four Line-based text data. 

- `crew_manifests_q1_2026.csv\n`
- `crew manifests_q2_2026.csv\n`
- `crew_manifests_q4_2025.csv\n`
- `billet_summarv_2026.json\n`

More questions came to mind: _Why was q3_2026 not included_? _Where did q4_2025 come from when the other line-based text say 2026_? _Was that information which the hacker was trying to obtain?_ 

I needed to investigate further and find the HTTP GET or HTTP POST request that triggered that text and the questions in my mind. I looked back again at all the entries in the “Info” column for something close to those text exchange. 

I found a GET entry that specifically mentioned: `GET /api/v1/personnel/crew_manifests_q2_2026.csv HTTP/1.1`

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/7-manifest-image-two.png" alt="Image two graphic" width="400">
</p>

I found the exact moment the theft happened! I believe this GET request was when the attacker asked the server to give them the file containing the crew manifests for the second quarter of 2026.

Now, I needed to see what the server gave them. I performed the following: right clicked the Entry > Follow > HTTP Stream. I was shocked to find a long list of personal information which included personnel crew names, id, rank, billet, start and dates.

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/7-manifest-image-three.png" alt="Image three graphic" width="400">
</p>

One particular name, Tolliver Jonas, stood out to me: `WAB-2207,BR9X2E,Jonas,Tolliver,Master,Charter Liaison,2026-02-14,U1ZJVVNDR3t3YWJhc2hfZmlud3NfcGl2b3RfbmFzX21hcml0aW1lXzAxfQ==`

_Why did Tolliver Jonas have a long string of letters and numbers next to the record?_ It was the only entry that looked out of place. That was it!! I quickly copied those fragments and opened CyberChef, plugged the data into the Input box, and added the operations Base64, Hex, and Magic. 

There we have it! The output box revealed the flag:

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/7-manifest-image-four-FLAG.png" alt="Image four graphic" width="400">
</p>

In summary, for this challenge, I performed a full-scale forensic investigation which included identifying the attacker’s movement, isolating the malicious network traffic, extracting the stolen data from a packet stream, and using CyberChef to decode the final payload. 


## Flag
`SVIUSCG{wabash_finws_pivot_nas_maritime_01}`


## MITRE ATT&CK
<span style="color:yellow; font-style:italic;">_Reflections | Suggestions | What was the Attacker Doing?_</span>

Let's simplify things by ignoring Wireshark, CyberChef, and the methodology. Instead, let's view it from the attacker's perspective. The attacker moved from one computer to another, they found a file they wanted, and sent an HTTP GET request asking for that file (`crew_manifest_q2_2026.csv`). The server responded with the file and the attacker now had the data. The attacker's goal wasn't to hide or encrypt, but rather to collect data. Thus, I believe a MITRE ATT&CK to keep in mind in this scenario is the Collection tactic. While there are many type of techniques under Collection, the closest one that caught my eye was "data from local system," because the attacker was simply collecting a file from a computer. 

| Field | Details |
|:--------|:---------|
| ID | T1005 |
| Tactic | Collection |
| Technique | Data from Local System |
| Mitigation | Limit access to sensitive files using the principle of least privilege, segment internal networks, and require authentication and authorization for access to sensitive resources. |
| Detection Strategy | Monitor for unusual HTTP GET requests targeting sensitive files, unexpected access to internal file repositories, and abnormal data retrieval from network attached storage (NAS) systems. |

Source: https://attack.mitre.org
