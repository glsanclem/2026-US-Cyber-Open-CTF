---
layout: default
title: "Your Page Title Here"
hero:
  heading: "US Cyber Open Challenge 2026 CTF Technical Writeup"
  text: "Selected CTF challenges, methodologies, and technical analysis from the Season VI: 2026 US Cyber Open, June 5 to 14, 2026."
---


# Souvenirs

| Points | Difficulty | Category |
| :----- | :--------- | :------- |
| 132 | Easy | Forensics, Steganography |

## Description
Every traveler comes home with a bag full of souvenirs — some you put on a shelf, some you tuck quietly inside other things so the airport doesn't ask questions. This postcard came back from a long trip around the world. Open it carefully. Some travelers leave more behind a picture than you'd think.

This is an `Around The World` challenge submitted by `Women in CyberSecurity Middle East (WiCSME)`.


## Objective
The objective was to find a hidden file (ZIP archive) that was secretly appended to the end of an image file and then extract the text files inside it to find the flag.


## Flag Format
The flag should be in the format: SVIUSCG{This_is_a_Flag}


## Tools Used
MacOS Terminal


## Methodology
When I read from the description, “*some you tuck quietly inside other things…and some leave more behind a picture than you’d think,*” I felt that there was some hidden data behind the image or file structure.

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/5-souvenirs-sunset.jpg" alt="Sunset graphic" width="500">
</p>

Sometimes a `.jpg` has either a `.zip` or `.txt` attached to it and that file might have information which is valuable to solving the challenge.

I opened a terminal on the computer, typed the following strings code, and hit enter:

`strings image {attached image file} | tail -n 20`

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/5-souvenirs-strings-lines-in-terminal.jpg" alt="Terminal lines graphic" width="400">
</p>

The file listed a bunch of letters and symbols, but what caught my attention were four text files at the bottom titled, “marrakech, tokyo, oman, and iceland.” 

To unzip those file, I ran the following command in the terminal:

`unzip /Users/Desktop/souvenirs.jpg`

This created a folder on the desktop with text files. I opened each one and read through the messages for any clue or the flag.

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/5-souvenirs-tokyo-txt-file.jpg" alt="Tokyo graphic" width="700">
</p>


<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/5-souvenirs-marrakech-txt-file.png" alt="Marrakech graphic" width="700">
</p>


<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/5-souvenirs-iceland-txt-file.png" alt="Iceland graphic" width="700">
</p>

The flag was finally revealed in the last document:

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/5-souvenirs-oman-txt-file.png" alt="Oman graphic" width="700">
</p>


## Flag
`SVIUSCG{p0stc4rds_h1dd3n_p4st_th3_FFD9_h0r1z0n}`  


## MITRE ATT&CK
<span style="color:yellow; font-style:italic;">_Reflections | Suggestions | What was the Attacker Doing?_</span>

If we think about it from the attacker's perspective, the idea is to hide information inside of another file to prevent detection. Here, the JPEG contained additional data that was not visible when the image was opened normally.

| Field | Details |
|:--------|:---------|
| ID | T1027 |
| Tactic | Defense Evasion |
| Technique | Obfuscated Files or Information |
| Mitigation | Inspect files for embedded or hidden content using forensic and file analysis tools. Validate file formats and investigate files whose contents do not match their expected structure. |
| Detection Strategy | Monitor for files containing unxpected embedded data, appended archives, or abnormal file structures. Use file integrity checks and forensic analysis tools to identify hidden content. |

Source: https://attack.mitre.org
