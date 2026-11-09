# 🗄️ Data Platform Model

**Control point:** the underlying data platform.

## How it works
Security data stays in **storage the customer controls**, or in an existing enterprise data platform. Security teams search, analyze, and detect against that data without sending everything to an expensive SIEM storage tier.

There are two variants:

| Variant | Description | Examples |
|---|---|---|
| **Object-Storage-Native** | Keeps telemetry in customer-controlled object storage (S3, GCS, Azure Blob) and adds the indexing, search, and detection needed to use it | Scanner, Mitiga |
| **Enterprise-Data-Platform-Native** | Uses an existing lakehouse as the foundation, so security, IT, cloud, and business data are governed together | Databricks |

## Why teams choose it
- More control over security data, retention periods, and long-term storage cost.
- AI systems get access to a much larger collection of historical evidence.
- Organizations can reuse existing data engineering, governance, and AI investments.

## Main risk
**Owning the data doesn't guarantee the SOC can use it.** A strong data platform does not automatically provide a full security operations experience. Teams may still need to build or integrate detections, alert management, analyst search, case management, and response.

## Example vendors
| Vendor | Why it fits | What to test |
|---|---|---|
| Scanner | Indexes logs where they're stored, with fast search, continuous detection, detection-as-code, and MCP access for AI agents | Historical search at scale, alert-to-case handoff, and the engineering effort to keep it all connected |
| Mitiga | Bring-your-own-bucket security data lake that handles normalization, enrichment, detection, AI-assisted triage, and response | How much processing depends on the vendor, and coverage of your key sources |
| Databricks | Security lakehouse reference architecture: collect, normalize, govern, and apply analytics and AI | How much SOC tooling you still need to build around it |

## SACR assessment
Buyers must confirm analysts can **search the data, run detections, and retrieve evidence quickly during a live investigation**, without relying on a data engineer for routine tasks.

[← Back to MSAM overview](../README.md)
