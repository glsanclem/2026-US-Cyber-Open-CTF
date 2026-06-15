---
layout: default
title: "2025 WiCyS Target Cyber Defense CTF"
hero:
  heading: "2025 Target Cyber Defense Challenge CTF Write-Up"
  text: "This page showcases my participation in the 2025 Target Cyber Defense CTF Challenge hosted by WiCyS, which ran from July 1 through August 14, 2025."
---

## INTRO

<img src="/2025_wicys_target_ctf/assets/images/a1-target-tier1-badge.png" alt="Tier 1 Badge" style="float: right; margin-left: 15px; width: 300px;" />

<p>
The 2025 Target + WiCyS Cyber Defense Challenge was a Capture the Flag (CTF)-themed event. This writeup shows my methodology, including tactics, techniques, and procedures in the challenge. As a social scientist, I wanted to try something completely new that would challenge my mind, and it was my first time participating in a CTF event. The event allowed me to gain more practical and technical skills, push myself further, and think outside the box while solving cybersecurity issues.
</p>

<p>
There were two tiers: Tier 1 is primarily blue team focused and Tier 2 is red team. This write up is based on my experience from Tier 1. I completed 14 challenges in Tier 1, which included the preliminary and main challenges. Each stage had different levels of difficulty, and you could only progress by capturing the flag. While the MITRE ATT&CK framework encompasses over 300 adversarial tactics, techniques, and common knowledge, I explored the connections during the challenges and added a few to this write up as a way to build familiarity.
</p>

<div style="clear: both;"></div>

## KEY TAKEAWAYS

- Strengthened network analysis, intelligence analysis, and digital forensics skills through mock hands-on CTF challenges.
- Learned to use various sources of research methods from manual to automation analysis during complex investigations.
- Practiced negotiation and incident response techniques in ransomware scenarios.
- Reinforced the importance of having patience, persistence, determination, and analytical thinking when handling cybersecurity challenges.

## SCENARIO

In Tier 1, we worked through simulated cyberattack scenarios against a tech company, Personalyz.io, to test our ability to detect, analyze, and respond to threats. Personalyz.io is a mid-size company with 500 employees that offered data collection SaaS products for the purpose of targeted ads. Personalyz.io received a ransom demand, and we played the defender to identify the intrusion and determine how the data was exfiltrated. The challenges focused on threat detection, digital forensics, incident response, network analysis, and threat intelligence.

## PRACTICE CHALLENGES

Click on any box below to view the challenge.

<div class="challenge-grid">

  <div class="challenge-box">
    <h3><a href="practice_challenges/p1-wicys-welcome">P1. wicys[Welcome]</a></h3>
    <p><strong>Points:</strong> 30</p>
    <p><strong>Category:</strong> Tutorial</p>
  </div>

  <div class="challenge-box">
    <h3><a href="practice_challenges/p2-hidden-challenges">P2. Hidden Challenges</a></h3>
    <p><strong>Points:</strong> 40</p>
    <p><strong>Category:</strong> Recon</p>
  </div>

  <div class="challenge-box">
    <h3><a href="practice_challenges/p3-1-sub-challenge">P3.1 Sub Challenge</a></h3>
    <p><strong>Points:</strong> 50</p>
    <p><strong>Category:</strong> Misc</p>
  </div>

  <div class="challenge-box">
    <h3><a href="practice_challenges/p3-2-limited-attempts">P3.2 Limited Attempts</a></h3>
    <p><strong>Points:</strong> 50</p>
    <p><strong>Category:</strong> Misc</p>
  </div>

  <div class="challenge-box">
    <h3><a href="practice_challenges/p4-hints">P4. Hints</a></h3>
    <p><strong>Points:</strong> 20</p>
    <p><strong>Category:</strong> Tutorial</p>
  </div>

  <div class="challenge-box">
    <h3><a href="practice_challenges/p5-cooperation">P5. Cooperation</a></h3>
    <p><strong>Points:</strong> 60</p>
    <p><strong>Category:</strong> Collaboration</p>
  </div>

  <div class="challenge-box">
    <h3><a href="practice_challenges/p6-scenario">P6. Scenario</a></h3>
    <p><strong>Points:</strong> 70</p>
    <p><strong>Category:</strong> Scenario</p>
  </div>

</div>



## MAIN CHALLENGES

Click on any box below to view the challenge.

<div class="challenge-grid">

  <div class="challenge-box">
    <h3><a href="main_challenges/d1-mystery-mail">D1. Mystery Mail</a></h3>
    <p><strong>Points:</strong> 100</p>
    <p><strong>Category:</strong> Email</p>
  </div>

  <div class="challenge-box">
    <h3><a href="main_challenges/d2-not-so-simple-mail-protocol">D2. Not So Simple Mail Protocol</a></h3>
    <p><strong>Points:</strong> 150</p>
    <p><strong>Category:</strong> Networking</p>
  </div>

  <div class="challenge-box">
    <h3><a href="main_challenges/d3-ransom-wrangler">D3. Ransom Wrangler</a></h3>
    <p><strong>Points:</strong> 200</p>
    <p><strong>Category:</strong> Malware</p>
  </div>

  <div class="challenge-box">
    <h3><a href="main_challenges/d5-ahoy-pcapn">D5. Ahoy, PCAP'n!</a></h3>
    <p><strong>Points:</strong> 120</p>
    <p><strong>Category:</strong> Packet Analysis</p>
  </div>

  <div class="challenge-box">
    <h3><a href="main_challenges/d6-smuggled-away">D6. Smuggled Away</a></h3>
    <p><strong>Points:</strong> 180</p>
    <p><strong>Category:</strong> Steganography</p>
  </div>

  <div class="challenge-box">
    <h3><a href="main_challenges/d7-endpoints-exfiltration">D7. Endpoints and Exfiltration</a></h3>
    <p><strong>Points:</strong> 220</p>
    <p><strong>Category:</strong> Forensics</p>
  </div>

  <div class="challenge-box">
    <h3><a href="main_challenges/d8-shadow-commit">D8. Shadow Commit</a></h3>
    <p><strong>Points:</strong> 250</p>
    <p><strong>Category:</strong> Git/Version Control</p>
  </div>

</div>


## DISCLAIMER 

These write-ups provide educational insight into the process I followed to complete each challenge. Since Tier 1 officially ended, we were given the green flag (pun intended) to create our write-ups, including the flag answers.
