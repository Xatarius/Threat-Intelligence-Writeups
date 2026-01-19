# Technical Threat Intelligence Report: Microsoft Outlook "2FA Verification" Phishing

**Date of Analysis:** January 20, 2026
**Analyst:** Roy Castro
**Threat Level:** 🔴 High (Credential Harvesting / Account Takeover)
**Campaign Status:** Active

---

## 1. Executive Summary
This report documents a credential harvesting campaign targeting Microsoft Outlook users. The Threat Actor (TA) utilizes **Compromised Academic Accounts** (University of Uberlândia, Brazil) to distribute phishing emails, bypassing standard SPF/DKIM filters. The campaign leverages **Free Hosting Infrastructure** (`webcindario.com`) to host a fraudulent landing page mimicking the Microsoft 2FA login portal.

## 2. Attack Lifecycle (Kill Chain)
* **Initial Vector:** Phishing email sent from a compromised legitimate educational account (`@ufu.br`).
* **Lure:** False security alert stating "Su cuenta será bloqueada" (Your account will be blocked) due to missing 2-step verification.
* **Trust Layer:** Usage of valid SPF/DKIM signatures from the compromised university domain to bypass "Spam" folders.
* **Payload URL:** `hxxps://protegermiemail3.webcindario[.]com/`
* **Objective:** Exfiltration of Microsoft user credentials and Personal Phone Numbers (WhatsApp).

## 3. Technical Indicators of Compromise (IoCs)

| Indicator Type | Value | Context |
| :--- | :--- | :--- |
| **Sender Address (From)** | `gustavo-barbosa@ufu.br` | Compromised Account (Univ. Federal de Uberlândia). |
| **Sender Display Name** | `Protege ahora!` | Social Engineering tactic. |
| **Phishing Domain** | `protegermiemail3.webcindario[.]com` | Free hosting subdomain (Miarroba). |
| **Subject Line** | `Procederemos la Verificacion` | Urgency / Authority. |
| **Hosting Provider** | Miarroba Networks (Spain) | Infrastructure abuse. |

## 4. Visual Evidence

**Figure 1: Full Phishing Email Artifact**
The capture below illustrates the complete social engineering flow:
1.  **Impersonation:** Uses the official Outlook color scheme (#0072C6).
2.  **Fear Appeal:** Warns of imminent account blockage.
3.  **Anomalous Request:** Explicitly asks to link a **WhatsApp** number, a non-standard procedure for Microsoft enterprise security.
4.  **Malicious Link:** Redirects to a low-reputation free hosting subdomain.

![Full Phishing Analysis](Phishing_Analysis_ufu.br.jpg)

## 5. Evasion Techniques & Technical Analysis

### A. Compromised Academic Infrastructure (Sender Identity)
The email headers reveal the message originated from a valid university server in Brazil:
```text
From: Protege ahora! <gustavo-barbosa@ufu.br>
