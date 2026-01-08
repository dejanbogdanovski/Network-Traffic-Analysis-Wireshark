# Network Traffic Analysis - Wireshark Investigation

## Project Overview
This repository contains a comprehensive network forensic analysis of a real-world malware infection scenario. The investigation tracks a **typosquatting** attack where a user was lured to a fraudulent Google Authenticator site. I utilized Wireshark to dissect the traffic, identify the malicious payload, and uncover the attack infrastructure.

---

## Step-by-Step Investigation

### Phase 1: Environment Identification

**Step 1: Capture File Integrity**
The initial phase involved verifying the capture file's metadata and SHA256 hash.
![Capture Properties](Network Traffic Analysis Wireshark/01_Capture_Properties.png)

**Step 2: Endpoint Identification**
Mapped the local network to identify the victim machine and external malicious IPs.
![IPv4 Endpoints](Network Traffic Analysis Wireshark/02_IPv4_Endpoints.png)

**Step 3: DNS Statistical Anomaly**
Identified a massive surge in DNS "No such name" errors.
![DNS Statistics](Network Traffic Analysis Wireshark/03_DNS_Statistics.png)

---

### Phase 2: Infection Vector & DNS Analysis

**Step 4: Typosquatting Discovery**
Located the infection source: a typosquatted domain `authenticatoor.org`.
![DNS Queries](Network Traffic Analysis Wireshark/04_DNS_Queries.png)

**Step 5: Malicious IP Resolution**
Confirmed that the domain resolved to the attacker's infrastructure at `82.221.136.26`.
![DNS Resolution](Network Traffic Analysis Wireshark/05_DNS_Resolution.png)

---

### Phase 3: Payload Analysis

**Step 6: HTTP Object Extraction**
Isolated and exported suspicious objects like `29842.ps1` and `TV`.
![HTTP Payloads](Network Traffic Analysis Wireshark/06_HTTP_Payloads.png)

**Step 7: Script Deconstruction**
Analyzed the PowerShell script which revealed the downloader function.
![Script Analysis](Network Traffic Analysis Wireshark/07_Script_Analysis.png)

**Step 8: Binary Header Identification**
Confirmed the **MZ signature** on the file named `TV`.
![Binary Header](Network Traffic Analysis Wireshark/08_Binary_Header.png)

---

### Phase 4: Forensic Conclusion

**Step 9: Final Malware Fingerprinting**
Generated a SHA256 hash of the extracted `TV` file as a definitive IOC.
![Malware Hash](Network Traffic Analysis Wireshark/09_Malware_Hash.png)

---
