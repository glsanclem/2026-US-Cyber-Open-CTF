---
layout: default
title: "Your Page Title Here"
hero:
  heading: "US Cyber Open Challenge 2026 CTF Technical Writeup"
  text: "Selected CTF challenges, methodologies, and technical analysis from the Season VI: 2026 US Cyber Open, June 5 to 14, 2026."
---


# Up to Date

| Points | Difficulty | Category |
| :----- | :--------- | :------- |
| 100 | Beginner | Misc |


## Description
Our newly hired developer at our company seems to be big on vibe coding, and asked Claude Sonnet to generate some Zen-C code in a moment of hurried inspiration. They attempted to send this code over our system, but it seems like something went wrong with the transmission, resulting in custom TCP payloads! The code got split up into multiple chunks, and some network noise has been mixed in with the transmission. Luckily, they've done some preliminary analysis of the packets and determined how the valid and noise packets were transmitted and given you their annotations. Unfortunately though, we aren't exactly Up To Date with what the new generation is up to today, so we leave the decoding task to you. Filter the noise, reverse the custom protocol, and analyze the Zen-C source code.


## Objective
The objective was to recover the hidden flag from a set of provided files: `chall.py` and `output.txt`


## Flag Format
The flag format will either be: SVBRG{This_is_a_Flag} or SVIBGR{This_is_a_Flag}


## Tools Used
- **Terminal** was used as a primary tool to execute **Python** `python3 solve.py`
- **File Management** to navigate all of the folders on the Desktop and organizing the files.


## Methodology

The first step included analyzing the file `chall.py` to understand how the secret was hidden. To open the python file, I right clicked and opened the file with a **text editor**.

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/3-uptodate-chall.png" alt="Chall graphic" width="700" height="900">
</p>

I discovered the `chall.py` file included secret text split into five chunks and each chunk was wrapped was in a packet starting with a Magic Header (ZN), followed by a Sequence (Seq) number, and the Length (Len) of the data. It seems like the script added fake noise to the file to confuse the search tools.

Since the challenge also included a file called `solve.py`, I took a look at it to better understand how the packets were being reconstructed. 

I used the Python script, `solve.py` to recover the flag, which scanned the `output.txt` file for the ZN magic bytes.

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/3-uptodate-output.png" alt="Chall graphic" width="700">
</p>

It also checked if the packet started with the correct Sequence ID and placed the chunks back together in the proper order. A piece of code was recovered in a fictional language called **Zen-C**.

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/3-uptodate-solv.png" alt="Chall graphic" width="700">
</p>

The recovered Zen-C code revealed an XOR Cipher that used a single key (`0x42`)and the flag was revealed! 

<p align="center">
  <img src="/2026-US-Cyber-Open-CTF/assets/images/3-uptodate-flag-reveal.png" alt="Flag graphic" width="700">
</p>


## Flag
`SVIBGR{z3n_c_v1b3_da7a_gr4m}`


### Key Lessons

- **Careful with running the challenge script:** Often, `chall.py` is just a map to show how the puzzle was made. Running it can overwrite the evidence (like what happened to the `output.txt`).
- **Magic Bytes are Clues:** Whenever you see a repeating pattern like `ZN` in a hex file, it's usually a "Header" that tells you where a piece of important data starts.
- **XOR Spotting:** If you see a list of hex numbers and a single key, such as`0x42`, it is often that XOR was used to hide the data.


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
