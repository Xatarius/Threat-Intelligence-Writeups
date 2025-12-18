# Technical Threat Intelligence Report: "Correos de Costa Rica" Phishing Campaign

**Date of Analysis:** December 18, 2025
**Analyst:** [Tu Nombre o Nickname]
**Threat Level:** 🔴 High (Identity Theft & Financial Fraud)

---

## 1. Executive Summary
This report documents a sophisticated phishing campaign targeting users in Costa Rica. The threat actor (TA) utilizes a complex redirection chain, leveraging the legitimate infrastructure of **Eventbrite** to bypass email security filters (SPF/DKIM). 

## 2. Attack Lifecycle (Kill Chain)
* **Initial Vector:** Phishing email delivered via Eventbrite's official notification system.
* **Lure:** Notification of a "pending package delivery" requiring a fee of **₡3,500**.
* **Trust Layer:** Legitimate Eventbrite ticket page used as a reputation shield.
* **Compromised Host:** Redirected through a hijacked site in the UAE (`citymaids.ae`).
* **Final Destination:** Phishing Kit hosted on `saharforexport.com`.

## 3. Technical Indicators of Compromise (IoCs)

| Indicator Type | Value |
| :--- | :--- |
| **Malicious Domain** | `saharforexport.com` |
| **Server IP** | `65.181.111.248` (Buffalo, US) |
| **Phishing URL** | `https://saharforexport.com/doku/app/index.php?view=main` |
| **Redirector** | `https://citymaids.ae/voeventgfd/` |
| **Abused SaaS** | `eventbrite.com.mx` |

## 4. Visual Evidence
![Phishing Site Clone](VisualEvidence.jpeg)

## 5. Evasion Techniques & Technical Analysis

1. **SaaS Infrastructure Abuse (Living off the Land):** The attacker exploited Eventbrite's legitimate mailing infrastructure. This ensures the email passes **SPF** and **DKIM** authentication checks, allowing the message to bypass traditional spam filters and land directly in the inbox.

2. **Reputation Hijacking:** By utilizing `eventbrite.com.mx` as the initial landing point, the attacker leverages the high "domain authority" of a trusted platform to mask the subsequent malicious redirects.

3. **Compromised CMS Hosting:** The phishing kit is hosted on a hijacked legitimate website (`saharforexport.com`). Attackers frequently exploit vulnerabilities in outdated WordPress or DokuWiki installations to host malicious files in hidden directories like `/doku/app/`.

4. **Micro-Transaction Psychology:** The request for a small fee (**₡3,500**) is a deliberate "low-friction" tactic. It minimizes victim suspicion while successfully exfiltrating high-value credit card data (PAN, CVV, Expiry).

5. **Individual Target Tracking:** The use of a unique hash ID (`id=0e0c4bc3...`) in the URL allows the threat actor to verify which specific email accounts are active and vulnerable, facilitating future "spear-phishing" attempts.

---
*Report generated for Cybersecurity Portfolio purposes.*