# ✅ SIEM POC Checklist

Copy this into your own tracker and fill it in for each candidate platform. Set pass/fail thresholds **before** testing starts.

**Candidate:** `__________` &nbsp;&nbsp; **MSAM model(s):** `__________` &nbsp;&nbsp; **Baseline date:** `__________`

---

### 1. Evidence & search
- [ ] **Historical search performance:** realistic investigations across 6–12 months of production-scale data (full-text, identity correlation, rare indicators, aggregations, concurrent analyst queries)
- [ ] Query latency at 90- and 365-day lookbacks: `____ s` / `____ s`
- [ ] Indexed vs. federated / search-in-place results compared for the same investigation
- [ ] **Native vs. external evidence:** investigation quality compared for platform-native, third-party, and federated data
- [ ] Missing source or pipeline delay is clearly **flagged** to analysts and agents
- [ ] Log-gap rate measured: `____ %`

### 2. Detection operations
- [ ] Existing detections replayed against historical data
- [ ] Continuous detections, historical backtesting, and detection-as-code workflows tested
- [ ] Rule deploy → tune → **rollback** completed (including an AI-written rule) under normal approval
- [ ] Schema change test: renamed field, and silently broken rules identified
- [ ] False-positive rate per rule: `____` &nbsp; Tuning cycle time: `____`

### 3. AI agents
- [ ] **AI evidence quality:** the agent shows the evidence and queries behind its conclusions, flags uncertainty, and lets analysts challenge the result
- [ ] **Machine query economics:** searches per investigation, plus latency and cost as agent-generated query volume grows
- [ ] **Evidence access:** humans and agents reach the same evidence, and permissions can restrict which datasets an agent can query
- [ ] Read and write credentials are separate, and permissions are scoped by asset, action type, and blast radius
- [ ] Override rate: `____ %` &nbsp; Verified-outcome rate: `____ %`
- [ ] Permission revoked mid-investigation, and the system stops, escalates, and preserves context

### 4. Case, response & verification
- [ ] **Case integration:** evidence and context survive the handoff into case management or the existing SIEM
- [ ] **Response integration:** findings move into SOAR, identity, endpoint, or cloud controls with approval boundaries intact
- [ ] **Verified closure:** the architecture records whether the action actually achieved the intended outcome, independent of SOAR "success"
- [ ] **Auditability:** searches, detection changes, agent access, and actions can be reconstructed afterwards

### 5. Ownership & economics
- [ ] **Portability:** dataset exported and queried outside the platform
- [ ] Custom detections ported to another engine (rewrite effort noted)
- [ ] **Total operating responsibility:** engineering effort to maintain collection, schemas, detections, permissions, integrations, cases, and response
- [ ] Ingestion, indexing, retention, and federated access costs modeled at realistic volumes
- [ ] Vendor-reported performance figures validated in **your** environment

---

**Decision:** ☐ Adopt &nbsp; ☐ Coexist (add alongside current SIEM) &nbsp; ☐ Reject &nbsp;&nbsp; **Notes:** `__________`

[← Decision guide](decision-guide.md) · [MSAM overview](README.md)
