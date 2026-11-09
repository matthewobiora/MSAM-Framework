# 🧩 Converged SIEM/XDR Model

**Control point:** the integrated security platform.

## How it works
The Converged model brings more of the SOC into one security platform. SIEM, XDR, detection, threat intelligence, investigations, cases, automation, and response all work through a shared operating environment.

## Why teams choose it
- Analysts spend less time moving alerts and context between tools.
- An investigation can start with a detection, pull in endpoint or identity evidence, become a case, and end in a response action, all without rebuilding the story in several systems.
- AI gets a more coherent working environment when evidence, permissions, case history, and available actions are governed in one place.

## Main risk
**Consolidation changes the buyer's risk.** The more detection content, case history, automation logic, and analyst workflow become native to one platform, the less realistic it is to replace only one part of the stack.

## Example vendors
| Vendor | Why it fits | What to test |
|---|---|---|
| Microsoft Sentinel | Connects SIEM with detection, investigation, and automation across the wider Microsoft security ecosystem | Whether third-party evidence and non-Microsoft response actions get the same depth of support |
| CrowdStrike Falcon Next-Gen SIEM | Extends the Falcon platform with third-party telemetry, threat intel, cases, automation, and AI | Whether the experience stays as strong when investigations move beyond Falcon-native data |
| Palo Alto Networks Cortex XSIAM | Combines SIEM, XDR, analytics, automation, and response around a central data foundation | How tightly schemas, workflows, and playbooks become tied to Cortex |
| Exaforce | One SOC platform whose data layer connects cloud, identity, and SaaS sources for analysts and AI agents | Detection coverage on your sources, and whether AI decisions trace back to evidence |
| Anomali | A security data lake combined with ThreatStream intelligence and agentic operations | How the data layer supports detection, investigation, and response together |
| SentinelOne Singularity AI SIEM | Endpoint, cloud, identity, and third-party telemetry with Purple AI investigations; also overlaps Pipeline-First | How well its data pipeline features work for normalization and routing |
| Daylight Security | A *service-led* variant: detection engineering, data lake, agentic investigation, and human expertise delivered as managed services | How portable context and detection logic remain if you change providers |

## SACR assessment
Converged architectures can reduce integration burden and simplify how the SOC operates. The main risk is platform dependence: as more data, detections, cases, automation, and AI workflows move into one platform, replacing individual capabilities becomes harder.

[← Back to MSAM overview](../README.md)
