# SOC + SOAR Automation Lab

**End-to-end automated detection, enrichment and case management**

**Stack:** Wazuh (SIEM) · Shuffle (SOAR) · VirusTotal · TheHive · Windows 10 + Sysmon

---

## Overview

A full SOC + SOAR pipeline built from scratch in a homelab, modelled on the
detection-and-response workflow of a real Security Operations Center.

The environment detects a credential theft attempt (Mimikatz), enriches the
alert against VirusTotal, and automatically opens a case in TheHive with
observables and MITRE mapping attached — with no analyst in the loop.

**What it covers:** detection engineering · automation orchestration · threat
intelligence enrichment · incident response workflow design · SIEM + SOAR +
case management integration.

![SOAR workflow](screenshots/SOAR1.jpg)

---

## Architecture

### Wazuh — SIEM

Collects telemetry from the Windows agent: Sysmon events, Security logs,
process creation, and command-line arguments. Fires an alert when Mimikatz
execution is detected.

### Shuffle — SOAR

The automation layer. Receives the Wazuh alert via webhook, extracts the file
hash, queries VirusTotal, applies routing logic to classify the result, and
creates a TheHive case with the full observable set.

### VirusTotal — enrichment

File reputation and detection ratio for the binary executed on the endpoint.

### TheHive — case management

Receives the automated case: title, description, severity, MITRE technique
(T1003 — OS Credential Dumping), observables, and timestamps.

![Enrichment and case creation](screenshots/SOAR3.jpg)

---

## Attack simulated

**Credential theft — Mimikatz execution**

| Stage | What happens |
|---|---|
| Execution | Mimikatz runs on the Windows endpoint |
| Telemetry | Sysmon Event ID 1 (process creation) with command line |
| Detection | Wazuh rule matches on process name and signature |
| Enrichment | Shuffle queries VirusTotal for the file hash |
| Case | TheHive case opened, mapped to T1003 — OS Credential Dumping |

---

## What I learned

- How SIEMs and SOARs share structured alert data
- Designing scalable, modular SOAR playbooks
- Implementing automated threat-intelligence enrichment
- Mapping detections to MITRE ATT&CK
- Reducing alert fatigue with rule tuning
- Real-world IR workflow: detect → enrich → investigate → contain

> **Fill this in.** These are your original bullets. They're accurate but
> generic — they'd fit any SOAR lab. The version that survives an interview
> names one specific thing: a field mapping that broke, an enrichment result
> that was misleading, a workflow step you had to rebuild. Replace these with
> what actually happened and delete this note.

---

## Defensive recommendations

Based on the attack path exercised here:

- Restrict LSASS access — Credential Guard, RunAsPPL
- EDR protections specifically targeting credential dumping
- Monitor high-value Event IDs: 4624 (logon), 4672 (special privileges assigned), 4688 (process creation)
- Application control via AppLocker or WDAC
- MFA and least privilege
- Regular patch cycle for the OS and security subsystems

---

## Limitations

Single Windows endpoint lab. One enrichment source (VirusTotal). Wazuh rules
are tuned against one machine's baseline and would need rework against
enterprise log volume. Response is detect-and-document only — the containment
actions listed under Future improvements are not implemented.

---

## Future improvements

- Cortex analyzers for deeper enrichment
- MISP threat feed ingestion
- Containment actions — disable user, block IP, isolate host
- Sigma → Wazuh rule generation pipeline

---

## Repo contents

```
├── configs/
│   ├── shuffle-workflow.json    # Shuffle workflow export
│   ├── wazuh-sample-alert.json  # Alert that triggers the pipeline
│   └── virustotal-request.json  # Enrichment request body
├── docs/
│   ├── methodology.md           # How the lab was built, in order
│   ├── soar-logic.md            # Routing and classification logic
│   └── prevention.md            # Defensive controls in depth
└── screenshots/
```

© 2025 Chirayu Paliwal
