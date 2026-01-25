# Technical Threat Intelligence Report: "iCloud Storage" Phishing Campaign

**Date of Analysis:** January 21, 2026
**Analyst:** Roy Castro
**Threat Level:** 🔴 High (Credential Harvesting & Account Takeover)

---

## 1. Executive Summary
This report documents a deceptive phishing campaign targeting Apple users. The threat actor (TA) exploits **Google Cloud Storage** public buckets to host malicious assets. By leveraging the high reputation of the `googleapis.com` domain, the campaign successfully bypasses standard Secure Email Gateway (SEG) reputation filters and delivers credential harvesting payloads directly to the inbox.

## 2. Attack Lifecycle (Kill Chain)
* **Initial Vector:** Phishing email sent via a spoofed/relayed address using Google's SMTP infrastructure.
* **Lure:** "Cloud Storage Full" notification threatening data loss (photos/backups).
* **Trust Layer:** Google Cloud Storage (`storage.googleapis.com`) used as a reputation shield.
* **Abused Infrastructure:** Public Cloud Bucket hosting a malicious `.html` file.
* **Final Destination:** Fake Apple ID login portal rendered directly from the cloud storage link.

## 3. Technical Indicators of Compromise (IoCs)

| Indicator Type | Value |
| :--- | :--- |
| **Sender Address** | `zzpu7@slyidqbdxrotf.returnpathwtf.com.tr` |
| **Sender IP** | `209.85.216.54` (Google Relay) |
| **Phishing URL** | `hxxps://storage[.]googleapis[.]com/liveislive/STRGADVNWFMRKT01.html` |
| **Subject Line** | `Importante: lo spazio di archiviazione nel cloud è quasi pieno. ID#08165` |
| **Abused SaaS** | Google Cloud Storage (GCP) |

## 4. Visual Evidence
![Phishing Email Evidence](./Phishing_Evidence_iCloud.jpg)

## 5. Evasion Techniques & Technical Analysis

1.  **PaaS Abuse (Living off the Land):** The attacker hosted the malicious landing page (`STRGADVNWFMRKT01.html`) on a public Google Cloud Storage bucket. Security filters often whitelist `*.googleapis.com` domains to prevent disrupting legitimate business operations, allowing the phishing link to pass through.

2.  **Reputation Hijacking:** Similar to the Eventbrite case, the attacker does not use a newly registered domain (which would be flagged). Instead, they piggyback on Google's domain authority to lend technical legitimacy to the malicious link.

3.  **Static Content Evasion:** By using a `.html` file hosted directly on cloud storage rather than a complex PHP backend on a compromised server, the payload appears as static content, which is often subjected to less rigorous scanning by automated security tools.

4.  **Psychological Manipulation & Urgency:** The email employs a "loss aversion" trigger. By warning that "email and file synchronization may stop" and showing a visual progress bar near 100%, the attacker forces a hasty decision, bypassing critical thinking.

5.  **Spoofing & Relaying:** The email passed SPF checks because it was routed through Google's legitimate mail servers (`mail-pj1-f54.google.com`), despite the `Return-Path` pointing to the highly suspicious Turkish domain `returnpathwtf.com.tr`. This indicates the use of a compromised or burner Gmail account to relay the message.

---

*Report generated for Cybersecurity Portfolio purposes.*
