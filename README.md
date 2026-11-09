# MSAM: Modern SIEM Architecture Models

**A framework for classifying and evaluating SIEM architectures as security data spreads out and AI agents join the SOC.**

![Framework](https://img.shields.io/badge/Framework-MSAM-2F81F7?style=flat-square)
![Domain](https://img.shields.io/badge/Domain-SIEM_%7C_SecOps_%7C_AI_SOC-6E40C9?style=flat-square)
![Published](https://img.shields.io/badge/Published-SACR_Oct_2026-FF6719?style=flat-square&logo=substack&logoColor=white)
![Author](https://img.shields.io/badge/Author-Uche_Obiora-0A66C2?style=flat-square&logo=linkedin&logoColor=white)

> 📖 **Full report:** [*The SIEM Problem Has Become an Architecture Problem*](https://softwareanalyst.substack.com/p/the-siem-problem-has-become-an-architecture), Software Analyst Cyber Research (SACR), October 2026.
>
> This repository is a structured, practitioner-friendly companion to that report: the framework, the five models, and a decision and proof-of-concept (POC) toolkit security teams can reuse.

---

## Why MSAM?

The traditional SIEM ran on one idea: **centralize everything**. Collect telemetry, index it, run detections, and investigate in the same system. That model is under strain:

| Pressure | What happens |
|---|---|
| **Cost shapes visibility** | Teams filter, sample, or drop telemetry to control ingestion and retention costs, which creates blind spots before an investigation even starts. |
| **Search speed is now part of incident response** | Slow or expensive historical searches delay triage and limit how far analysts can follow an attack. |
| **Detection engineering is a system** | Rules must be written, tested, tuned, deployed, and measured continuously. |
| **AI is a new class of analyst** | Agents need governed data access, visible reasoning, and controlled authority to act. |

So the question is no longer *"Which SIEM should we buy?"* It is **"Where should control over our security data sit?"**

> **Thesis:** The strongest SIEM architectures will give analysts and AI fast, trustworthy access to the evidence they need, while keeping control over cost, data ownership, response authority, and portability.

---

## The Framework at a Glance

MSAM classifies architectures by **where the primary control point sits**:

```mermaid
flowchart TB
    Q{"Where does the primary<br/>control point sit?"}
    Q --> C["🧩 Converged<br/>Integrated security platform"]
    Q --> O["📈 Observability-Connected<br/>Observability platform"]
    Q --> P["🔀 Pipeline-First<br/>Security data pipeline"]
    Q --> D["🗄️ Data Platform<br/>Underlying data platform"]
    Q --> F["🌐 Federated<br/>Federated access layer"]
```

| Model | Control point | Best fit | Main risk | Examples |
|---|---|---|---|---|
| [**Converged**](models/01-converged.md) | Integrated security platform (SIEM + XDR + cases + AI + response) | Teams that want fewer tools and a single operating environment | Platform dependence and lock-in | Microsoft Sentinel, CrowdStrike Falcon Next-Gen SIEM, Palo Alto Cortex XSIAM, SentinelOne, Exaforce, Anomali, Daylight |
| [**Observability-Connected**](models/02-observability-connected.md) | Observability platform shared with engineering | Cloud-native orgs already standardized on one telemetry platform | Dependence on the observability platform's pricing, retention, and availability | Datadog Cloud SIEM |
| [**Pipeline-First**](models/03-pipeline-first.md) | Security data pipeline (filter, enrich, normalize, route) | Teams fighting ingestion costs or feeding many destinations | A bad filter creates blind spots across every downstream tool | Cribl, Brava |
| [**Data Platform**](models/04-data-platform.md) | Customer-controlled object storage or enterprise lakehouse | Orgs retaining large volumes of history that want to own their data | Owning data does not mean the SOC can use it fast | Scanner, Mitiga, Databricks |
| [**Federated**](models/05-federated.md) | Federated access layer that searches data where it lives | Large enterprises that cannot centralize (cost, regulation, M&A) | One search box can hide missing sources | Vega, 7AI, Artemis |

> Models overlap. Many vendors span more than one, and some enterprises combine several on purpose; a pipeline can feed a data platform while a federated layer searches it alongside an existing SIEM. **Vendors are classified by their dominant architectural control point.** Inclusion is illustrative, not an endorsement or ranking.

---

## Two Decisions Underneath Every Model

Every MSAM model is a mix of two deeper architecture choices:

| Decision | Option A | Option B | The trade-off |
|---|---|---|---|
| **1. Data plane** | **Customer-controlled:** tools operate across data you own | **Platform-controlled:** one vendor manages the full lifecycle | Control and portability vs. engineering load |
| **2. Operating model** | **Composable:** each component integrated independently | **Converged:** functions share one operating environment | Flexibility vs. simplicity and platform dependence |

1. **Data plane: customer-controlled or platform-controlled?** Owning the data plane gives you control over retention, portability, and storage cost, but your team manages integrations, schemas, permissions, and detections. A platform-controlled data plane cuts engineering work but deepens dependence.
2. **Operating model: composable or converged?** Composable stacks let you swap components (pipelines, storage, detections, cases, response, AI), but need strong integration and governance. Converged platforms simplify daily operations, but tie more of the SOC to one vendor's economics and direction.

The right balance depends on **team size, engineering capacity, existing investments, regulatory requirements, and data-control needs**.

---

## The Trusted SOC Test

Whatever model you pick, the architecture must keep this loop intact:

```mermaid
flowchart LR
    E["<b>Evidence</b><br/>What happened?<br/>Can it be traced?"] --> D["<b>Decision</b><br/>What should be<br/>done, and why?"]
    D --> A["<b>Authority & Action</b><br/>Who or what was<br/>allowed to act?"]
    A --> V["<b>Verification</b><br/>Did the intended<br/>outcome occur?"]
    V --> I["<b>Improvement</b><br/>What changes in the<br/>architecture next?"]
    I -. feeds the next investigation .-> E
```

A false positive, a rejected AI recommendation, or a failed response action should feed back into detection logic, data policy, case workflow, or automation scope. It shouldn't just get closed out.

---

## The New SOC Data Architecture

The SIEM no longer has to own every layer of the security data lifecycle:

```mermaid
flowchart LR
    subgraph SRC[Sources]
        direction TB
        s1[Endpoint] ~~~ s2[Identity] ~~~ s3[Network] ~~~ s4[Cloud] ~~~ s5[Application] ~~~ s6[Firewall]
    end
    subgraph PIPE[Routing & control]
        direction TB
        p1[Collect] --> p2[Filter] --> p3[Normalize] --> p4[Enrich] --> p5[Route]
    end
    subgraph TIER[Security data layer]
        direction TB
        h["🔥 <b>Hot</b><br/>SIEM / indexed<br/>real-time detection"]
        w["🌤️ <b>Warm</b><br/>Searchable lake<br/>threat hunting"]
        c["🧊 <b>Cold</b><br/>Object storage<br/>long-term evidence"]
    end
    subgraph DET[Detection & investigation]
        direction TB
        d1["Detection<br/>SIEM rules · XDR · detection-as-code<br/>historical · AI-assisted"]
        d2["Investigation & case<br/>triage · evidence · federated context via MCP<br/>human + AI investigation"]
        d1 --> d2
    end
    subgraph RESP[Response & AI ops]
        direction TB
        r1[AI recommendation] --> r2[Human approval] --> r3[Response action] --> r4[Verification & record]
    end
    SRC --> PIPE --> TIER --> DET --> RESP
```

| Tier | Purpose | Typical data |
|---|---|---|
| **Hot** | Real-time detection, active investigations, frequent searches | EDR alerts, auth/identity events, firewall/WAF, high-priority cloud security logs |
| **Warm** | Incident response and threat hunting | Older identity logs, DNS, network flow, cloud control-plane, application logs |
| **Cold** | Compliance, forensics, long-term investigations | Archived raw logs, historical cloud activity, audit records |

---

## Repository Contents

| Path | What's inside |
|---|---|
| [`models/`](models/) | One page per model: how it works, strengths, risks, example vendors, and what to validate |
| [`decision-guide.md`](decision-guide.md) | The four architecture decisions, metrics to track, failure tests, and a 30/60/90-day plan |
| [`poc-checklist.md`](poc-checklist.md) | A copy-and-use checklist for SIEM proofs of concept |
| [`CITATION.cff`](CITATION.cff) | Citation metadata. Use **"Cite this repository"** in the sidebar |

---

## Author

**Uche Obiora** is a Security Research Analyst at Software Analyst Cyber Research (SACR), researching SIEM modernization, AI-driven security operations, and identity security.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/uche-obiora-058631217/)
[![Substack](https://img.shields.io/badge/Substack-@uche222-FF6719?style=flat-square&logo=substack&logoColor=white)](https://substack.com/@uche222)
[![GitHub](https://img.shields.io/badge/GitHub-matthewobiora-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/matthewobiora)

<sub>MSAM was first published by Software Analyst Cyber Research (SACR). Vendor examples come from that research and are illustrative, not rankings or procurement recommendations. Vendor-reported performance figures should be validated in your own environment.</sub>
