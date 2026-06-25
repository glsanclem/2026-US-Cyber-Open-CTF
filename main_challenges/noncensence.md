---
layout: default
title: "Your Page Title Here"
hero:
  heading: "US Cyber Open Challenge 2026 CTF Technical Writeup"
  text: "Selected CTF challenges, methodologies, and technical analysis from the Season VI: 2026 US Cyber Open, June 5 to 14, 2026."
---


# Noncesence

**Points:** 100  
**Difficulty:** Beginner
**Category:** Crypto

---

## Description
This encryption service will encrypt any plaintext you send it. It also encrypted our flag — can you recover it? Attachment: `nc challenge.ctf.uscybergames.com 55705`

---

## Objective
The objective was to recover a hidden flag encrypted by a remote server. The server provided an "encryption service" where users could send any plaintext and receive the encrypted version in return. The challenge provided the source code `server.py` to help analyze how the encryption was being handled.

---

## Flag Format
The flag format will either be: SVBRG{This_is_a_Flag} or SVIBGR{This_is_a_Flag}

---

## Tools Used
- TextEdit
- Netcat (nc)
- Socat
- CyberChef

---

## Methodology

### **1. Analysis**

I opened the server.py file with TextEdit to see how the challenge worked behind the scenes. I noticed that the server included **AES** cipher encrypted data. Specifically, I noticed the server was using AES-CTR (counter mode).

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/4-noncensense-server.png" alt="server graphic" width="400">
</p>

From my understanding, this mode generates a keystream (stream of random bytes) using a `KEY` and a `NONCE`, and then combines that keystream with the plaintext using **XOR**.

As I continued to read through the code, I noticed that both the `KEY` and `NONCE` were generated only once when the server started:

```
KEY = os.urandom(16)
NONCE = os.urandom(8)
```

Since these values never changed, it appeared that the server was using the **same keystream** to encrypt both the flag and any user supplied input. After doing a bit of research, I learned this is a cryptographic weakness known as **Nonce Reuse**.

### **2. Execution**

To test the theory, I connected to the challenge instance and copied the “Encrypted Flag.”

Next, I sent a string of 32 zeros (`0000...`) in hexadecimal format to the server. Since XORing with zero returns the original value, the resulting ciphertext revealed the keystream being used by the server.

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/4-noncensense-ciphertext.png" alt="ciphertext graphic" width="400">
</p>

### **3. Solution**

Once I had both the encrypted flag and the keystream, I moved over to CyberChef.

Using  the XOR operation, I combined the `Encrypted flag` with the recovered `Keystream` (the ciphertext of the zeros). Since the XOR is reversible,  the keystream cancelled itself out and revealed the original plaintext.

The logic looked like this:

Flag XOR Keystream = Encrypted Flag

Encrypted Flag XOR Keystream = Flag

The output revealed the flag: `SVIBGR{...}`.

<p align="center">
  <img src="/2025_wicys_target_ctf/assets/images/4-noncensense-cyberchef-flag.png" alt="cyberchef flag graphic" width="400">
</p>

---

## Flag
`SVIBGR{3t_7u_k3y$7r34m}`

---

## MITRE ATT&CK
<span style="color:yellow; font-style:italic;">(What was the Attacker Doing? | Reflections | Suggestions)</span>

**CWE-323: Reusing a Nonce, Key Pair in Encryption**

| Field | Details |
|:--------|:---------|
| ID | CWE-323 |
| Weakness | Reusing a Nonce, Key Pair in Encryption |
| Mitigation | Generate a unique nonce for every encryption operation and never reuse a nonce and key pair. |
| Detection Strategy | Review cryptographic implementations for nonce reuse and test encryption systems for repeated keystream generation. |

Source: https://attack.mitre.org
