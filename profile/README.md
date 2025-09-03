# GTCX Protocol Ecosystem

Public home for the GTCX verification protocols and sovereign platforms.

![License](https://img.shields.io/badge/License-MIT-yellow.svg) ![Updated](https://img.shields.io/badge/Updated-2025--09--03-success) ![Protocols](https://img.shields.io/badge/Protocols-5-blue) ![Sovereignty](https://img.shields.io/badge/Design-Sovereignty--Preserving-brightgreen)

Last updated: 2025‑09‑03 06:50Z

## Table of contents
- Executive summary
- Who this is for
- Problems we solve
- Protocols (foundation) — deep dives
- Three‑tier architecture
- Open‑source platforms & tooling
- End‑to‑end data flow and visuals
- Five flagship use cases
- Pilot in one week (checklist)
- Spec links
- FAQ and Glossary
- Community & contributions

> Start here: protocols index → `research/02-protocol-specifications/l1-core-protocols/` • platforms overview → `gtcx-ecosystem-platforms/README.md` • e2e demo (PANX↔Cortex) → `gtcx-ecosystem-cognitive/README.md`

## Executive summary
GTCX standardizes how facts are verified, approved, and preserved in global trade. Five core protocols (TradePass, GCI, GeoTag, VaultMark, PvP) produce sovereign proofs that platforms (CRX, SGX, AGX) use to automate permits, markets, and cross‑border settlement.

## Who this is for
- Governments and regulators seeking sovereignty‑preserving digital infrastructure
- Verified producers and cooperatives needing market access with trust guarantees
- Exchanges, vaults, and banks integrating proof‑based settlement
- Integrators and open‑source builders adopting a protocol‑first stack

## Problems we solve
- Fragmented identity and inconsistent policy enforcement across jurisdictions
- Location/provenance fraud and unverifiable documentation
- Trust bottlenecks that slow approvals, trading, and settlement
- Audit gaps and verification “washing” through custody chains

## Protocols (foundation)
Core protocol specifications live in `gtcx-ecosystem-research/02-protocol-specifications/`.
- TradePass — identity & authorization (DIDs/VCs, roles, entitlements)
- GCI — compliance & policy (credentials, attestations, scoring)
- GeoTag — evidence (cryptographic location, timestamping, device attestation)
- VaultMark — audit (sealed receipts, custody chain)
- PvP — settlement (post‑verification, atomic payment‑versus‑physical)

Transport and data contracts use JSON Schema with versioned `$id`.

### The five protocols (deep dives)
- TradePass (Identity & Authorization): DIDs/VCs, role catalogs, time‑boxed grants, least‑privilege; composes with GCI and PANX weights
- GCI (Compliance & Policy): attestations, algorithmic scoring, jurisdictional policies, predictive risk; gates roles and settlement
- GeoTag (Evidence): multi‑constellation GPS, satellite correlation, HSM signatures, Merkle proofs; replaces claims with proofs
- VaultMark (Audit): physical‑digital binding (NFC/RFID), digital twins, immutable custody; prevents verification washing
- PvP (Settlement): atomic payment‑versus‑physical; settlement only when proof+policy pass

<!-- Removed high-level A→B→C diagram to reduce redundancy -->

### Spec links
- CRX/SGX Exchange Integration: `research/02-protocol-specifications/l3-exchange-layer/crx-sgx-exchange-integration.md`
- AGX (Authenticated Global Exchange): `research/02-protocol-specifications/l3-exchange-layer/agx-authenticated-global-exchange.md`

### Verification layers → platforms (visual)
```mermaid
flowchart LR
  subgraph VP["Verification Protocols"]
    TP["TradePass"]
    GCI["GCI"]
    GT["GeoTag"]
    VM["VaultMark"]
    PVP["PvP"]
  end
  subgraph RS["Reference Services"]
    PANX["PANX Verification"]
    ANISA["ANISA Cultural"]
    CORTEX["Cortex Analytics"]
  end
  subgraph PL["Platforms"]
    CRX["CRX Regulatory"]
    SGX["SGX Exchange"]
    AGX["AGX Global"]
  end
  TP --> PANX
  GCI --> PANX
  GT --> PANX
  VM --> PANX
  PVP --> PANX
  ANISA -.-> PANX
  PANX --> CORTEX
  PANX --> CRX
  PANX --> SGX
  PANX --> AGX
```

## Five flagship use cases
- Permit issuance: GCI + TradePass + VaultMark; hours instead of weeks
- Depart/arrive verification: GeoTag + VaultMark → PANX proof; real‑time alerts
- Corridor policy enforcement: GCI + TradePass; transparent, consistent governance
- Milestone‑based payment: PANX proof → PvP + VaultMark; risk‑free release
- Dispute packet: VaultMark + GeoTag + GCI; complete sealed evidence

## Pilot in one week (checklist)
1) Site onboarding: issue TradePass, bind GeoTag devices, enable VaultMark
2) Capture: record depart/arrive events with signed evidence
3) Verify: PANX proof thresholds per event type
4) Govern: GCI policy gates; simulate corridor rules
5) Settle: dry‑run PvP release conditions
6) Report: sealed audit bundle + metrics

## FAQ
- Is PANX a protocol? No. PANX is a verification service that consumes protocol artifacts to produce network proofs.
- What’s sealed? Proofs, custody events, and artifacts via VaultMark.
- How do I pilot? Start with GeoTag + VaultMark at one site; add GCI/TradePass; then PANX; gate PvP last.

## Glossary
- Protocol — shared rulebook and data contracts
- Proof — evidence‑backed claim you can independently verify
- Seal — tamper‑evident record preserved for audit
- Atomic settlement — payment/delivery only complete together

## Three‑tier architecture
1) Protocols — specifications and data contracts (research repo)
2) Reference services — PANX, Cortex, ANISA (this org)
3) Platforms & apps — open‑source frontends, terminals, and integrations

#### Protocols layer
```mermaid
flowchart LR
  TP["TradePass"] --> GT["GeoTag"]
  GT --> VM["VaultMark"]
  VM --> PVP["PvP"]
  GCI["GCI"] --> TP
  GCI --> PVP
```
Protocols are composable, not strictly linear. TradePass authorizes capture, GeoTag produces signed evidence, VaultMark seals artifacts, and PvP gates settlement. GCI applies policies into both authorization and settlement.

#### Reference services layer
```mermaid
flowchart LR
  ANISA["ANISA Cultural"] <--> PANX["PANX Verification"]
  PANX -->|verified events / metrics| CORTEX["Cortex Analytics"]
  CORTEX -.->|anomaly alerts / re‑verify triggers| PANX
  CORTEX -.->|insights / topics| ANISA
```
Reference services enrich, verify, and analyze protocol artifacts. ANISA adds cultural context; PANX turns evidence + policy into network proofs; Cortex aggregates and visualizes signals for operators.

#### Platforms layer
```mermaid
flowchart LR
  CRX["CRX Regulatory"]
  SGX["SGX Sovereign Exchange"]
  AGX["AGX Global Exchange"]

  CRX --> SGX
  SGX --> CRX
  SGX --> AGX
  AGX --> SGX
  CRX -.-> AGX
  AGX -.-> CRX
```
Platforms interoperate rather than strictly chain. CRX feeds sovereign approval/compliance into SGX; SGX returns market and custody events back to CRX. AGX connects multiple SGX instances to international buyers; limited CRX↔AGX links exist for export controls and revenue reporting.

## Reference services (live repos)
- PANX (Oracle/Verification): `gtcx-ecosystem-cognitive/panx` — consensus, proofs, forward to Cortex
- Cortex (Analytics): `gtcx-ecosystem-cognitive/cortex` — ingest, summary, anomalies
- ANISA (Cultural Intelligence): `gtcx-ecosystem-anisa` — analyze/assess endpoints for enrichment

Each service includes: README, user/agent guides, runbooks, deploy guides, JSON Schemas, and changelogs.

## Open‑source platforms & tooling
- CRX — government workflow automation & regulatory processing
- SGX — sovereign national exchange & settlement
- AGX — authenticated global exchange (international marketplace)
- Terminal & UI shells — operator dashboards and community views (repos under `gtcx-ecosystem-platforms/`)
- APIs & gateways — shared adapters and routing (`gtcx-ecosystem-api-gateway/`)
- Research & specs — canonical protocol drafts and design notes (`gtcx-ecosystem-research/`)

### End‑to‑end trade process (custody before SGX)
```mermaid
flowchart TD
  CRX["CRX Registration & Onboarding"] --> TP["TradePass Identity"]
  TP --> GT["GeoTag Site & Production Evidence"]
  GT --> GCI["GCI Compliance Evaluation (Score)"]
  GCI --> VM["VaultMark Custody (Sealed Lots)"]
  VM --> SGX["SGX Export License / National Exchange"]
  SGX --> AGX["AGX Authenticated Global Exchange"]
  AGX --> PVP["PvP Cross‑Border Settlement"]
  PVP --> VM2["VaultMark Sealed Audit Records"]

  %% Gates (dashed control links)
  PANX["PANX Verification"]
  CRXGATE["CRX Permit / Export Approval"]
  PANX -.->|proof achieved / lot eligibility| VM
  CRXGATE -.->|permit issued| SGX
  PANX -.->|settlement proof ref| PVP
```

### Verification gates (at a glance)
```mermaid
flowchart LR
  TP["TradePass"] --> GT["GeoTag"] --> GCI["GCI Eligibility"] --> VM["VaultMark Custody"] --> PVP["PvP"]
  PANX["PANX Verification"] -.->|lot eligibility| VM
  CRX["CRX Permit"] -.->|export approval| VM
  PANX -.->|proof reference| PVP
```

### End‑to‑end sequence (eligibility first, then trade)
```mermaid
sequenceDiagram
  participant CRX as CRX (register)
  participant TP as TradePass
  participant GT as GeoTag
  participant GCI as GCI (eligibility)
  participant VM as VaultMark (at trade)
  participant PVP as PvP (settle)

  CRX->>TP: Onboard & issue TradePass
  TP->>GT: Authorize capture & bind identity
  GT->>GCI: Provide signed site/production evidence
  GCI-->>TP: Trade eligibility (greenlight)

  Note over VM,PVP: When there is product to trade
  TP->>VM: Create custody/lot & seal artifacts
  VM-->>PVP: Custody proof
  GCI-->>PVP: Policy OK
  PVP->>PVP: Atomic settlement
```

## Contracts and versioning
- Schemas: JSON Schema with stable `$id` and semantic versioning
  - Shared interfaces: `gtcx-ecosystem-cognitive/shared/interfaces/`
  - PANX request/response: `panx_verification_event.schema.json`, `panx_verify_response.schema.json`
  - Cortex ingest: `cortex_ingest_event.schema.json`
- Runtime signaling
  - Response header: `X-Contract-Version: vMAJOR.MINOR`
  - Backward‑compatible additive changes bump MINOR; breaking changes bump MAJOR with deprecation window
- Tooling & checks
  - Compatibility script: `gtcx-ecosystem-cognitive/shared/interfaces/contracts_compat_check.py`
  - CI suggestion: validate schemas + sample instances on PRs (can be run locally now)
  - Environment override for schema paths in containers: see `panx/service/app/validation.py`

## Deploy
- Local Docker Compose (PANX + Cortex + DB)
  - Compose: `gtcx-ecosystem-cognitive/docker-compose.yml`
  - PANX service: `gtcx-ecosystem-cognitive/panx/service/README.md`
- GCP VM (TLS via Caddy)
  - Overlay & guide: `gtcx-ecosystem-cognitive/infra/compose-prod/README.md`
  - Env template: `gtcx-ecosystem-cognitive/infra/compose-prod/ENV.example`
- ANISA API
  - Deploy guide: `gtcx-ecosystem-anisa/agile-pm/deploy_gcp_vm.md`
- Planned
  - Helm charts & GKE Autopilot manifests
  - Terraform modules for VM + DNS + secrets

## Roadmap (high‑level)
- Protocol hardening & specification snapshots
  - TradePass, GCI, GeoTag, VaultMark, PvP: stabilize core semantics and data contracts
  - Snapshot cadence and change control (proposal → review → RFC → snapshot)
  - Conformance test suite and fixtures per protocol (positive/negative cases)
- Schema‑first development
  - Semantic versioning rules, deprecation windows, and upgrade playbooks
  - Reference client SDKs for TypeScript/Python (schema‑bound types, validators)
  - CI gates for schema compatibility and sample instance coverage
- Interoperability & federation (from protocols repo roadmap)
  - TradePass federation and identity linking across jurisdictions
  - PvP multi‑rail connectors (banking, mobile money, crypto) with atomicity proofs
  - GeoTag secure attestation (device certs, HSM rotation, field audit trail)
  - VaultMark smart seal program and digital twin APIs
- Persistence & retention
  - Managed Postgres/Timescale for proofs/events, partitioning and TTL policies
  - Audit archive export (cold storage bundles signed by VaultMark)
- Observability
  - Service metrics and SLOs; dashboards for operators and regulators
  - Distributed tracing with selective sampling; alert runbooks
- Agentic behaviors (progressive)
  - PANX: borderline re‑verify plans; dynamic thresholds informed by risk/quality
  - Cortex: anomaly watchers, action proposals, operator copilot integrations
- Pilots & reference implementations
  - Corridor deployments with partners; playbooks for CRX/SGX/AGX rollout
  - Telegram onboarding funnels linked to TradePass/GeoTag quickstarts

See also: Protocols roadmap in `gtcx-ecosystem-protocols/README.md` (Future Roadmap section).

## Community
- Issues and discussions in each repo (use repo issue trackers)
- Contributions welcome: docs, specs, code, diagrams
- Security: report privately to maintainers before public disclosure

MIT License

---

Contributions & governance: open issues/PRs against component repos; follow per‑component CHANGELOGs for releases (`gtcx-ecosystem-cognitive/CHANGELOG.md`, `gtcx-ecosystem-anisa/CHANGELOG.md`, `gtcx-ecosystem-cognitive/panx/changelog.md`, `gtcx-ecosystem-cognitive/cortex/changelog.md`).

## Telegram onboarding (fast path)
- Telegram bot utilities and onboarding flows:
  - `gtcx-ecosystem-shared/utilities/gtcx-utility-telegrambot/README.md`
  - `gtcx-ecosystem-shared/utilities/gtcx-utility-tradedesk/README.md`
  - Master onboarding playbook: `gtcx-ecosystem-shared/utilities/gtcx-utility-tradedesk/agentic/gtcx-master-onboarding.md`
- Typical flow: chat‑based TradePass issuance → GeoTag device pairing → basic compliance prompts → CRX pre‑registration → links into SGX/AGX portals when eligible.
