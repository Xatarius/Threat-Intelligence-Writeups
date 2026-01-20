# Technical Threat Intelligence Report: UnitedHealthcare "Rewards" Phishing

**Date of Analysis:** January 20, 2026
**Analyst:** Roy Castro
**Threat Level:** 🟠 Medium-High (Personal Data Theft / Fraud)
**Campaign Status:** Active

---

## 1. Executive Summary
This report analyzes a phishing campaign impersonating **UnitedHealthcare** (UHC). The Threat Actor (TA) utilizes **Microsoft Tenant Abuse** (`onmicrosoft.com` infrastructure) to bypass spam filters. The attack employs a "2026 Rewards Program" lure to drive traffic to a malicious landing page hosted on a **Direct IP address**, evading DNS-based blocklists.

## 2. Attack Lifecycle (Kill Chain)
* **Initial Vector:** Email sent via a fraudulent Microsoft 365 Tenant (`den19954040.onmicrosoft.com`).
* **Lure:** "A Special Thank You – 2026" (Exclusive Reward).
* **Trust Layer:** Abuse of Microsoft's legitimate sending infrastructure to obtain passing SPF checks relative to the tenant.
* **Payload:** Direct HTTP links to a raw IP address (`81.171.12.132`).
* **Objective:** Theft of PII (Personally Identifiable Information) and Member Portal Credentials.

## 3. Technical Indicators of Compromise (IoCs)

| Indicator Type | Value | Context |
| :--- | :--- | :--- |
| **Sender Address** | `UHC@UnitedHealthcareuuv[.]com` | Typosquatting Domain (Extra "uuv" suffix). |
| **Sending Infrastructure** | `den19954040.onmicrosoft.com` | **Microsoft Tenant Abuse**. The attacker spun up a trial/throwaway tenant to send mail. |
| **Malicious IP (Payload)** | `81[.]171[.]12[.]132` | **Direct IP Abuse**. Hosting phishing kit without a domain name. |
| **Subject Line** | `Your UnitedHealthcare Rewards Program Has New Options` | Benefit/Reward Lure. |

## 4. Visual Evidence

**Figure 1: The Lure**
The email uses the official UHC color palette and logo. It employs a "Benefit Claim" strategy ("Explore Your Reward") rather than fear. Note the clean layout designed to look like an automated corporate notification.

![UnitedHealthcare Phishing Evidence](Phishing_Evidence_UHC.jpg)

## 5. Technical Analysis & Evasion Techniques

### A. Microsoft Tenant Abuse (onmicrosoft.com)
The headers reveal the email originated from `den19954040.onmicrosoft.com`.
* **Technique:** Attackers register free or trial Microsoft 365 tenants. By sending emails through this infrastructure, they leverage Microsoft's IP reputation. While the `From` address (`UnitedHealthcareuuv.com`) might fail alignment, the *Envelope Sender* (`...onmicrosoft.com`) passes authentication, confusing many Secure Email Gateways (SEGs).

### B. Direct IP Linking (Naked IP)
All call-to-action links in the email point directly to `http://81.171.12.132/...` wrapped in Outlook Safelinks.
* **Evasion:** By using a raw IP address instead of a domain name, the attacker avoids **Domain-based Reputation Filtering**. Since there is no domain to register or analyze, they bypass "newly registered domain" flags. However, this is distinct "poor tradecraft" as legitimate organizations rarely link to raw IPs.

### C. Typosquatting
The visible sender domain is `UnitedHealthcareuuv.com`. This closely resembles the legitimate `UnitedHealthcare.com` but includes a subtle suffix ("uuv") intended to be overlooked by users skimming the header on mobile devices.

---

*Report generated for Cybersecurity Portfolio purposes. Analysis based on headers and body artifacts from a live sample.*
