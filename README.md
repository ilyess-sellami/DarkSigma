# 🕵️ DarkSigma

**DarkSigma** is a cybersecurity research and detection engineering project focused on monitoring, detecting, and analyzing **Dark Web–related threats**.  
The project’s goal is to provide a structured detection framework that can be translated into **Splunk**, **ELK/Sigma**, and **Wazuh** rules, and tested against synthetic and real-world logs.  

---

## 🎯 Project Objectives
- Define a **taxonomy of Dark Web threats** with professional categories.  
- Map each category to **MITRE ATT&CK tactics and techniques**.  
- Assign **severity levels** to prioritize detection and response.  
- Develop **30+ professional detection rules** for `.onion` access, marketplaces, credentials leaks, malware distribution, and more.  
- Convert the rules to **Splunk SPL**, **Sigma (for ELK)**, and **Wazuh** formats.  
- Validate detections with **synthetic test logs** and real-world threat intel.  

---

## 🔥 Dark Web Threat Categories → ATT&CK Mapping

| # | Dark Web Category | Primary ATT&CK Tactic(s) | Example Techniques | Severity |
|---|-------------------|--------------------------|--------------------|----------|
| 1 | **Web Access & Network Layer** (.onion, Tor gateways, UA anomalies) | Command & Control (C2), Reconnaissance, Defense Evasion | C2 via Web (T1071.001), Ingress Tool Transfer (T1105) | **High** |
| 2 | **Dark Web Marketplaces & Forums** | Collection, Resource Development, Exfiltration | Acquire Infrastructure (T1583), Data from Information Repositories | **High** |
| 3 | **Credentials & Data Exposure** | Credential Access, Collection, Impact | Credential Dumping (T1003), Valid Accounts (T1078) | **Critical** |
| 4 | **Malware & Exploit Distribution** | Initial Access, Execution, C2, Defense Evasion | Drive-by Compromise (T1189), Exploit Public-Facing App (T1190) | **Critical** |
| 5 | **Financial Crimes** (crypto mixers, carding, cashout) | Exfiltration, Impact, Command & Control | Exfiltration Over Web (T1041), Data Staged (T1074) | **High** |
| 6 | **Supply-chain / Service Abuse** | Supply Chain Compromise, Persistence, Defense Evasion | Compromise Software Supply Chain (T1195), Signed Binary Proxy Execution | **Critical** |
| 7 | **Insider / Recruitment Scams** | Initial Access, Impact, Collection | Valid Accounts (T1078), Spearphishing Attachment (T1193) | **High** |

---
## ⚙️ Sigma CLI Installation

1. Install Python 3.9+ and pip if not already installed.
2. Install Sigma CLI:
```bash
pip install sigma-cli
```
3. Confirm installation:
```bash
sigma -h
```
4. Optionally, list available backend targets:
```bash
sigma list targets
```
Typical backends: `splunk`, `lucene`, `eql`, `esql`, `elastalert`.

📝 Adding Your Rules
1. Place your Sigma `.yml` rule files in a structured folder:
```bash
rules/
 ├─ 01_web_access/
 ├─ 02_marketplaces/
 ├─ 03_credentials_and_data_exposure/
 └─ ...
```
Each folder should contain `.yml` rules for that category (e.g., `001_darkweb_onion_access.yml`).

---

## 🔄 Converting Rules with Sigma CLI
```bash
mkdir -p converted_rules/<backend>
sigma convert -t <backend> rules/01_web_access/*.yml -o converted_rules/<backend>/01_web_access.spl --without-pipeline
```

---

## ⚠️ Disclaimer
DarkSigma is a **research and educational project**.  
It does **not** provide access to Dark Web resources and does not encourage their use.  
All detections are built for **defensive cybersecurity purposes only**.  
