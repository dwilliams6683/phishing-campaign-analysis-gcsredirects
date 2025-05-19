Phishing Campaign Using Google Cloud Storage Redirects

🧠 Background

This repository documents a phishing/spam campaign observed in 2025 that utilized base64-encoded HTML emails and Google Cloud Storage (GCS) links as initial redirection points. The campaign aimed to lure users with fake giveaways or surveys and included spoofed unsubscribe links that may have been used for email harvesting.

⚠️ This is a retrospective analysis. Due to the transient nature of the campaign infrastructure, indicators of compromise (IOCs) were not preserved. The methodology and findings outlined below are reconstructed based on hands-on investigation during the live period.

🔍 Key Characteristics

Email Body: Entire body encoded in base64

Initial Redirect: https://storage.googleapis.com buckets

Dynamic Content: Redirect destinations loaded via # hash fragments and JavaScript

Secondary Domains: Used randomized subdomains on domains like *.nikkeibp.org

Spoofed Unsubscribe Links: Redirected to https://opt-out-me.com, likely used for email validation or harvesting

Visual Theme: Disguised as promotional content, such as giveaways or surveys

📊 Methodology (Reconstructed)

1. Base64 Decoding

Extracted base64-encoded body from sample emails

Decoded into human-readable HTML using Python

2. Link Extraction

Parsed decoded HTML for embedded https:// links

Focused on links beginning with https://storage.googleapis.com/

3. Redirect Chain Observation

Opened extracted links in browser with Developer Tools active

Observed JavaScript extracting values from # hash fragments

Confirmed dynamic redirection to secondary domains (e.g., https://8char.nikkeibp.org)

4. Behavioral Analysis

Noted rapid disappearance or expiration of redirect targets

Redirection sequence designed to appear legitimate (e.g., loading indicators, brief delays)

5. Heuristics and Pattern Matching

Secondary domains followed a consistent 8-character subdomain pattern

"Unsubscribe" links consistently pointed to third-party domain, not sender

Suggests mass campaign using rotating infrastructure

🤔 Insights & Hypotheses

Use of Trusted Domains: Starting redirection chain on storage.googleapis.com likely intended to bypass email filters and antivirus scanners

Dynamic Hash Fragment Usage: Makes traditional IOC matching less effective; harder for automated systems to detect malicious behavior

Spoofed Opt-Out Links: May be used to validate active email addresses, increasing value of target lists

Volatile Infrastructure: Links and destinations became inactive quickly, suggesting ephemeral hosting or automation

🛠️ Tools Used

Python (base64 decoding, link parsing)

Browser Developer Tools (redirect tracing, JavaScript behavior)

curl / wget (manual URL testing)

📌 Lessons Learned

Even when a campaign's IOCs cannot be preserved, documenting its tactics, techniques, and procedures (TTPs) offers lasting value. Reconstructing behavioral analysis allows others to build detection strategies based on methodology rather than fixed indicators.

This approach encourages:

Security awareness

Heuristic-based detection

Improved understanding of spam and scam distribution mechanisms

🌐 Related Topics

Phishing Redirection Chains

Email Base64 Encoding Tactics

Dynamic JavaScript-Based Redirects

Trusted Domain Abuse in Email Campaigns

📄 Disclaimer

This repository is for educational and awareness purposes only. No live malicious content is hosted here, and all analysis is based on publicly observable behavior at the time of investigation.

💡 Future Work

Add example decoder script for base64 HTML extraction

Create flowchart of redirection chain

Compare to other known redirect-based phishing campaigns
