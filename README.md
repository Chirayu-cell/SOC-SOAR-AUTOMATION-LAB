🔥 SOC + SOAR Automation Lab
End-to-End Automated Incident Detection, Enrichment & Case Management

Stack: Wazuh (SIEM) • Shuffle (SOAR) • VirusTotal • TheHive • Windows 10 + Sysmon

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

📌 Overview

This project is a full enterprise-style SOC + SOAR pipeline, built completely from scratch.
It simulates a real-world detection and automated response workflow used by Security Operations Centers.

The environment detects credential theft attempts (Mimikatz), enriches the alert using VirusTotal, and automatically creates a case inside TheHive for further investigation — all without analyst involvement.

This project showcases key skills in:

Detection engineering

Automation orchestration

Threat intelligence enrichment

Incident response workflow design

SIEM + SOAR + Case Management integration

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

🏆 Key Achievements

✔ Reduced manual triage by ~80% using fully automated SOAR playbooks
✔ Integrated SIEM + SOAR + Threat Intel + Case Management
✔ Automated alert enrichment using VirusTotal
✔ Created structured cases in TheHive for analyst workflows
✔ Fine-tuned Wazuh rules to remove noise and improve detection fidelity
✔ Simulated real-world credential theft attack using Mimikatz
✔ Significantly improved MTTD & MTTR through automation

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

🏗️ Architecture
🔹 Wazuh (SIEM)

Collects telemetry from Windows agent:

Sysmon logs

Security logs

Process creation

Suspicious command line usage

Triggers alert when Mimikatz is executed.

🔹 Shuffle (SOAR)

Automates the entire workflow:

Receives Wazuh alert via webhook

Extracts file hash

Queries VirusTotal API

Applies logic to determine malicious/benign

Creates a case in TheHive with full observable details

🔹 VirusTotal

Provides threat intelligence for the file executed on the endpoint.

🔹 TheHive

Acts as the central case management platform.
Automatically populated with:

Title

Description

Severity

TTP mapping (ex: T1003 — Credential Dumping)

Observables

Timestamps

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

🧪 Attack Simulated
Credential Theft Attempt — Mimikatz Execution

Triggers Sysmon Event ID 1 (process creation)

Wazuh rule detects suspicious process name & signature

Shuffle enriches with VirusTotal metadata

TheHive automatically logs case with MITRE mapping:

T1003 — OS Credential Dumping

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

💡 What I Learned

How SIEMs and SOARs share structured alert data

Designing scalable, modular SOAR playbooks

Implementing automated threat-intelligence enrichment

Mapping detections to MITRE ATT&CK

Reducing alert fatigue with rule tuning

Real-world IR workflow:
Detect → Enrich → Investigate → Contain

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

🛡️ Defensive Recommendations (Based on Attack)

Restrict LSASS access with Credential Guard / RunAsPPL

EDR protections against credential dumping

Monitor high-value Event IDs:

4624 – Logon

4672 – Special privileges assigned

4688 – Process creation

Application control (AppLocker / WDAC)

MFA + Least Privilege

Regular patch cycle for OS + security subsystems

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

🚀 Future Improvements

Add Cortex analyzers for deeper enrichment

Add MISP threat feed ingestion

Expand workflows to include containment (disable user, block IP, isolate host)

Add Sigma → Wazuh rule generation pipeline

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

✨ About This Project

This project was built to gain real-world SOC experience:
from intrusion detection → enrichment → automated response → case creation.

It demonstrates deep hands-on ability with modern blue-team technologies and automated incident response engineering.

If you like this project, feel free to ⭐ star the repository!
