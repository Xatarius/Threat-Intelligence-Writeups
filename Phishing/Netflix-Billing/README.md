# Technical Threat Intelligence Report: Netflix Payment Phishing Campaign
**Date of Analysis:** April 10, 2026
**Analyst:** Roy Castro
**Threat Level:** 🔴 CRITICAL

---

## 1. Executive Summary
A sophisticated phishing campaign has been detected impersonating **Netflix**. The attack leverages urgency-based social engineering ("trouble with your billing") to coerce users into disclosing sensitive financial information. Technically, the campaign is notable for its use of **Zero-Width Characters**, HTML-based logo reconstruction, and the abuse of legitimate infrastructure to bypass modern email security filters (SPF/DKIM).

## 2. Attack Lifecycle (Kill Chain)
1.  **Reconnaissance:** Attackers utilized a pixel-perfect template of official Netflix communications.
2.  **Weaponization:** Integration of a malicious redirect URL hidden behind an "Update Payment" call-to-action button, utilizing a Microsoft "open redirect" to mask the final destination.
3.  **Delivery:** Emails were dispatched via a compromised or misused legitimate domain (`fukusyodo.com`), ensuring high deliverability by passing SPF and DKIM checks.
4.  **Exploitation:** Upon clicking the link, the victim is directed to a credential harvesting landing page designed to steal credit card data and account credentials.

## 3. Technical Indicators of Compromise (IoCs)

| Indicator Type | Value | Description |
| :--- | :--- | :--- |
| **Sender Address** | `cg@fukusyodo.com` | Potentially compromised legitimate domain used for relay. |
| **Reply-To** | `payment@netflix.com` | Spoofed header intended to increase perceived legitimacy. |
| **Source IP** | `209.85.208.195` | Originating Mail Server (Google/Gmail Relay). |
| **Phishing URL** | `https://fukusyodo.com/medical/?&https://go.microsoft.com/fwlink/?linkid=89069...` | Malicious URL leveraging trusted Microsoft redirectors. |
| **Subject** | `Re: Updte Your Payment Information Bill` | Intentional typo ("Updte") used to evade simple keyword filters. |

## 4. Visual Evidence
Captures of the malicious email and the underlying attack structure:

![Netflix1.jpg](Netflix1.jpg)
*Figure 1: Email body masquerading as an official Netflix notification.*

![Netflix2.jpg](Netflix2.jpg)
*Figure 2: Analysis of the malicious link obfuscated behind the action button.*

## 5. Evasion Techniques & Technical Analysis
* **Zero-Width Characters & Homoglyphs:** The attacker embedded invisible characters (e.g., `EF BB BF` or `E2 80 8C`) within the string "Netfl‌ix". This bypasses automated signature-based detection while remaining visually identical to the user.
* **Authentication Bypass:** The email successfully passed `dkim=pass` and `spf=pass`. By utilizing a legitimate domain's infrastructure, the attacker evades reputation-based spam filters.
* **HTML/CSS Logo Obfuscation:** Instead of using a static image file (which could be hashed and blocked), the Netflix logo is reconstructed using a complex HTML table with specific background colors in each cell.
* **URL Masking (Open Redirect):** The inclusion of `go.microsoft.com/fwlink` within the URL string is a tactical move to deceive users who hover over the link, as the initial domain belongs to a trusted entity.
