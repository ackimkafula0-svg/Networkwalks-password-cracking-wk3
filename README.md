
# NETWORKWALKS-B084-WK3-JTR-PASSWORD-CRACKING
### Week 3 – Project Module 1: Password Cracking with John the Ripper

![Platform](https://img.shields.io/badge/Platform-Ubuntu-E95420?logo=ubuntu&logoColor=white)
![Tool](https://img.shields.io/badge/Tool-John%20the%20Ripper-black)
![Interface](https://img.shields.io/badge/Interface-CLI-informational)
![Status](https://img.shields.io/badge/Status-Complete-success)

A hands-on password-auditing lab from the NetworkWalks Cybersecurity & Ethical Hacking Program (Batch B084): using **John the Ripper (JTR)** via the command line, and the NetworkWalks Hash Calculator & Password Cracker web tools, to recover the passwords of protected PDFs on Ubuntu.

🔗 Project post: [https://lnkd.in/p/dzWHsqhZ](#)

---

## Table of Contents

- [Overview](#overview)
- [Lab Objectives](#lab-objectives)
- [Lab Environment](#lab-environment)
- [Tools & Technologies](#tools--technologies)
- [Repository Structure](#repository-structure)
- [Practical Workflow](#practical-workflow)
- [Screenshot Evidence](#screenshot-evidence)
- [Result](#result)
- [Learning Outcomes](#learning-outcomes)
- [Security Insights](#security-insights)
- [Ethical Considerations](#ethical-considerations)
- [References](#references)
- [Author](#author)
- [Disclaimer](#disclaimer)

---

## Overview

John the Ripper (JTR) is a widely used password-auditing tool for testing password strength, capable of checking many hash types and unlocking password-protected files such as PDF, ZIP, and Office documents.

This lab uses JTR directly from the Ubuntu command line, in a controlled training environment, to recover the password of protected PDFs. For one of the files, the NetworkWalks **Hash Calculator** and **Password Cracker** web tools were used instead — these simulate the same dictionary-attack logic as JTR (hashing each word in a wordlist and checking it against the target `$pdf$` hash) through a browser interface. Either way, the exercise demonstrates concretely why weak passwords are a security liability.

## Lab Objectives

- Understand the fundamentals of password auditing.
- Explore John the Ripper's core functionality from the CLI.
- Compare a CLI-based dictionary attack (JTR) against a browser-based equivalent (NetworkWalks Hash Calculator / Password Cracker).
- Understand the difference between a password-protected file and the password hash representation these tools actually attack.
- Walk through a dictionary-based password-auditing workflow end to end.
- Document the process with real screenshots, in chronological order.

## Lab Environment

| Component | Detail |
|---|---|
| Host OS | Ubuntu (Linux) |
| Password-Auditing Tool | John the Ripper (JTR) |
| Interface | Command Line (Terminal) |
| Alternate Tool | NetworkWalks Hash Calculator & Password Cracker (web) |
| Target Files | Password-protected PDFs (incl. `My Locked PDF1.pdf`) |

## Tools & Technologies

| Tool | Purpose |
|---|---|
| John the Ripper | Core password-auditing engine (CLI) |
| `pdf2john.py` | Extracts the password-hash representation of a protected PDF |
| NetworkWalks Hash Calculator | Browser-based tool to extract a PDF's `$pdf$...` hash |
| NetworkWalks Password Cracker | Browser-based dictionary-attack tool matching wordlist entries against the `$pdf$` hash |
| Terminal / Bash | Running JTR commands |
| Dictionary wordlist | `rockyou.txt` (14,344,380 words) used as the candidate-password list |

## Repository Structure

```
NETWORKWALKS-B084-WK3-JTR-PASSWORD-CRACKING/
│
├── README.md
│
├── John/
│   ├── Screenshot 2026-11-16 014535.png
│   ├── Screenshot 2026-11-16 015330.png
│   ├── ... (screenshots in chronological order)
│   └── Screenshot 2026-11-16 023610.png
```

## Practical Workflow

**Step 1 — Install John the Ripper**
Installed JTR on Ubuntu (via `apt` or by building from the official Openwall source).

**Step 2 — Prepare the target PDF**
Placed the encrypted lab PDF (`My Locked PDF1.pdf`) in the working directory.

**Step 3 — Extract the PDF hash**
Used `pdf2john.py` to convert the protected PDF into a crackable hash format and redirected the output into `hash1.txt`.

```bash
pdf2john.py "My Locked PDF1.pdf" > hash1.txt
```

**Step 4 — Run the dictionary attack**
Ran John the Ripper against `hash1.txt` using a wordlist.

```bash
john --wordlist=/path/to/wordlist.txt hash1.txt
```

**Step 5 — Reveal the cracked password**
Once JTR found a match, displayed the recovered password.

```bash
john --show hash1.txt
```

**Step 6 — Verify the result**
Reopened the original encrypted PDF and entered the recovered password to confirm it worked.

**Step 7 — Third PDF: NetworkWalks Hash Calculator & Password Cracker**
For the third protected PDF, used the NetworkWalks **Hash Calculator** to extract its `$pdf$...` hash, then pasted that hash into the NetworkWalks **Password Cracker** tool. Selected the `rockyou.txt` wordlist (14,344,380 words) as the active list and ran **Start Cracking**, which tried candidate passwords against the hash in the same way JTR would, until a match was found.

## Screenshot Evidence

*(Grouped by workflow stage, ordered by capture timestamp.)*

### 1. Installation & Setup
Installing John the Ripper on Ubuntu.
<img width="1360" height="761" alt="Screenshot from 2026-11-20 00-29-47" src="https://github.com/user-attachments/assets/9f4b0bce-502c-4b70-a619-0adb273ac649" />


### 2. PDF Hash Extraction
Running `pdf2john.py` against the target PDF and generating `hash1.txt`.

<img width="1360" height="761" alt="image" src="https://github.com/user-attachments/assets/d07bc048-77f9-4cc8-8b3c-c632bb8d5b9b" />

### 3. Password Audit Execution
Running `john --wordlist=...` against `hash1.txt` — dictionary attack in progress.
<img width="1360" height="761" alt="Screenshot from 2026-11-20 00-51-37" src="https://github.com/user-attachments/assets/55539ae4-b75d-4eac-8bed-8c359274c32d" />


### 4. Result Verification
Running `john --show hash1.txt` to reveal the recovered password, then reopening the PDF to confirm.
<img width="1360" height="761" alt="Screenshot from 2026-11-20 00-56-56" src="https://github.com/user-attachments/assets/233cd9f3-33cf-45cf-9dba-54a6e6eb89f5" />



### 5. Third PDF — NetworkWalks Hash Calculator & Password Cracker
Pasting the extracted `$pdf$...` hash into the Password Cracker tool, selecting the `rockyou.txt` wordlist, and running the dictionary attack to completion.
<img width="1360" height="761" alt="Screenshot from 2026-11-20 01-04-42" src="https://github.com/user-attachments/assets/b6d7d120-4f3c-4c1a-94f8-c47b124e1398" />

## Result
<img width="1360" height="761" alt="Screenshot from 2026-11-20 01-04-26" src="https://github.com/user-attachments/assets/415966ae-4188-49f2-b85b-c041b90799dd" />


The passwords for the protected PDFs were successfully recovered — two via John the Ripper on the Ubuntu CLI, and one via the NetworkWalks Hash Calculator and Password Cracker web tools — and verified by reopening each file. The following flags were captured from the recovered PDF content:

```
nw{networkwalks_flag1_jtr_270521_1}
nw{networkwalks_persistence_jtr_270521}
```

## Learning Outcomes

- Practical exposure to password auditing using an industry-standard tool.
- Working understanding of John the Ripper's CLI workflow on Linux.
- Comparison of a native CLI tool (JTR) against a browser-based equivalent built on the same dictionary-attack principle.
- Clear grasp of the role password hashes play in security testing — and that a hash is not simply "scrambled" data you decrypt back to the original.
- Hands-on experience with dictionary-based auditing against real protected files.
- Reinforced awareness of why weak passwords are a serious security liability.
- Improved technical documentation and evidence-based writeup skills.

## Security Insights

- **Weak passwords fall fast**: dictionary attacks like this one succeed quickly against common, short, or predictable passwords.
- **Length and complexity matter**: longer passwords with mixed character types dramatically increase the search space an attacker has to cover.
- **Reuse compounds risk**: a password cracked once can unlock every other account that reuses it.
- **Hashing vs. encryption**: encryption is reversible with the right key; hashing is a one-way function. Tools like JTR (and the NetworkWalks Password Cracker) don't "decrypt" a password hash — they hash candidate passwords from a wordlist and check for a match, which is why a strong, unpredictable password resists this kind of audit even when the hash itself is exposed.
- **Defense in depth**: strong password policies plus multi-factor authentication (MFA) meaningfully reduce the real-world impact of a cracked or leaked password.
- **Responsible use**: password auditing is a legitimate security practice only when performed on systems and files you're authorized to test.

## Ethical Considerations

This project was carried out strictly for educational purposes, as part of an authorized NetworkWalks Cybersecurity training exercise in a controlled lab environment.

- Intended for learning password-security concepts and authorized security testing only.
- Not intended to encourage or assist cracking passwords on files, accounts, or systems you do not own or have explicit permission to test.
- Password auditing should always be performed responsibly, with proper authorization.

## References

- John the Ripper (official): https://www.openwall.com/john/
- NetworkWalks Academy: https://www.networkwalks.com/
- NetworkWalks Password Cracker tool: https://networkwalks.com/password-cracker/

## Author

Ackim Kafula Cybersecurity intern — NetworkWalks Cybersecurity & Ethical Hacking Program (Batch B084)

## Disclaimer

This repository documents a training lab exercise completed as part of NetworkWalks Academy's cybersecurity coursework. It is shared for educational and portfolio purposes only and does not constitute professional penetration-testing services or endorse unauthorized password recovery of any kind.
