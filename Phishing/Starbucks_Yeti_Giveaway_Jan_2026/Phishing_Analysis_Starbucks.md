# Technical Threat Intelligence Report: "Starbucks Reward" Phishing Campaign

**Date of Analysis:** January 28, 2026
**Analyst:** Roy Castro
**Threat Level:** 🔴 High (Credential Harvesting & Financial Fraud)

---

## 1. Executive Summary
This report analyzes a phishing campaign impersonating **Starbucks Rewards**. The attack uses a "Baiting" technique by offering a free YETI® Rambler Tumbler to selected members. Technical indicators suggest this campaign is part of a larger cluster of attacks, as it shares identical infrastructure (SMTP relays and landing page IPs) with the "AAA" campaign analyzed previously.

## 2. Attack Lifecycle (Kill Chain)
* **Initial Vector:** Email delivery through a compromised or malicious Microsoft tenant relay (`ant20562425.onmicrosoft.com`).
* **Lure:** "Enjoy a YETI® Rambler Tumbler On Us" — Exploiting the reputation of premium brands to entice clicks.
* **Trust Layer:** Use of the official Starbucks logo (vía Wikimedia) and a professional design to bypass visual scrutiny.
* **Payload:** Multiple CTA buttons (Claim, View Offer, Details) all redirecting to a raw IP destination (`81.171.12.132`).
* **Objective:** Capture of Starbucks Rewards credentials and potentially personal/financial data for exfiltration.

## 3. Technical Indicators of Compromise (IoCs)

| Indicator Type | Value | Note |
| :--- | :--- | :--- |
| **Sender IP** | `185.17.146.229` | Server in Germany (DE); used across multiple phishing campaigns. |
| **Display Name** | `Starbucks Giveaway` | Impersonation of a legitimate promotional event. |
| **From Address** | `info@Starbucksjld.com` | Typosquatted/Look-alike domain mimicking Starbucks. |
| **Return-Path** | `jpcx5@ant20562425.onmicrosoft.com` | Points to a shared malicious Microsoft tenant infrastructure. |
| **Phishing URL** | `hxxp://81[.]171[.]12[.]132/4Xnocw...` | Direct IP destination for the "Giveaway" portal. |
| **Subject Line** | `Your Chance to Get a YETI Rambler Tumbler (On Us) | No. WQO-932668` | Follows the same "Case Number" pattern as previous attacks. |

## 4. Visual Evidence
![Phishing Evidence Starbucks](./Phishing_Evidence_Starbucks.jpg)

## 5. Evasion Techniques & Technical Analysis

1. **Infrastructure Reuse (Campaign Clustering):**
   The threat actor is utilizing the exact same sending server (`185.17.146.229`) and landing page IP (`81.171.12.132`) as the AAA campaign. This indicates a centralized operation running concurrent brand-impersonation templates.

2. **SafeLinks Bypass & Obfuscation:**
   All links are wrapped in **Microsoft SafeLinks**. The attackers leverage the "reputation" of being inside the Microsoft ecosystem (`onmicrosoft.com`) to lower the probability of the email being outright blocked by EOP (Exchange Online Protection).

3. **External Asset Loading:**
   The email loads the Starbucks logo directly from an external Wikimedia URL. This "Living off the Land" technique avoids hosting malicious assets directly, which can sometimes bypass static image analysis.

4. **SCL & Auth Results:**
   Headers show **`spf=fail`** and an **`SCL: 5`**. While Microsoft correctly identified the risk, the message still managed to reach the recipient's Junk folder, where social engineering (urgency/reward) takes over.

---

*Report generated for Cybersecurity Portfolio purposes.*
