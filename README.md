# 🛡️ Business Email Compromise (BEC) Investigation

## 📌 Overview

This project documents a Business Email Compromise (BEC) investigation using Microsoft Sentinel.

The attacker used stolen credentials and an MFA fatigue attack to gain access, create inbox rules, and execute a fraudulent invoice request.

---

## 🎯 Key Skills Demonstrated

- Threat Hunting (KQL)
- Incident Response
- Log Correlation
- MITRE ATT&CK Mapping
- Cloud Security Analysis

---

## 🚨 Executive Summary

A finance employee account was compromised after the user approved a malicious MFA request.

The attacker:
- Accessed email data
- Created inbox rules for persistence
- Forwarded sensitive emails externally
- Sent a fraudulent invoice email
- Accessed cloud storage (OneDrive)

A major issue identified:
> ❌ Conditional Access policies were not enforced

---

## 🔓 Initial Access (MFA Fatigue)

The attacker triggered multiple MFA prompts until the user approved one.

![MFA Fatigue Evidence](mfa-fatigue-signinlogs.png)

---

## 🌍 Attacker Infrastructure

A foreign IP address was used to access the account.

![Attacker IP](attacker-ip-netherlands.png)

- IP: 205.147.16.190  
- Location: Netherlands  

---

## 🚨 Key Finding: Pre-MFA Mail Access

Mailbox activity occurred **before MFA approval**, indicating advanced attack behavior.

![Pre-MFA Mail Access](premfa-mail-access.png)

---

## 🧩 Persistence (Inbox Rules)

The attacker created inbox rules to maintain access.

![Inbox Rule Creation](inbox-rule-creation.png)

---

## 📤 Data Exfiltration

Sensitive emails were automatically forwarded to an external address.

![Forwarding Rule](forwarding-rule-exfiltration.png)

---

## 🗑️ Defense Evasion

Security-related emails were deleted to avoid detection.

![Delete Rule](delete-rule-evasion.png)

---

## 💰 BEC Attack Execution

A fraudulent invoice email was sent internally using a trusted conversation.

![BEC Email](bec-email-evidence.png)

---

## ☁️ Lateral Movement

The attacker accessed cloud storage after sending the fraudulent email.

![OneDrive Access](onedrive-file-access.png)

---

## 🚫 Root Cause

A critical security failure allowed the attack.

![Conditional Access Failure](conditional-access-failure.png)

- No Conditional Access enforcement  
- MFA fatigue attack successful  
- Stolen credentials used  

---

## 📌 Indicators of Compromise (IOCs)

- 205.147.16.190  
- insights@duck.com  
- Inbox Rules: ".", ".."  

---

## 🔒 Recommendations

- Enforce Conditional Access
- Disable legacy authentication
- Use phishing-resistant MFA
- Monitor inbox rule creation
- Train users on MFA fatigue attacks

---

## 📎 Conclusion

This incident demonstrates how attackers can bypass MFA using social engineering and exploit weak identity controls to execute financial fraud and access sensitive data.

---

## 👤 Author

Jason Stokes  
Cybersecurity | Threat Hunting | Incident Response
