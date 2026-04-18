# Business Email Compromise (BEC) Investigation

## Overview

This project documents a Business Email Compromise (BEC) investigation using Microsoft Sentinel.

The attacker used stolen credentials and an MFA fatigue attack to gain access, create inbox rules, and execute a fraudulent invoice request.

---

## Key Skills Demonstrated

- Threat Hunting (KQL)
- Incident Response
- Log Correlation
- MITRE ATT&CK Mapping
- Cloud Security Analysis

---

## Executive Summary

A finance employee account was compromised after the user approved a malicious MFA request.

The attacker:
- Accessed email data
- Created inbox rules for persistence
- Forwarded sensitive emails externally
- Sent a fraudulent invoice email
- Accessed cloud storage (OneDrive)

A major issue identified:
> * Conditional Access policies were not enforced

---

## Initial Access (MFA Fatigue)

The attacker triggered multiple MFA prompts until the user approved one.

<img width="624" height="209" alt="Screenshot 2026-04-18 at 7 38 09 AM" src="https://github.com/user-attachments/assets/d0d1a80c-791d-413d-a796-073bb9be6843" />

---

## Attacker Infrastructure

A foreign IP address was used to access the account.

<img width="623" height="195" alt="Screenshot 2026-04-18 at 7 39 02 AM" src="https://github.com/user-attachments/assets/1b47aede-585e-4c84-bbda-bf19e120e39b" />

- IP: 205.147.16.190  
- Location: Netherlands  

---

## Key Finding: Pre-MFA Mail Access

Mailbox activity occurred **before MFA approval**, indicating advanced attack behavior.

<img width="623" height="141" alt="Screenshot 2026-04-18 at 7 39 56 AM" src="https://github.com/user-attachments/assets/1cfc3b38-6658-4305-8e76-7d46678dce34" />

---

## Persistence (Inbox Rules)

The attacker created inbox rules to maintain access.

<img width="625" height="194" alt="Screenshot 2026-04-18 at 7 40 43 AM" src="https://github.com/user-attachments/assets/2d880557-bd5a-448e-a63f-fe7da70319b4" />

---

## Data Exfiltration

Sensitive emails were automatically forwarded to an external address.

<img width="625" height="141" alt="Screenshot 2026-04-18 at 7 41 17 AM" src="https://github.com/user-attachments/assets/f02ad1df-1c43-4f07-b874-879102ef5fd6" />

---

## Defense Evasion

Security-related emails were deleted to avoid detection.

<img width="625" height="204" alt="Screenshot 2026-04-18 at 7 41 54 AM" src="https://github.com/user-attachments/assets/399bc80e-a0d6-4376-bd81-9bc021620104" />

---

## BEC Attack Execution

A fraudulent invoice email was sent internally using a trusted conversation.

<img width="625" height="145" alt="Screenshot 2026-04-18 at 7 42 23 AM" src="https://github.com/user-attachments/assets/7c990ae1-3acc-43a3-84ac-c346dd02e796" />

---

## Lateral Movement

The attacker accessed cloud storage after sending the fraudulent email.

<img width="625" height="220" alt="Screenshot 2026-04-18 at 7 43 15 AM" src="https://github.com/user-attachments/assets/b7bb8090-cf2b-40fb-aada-edf1be83647f" />

---

## Root Cause

A critical security failure allowed the attack.

<img width="625" height="261" alt="Screenshot 2026-04-18 at 7 43 51 AM" src="https://github.com/user-attachments/assets/bf64714e-a9ce-4f5d-9ea7-be548b5b883a" />


- No Conditional Access enforcement  
- MFA fatigue attack successful  
- Stolen credentials used  

---

## MITRE ATT&CK Mapping

| Tactic | Technique | Description |
|-------|----------|-------------|
| Initial Access | T1078 – Valid Accounts | Attacker used stolen credentials to access the account |
| Credential Access | T1621 – Multi-Factor Authentication Request Generation | MFA fatigue attack used to gain access |
| Persistence | T1098 – Account Manipulation | Inbox rules created to maintain access |
| Defense Evasion | T1564.008 – Email Hiding Rules | Security-related emails deleted to avoid detection |
| Collection | T1114 – Email Collection | Attacker accessed and reviewed mailbox contents |
| Exfiltration | T1020 – Automated Exfiltration | Emails automatically forwarded to an external account |
| Impact | T1566.002 – Phishing (BEC) | Fraudulent invoice email sent using compromised account |

## Indicators of Compromise (IOCs)

- 205.147.16.190  
- insights@duck.com  
- Inbox Rules: ".", ".."  

---

## Recommendations

- Enforce Conditional Access
- Disable legacy authentication
- Use phishing-resistant MFA
- Monitor inbox rule creation
- Train users on MFA fatigue attacks

---

## Conclusion

This incident demonstrates how attackers can bypass MFA using social engineering and exploit weak identity controls to execute financial fraud and access sensitive data.

---

## 👤 Author

Jason Stokes  
Cybersecurity | Threat Hunting | Incident Response
