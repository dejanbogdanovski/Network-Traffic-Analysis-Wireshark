# Network Traffic Analysis - Wireshark Investigation

## Project Overview
This repository contains a comprehensive network forensic analysis of a real-world malware infection scenario. The investigation tracks a **typosquatting** attack where a user was lured to a fraudulent Google Authenticator site. I utilized Wireshark to dissect the traffic, identify the malicious payload, and uncover the attack infrastructure.

---

## Step-by-Step Investigation

### Phase 1: Environment Identification

**Step 1: Capture File Integrity**
The initial phase involved verifying the capture file's metadata and SHA256 hash to ensure a clean forensic starting point.
![Capture Properties](Network%20Traffic%20Analysis%20Wireshark/01_Capture_Properties.png)

**Step 2: Endpoint Identification**
Mapped the local network to identify the victim machine (10.1.17.215) and its communications with external malicious IPs.
![IPv4 Endpoints](Network%20Traffic%20Analysis%20Wireshark/02_IPv4_Endpoints.png)

**Step 3: DNS Statistical Anomaly**
Identified a massive surge in DNS "No such name" errors, signaling automated malicious activity.
![DNS Statistics](Network%20Traffic%20Analysis%20Wireshark/03_DNS_Statistics.png)

---

### Phase 2: Infection Vector & DNS Analysis

**Step 4: Typosquatting Discovery**
Located the infection source: a typosquatted domain authenticatoor.org designed to mimic a legitimate service.
![DNS Queries](Network%20Traffic%20Analysis%20Wireshark/04_DNS_Queries.png)

**Step 5: Malicious IP Resolution**
Extracted the DNS "Answer" section, confirming that the fraudulent domain resolved to the attacker's infrastructure.
![DNS Resolution](Network%20Traffic%20Analysis%20Wireshark/05_DNS_Resolution.png)

---

### Phase 3: Payload Analysis

**Step 6: HTTP Object Extraction**
Isolated and exported several suspicious objects from the traffic, including a PowerShell script and a mysterious file named TV.
![HTTP Payloads](Network%20Traffic%20Analysis%20Wireshark/06_HTTP_Payloads.png)

**Step 7: Script Deconstruction**
Analyzed the TCP stream of the PowerShell script, which revealed functions for downloading additional payloads.
![Script Analysis](Network%20Traffic%20Analysis%20Wireshark/07_Script_Analysis.png)

**Step 8: Binary Header Identification (MZ Signature)**
Deep dive into the TV file revealed it was a Windows executable/DLL identified by the MZ header.
![Binary Header](Network%20Traffic%20Analysis%20Wireshark/08_Binary_Header.png)

---

### Phase 4: Forensic Conclusion

**Step 9: Final Malware Fingerprinting**
The investigation concluded by generating a SHA256 hash of the extracted TV file, providing a definitive Indicator of Compromise (IOC).
![Malware Hash](Network%20Traffic%20Analysis%20Wireshark/09_Malware_Hash.png)

---

## Indicators of Compromise (IOCs)
* **Malicious IPs:** 82.221.136.26, 5.252.153.241
* **Malicious Domains:** authenticatoor.org
* **Payload Hash (SHA256):** 3448DA03808F24568E6181011F8521C0713EA6160EFD05BFF20C43B091FF59F7
