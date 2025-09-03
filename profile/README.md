# GTCX Verification Layers (Layer‑1 Protocols)

Public home for GTCX’s core verification protocols and how they work independently and together.

![License](https://img.shields.io/badge/License-MIT-yellow.svg)
![Updated](https://img.shields.io/badge/Updated-2025--09--03-success)
![Protocols](https://img.shields.io/badge/Protocols-5-blue)
![Sovereignty](https://img.shields.io/badge/Design-Sovereignty--Preserving-brightgreen)

Last updated: 2025‑09‑03

## Table of contents
- Executive summary
- Who this is for
- Problems we solve
- The five verification layers (deep dives)
- How they fit together (diagrams)
- Platforms mapping (CRX, SGX, AGX)
- Five flagship use cases
- Pilot in one week (checklist)
- Spec links
- FAQ
- Glossary
- Contributions & governance

> Start here: protocols index → `research/02-protocol-specifications/l1-core-protocols/` • platforms overview → `gtcx-ecosystem-platforms/README.md` • e2e demo (PANX↔Cortex) → `gtcx-ecosystem-cognitive/README.md`

---

## Executive summary
GTCX standardizes how facts are verified, approved, and preserved in global trade. Five core protocols (TradePass, GCI, GeoTag, VaultMark, PvP) produce sovereign, cryptographically verifiable artifacts. Platforms (CRX, SGX, AGX) consume these artifacts to automate permits, markets, and cross‑border settlement.

## Who this is for
- Governments and regulators seeking sovereignty‑preserving digital infrastructure
- Verified producers and cooperatives needing market access with trust guarantees
- Exchanges, vaults, and banks integrating proof‑based settlement
- Integrators and open‑source builders adopting a protocol‑first stack

## Problems we solve
- Who is allowed to do what? (access & roles)
- Who are the parties? Are they compliant? (identity & policy)
- Did a real event happen, where and when? (location & proofs)
- Can we settle safely across payment rails? (atomic settlement)
- Do we have tamper‑evident receipts for audit? (sealed records)

---

## The five verification layers (deep dives)

### 1) Identity & Authorization — TradePass
- What: roles, scopes, entitlements; who is allowed to act.
- Why: least‑privilege access, corridor rules, time‑boxed grants, transparent governance.
- Key ideas: DIDs/VCs, dynamic grants, role catalogs, reputation.
- Works independently: gate any API/UI or operational action.
- Composes with: GCI (grant by credentials), PANX (weights by role), PvP (initiate/approve permissions).
- Spec: https://github.com/gtcx-protocol/gtcx-ecosystem-research/blob/main/02-protocol-specifications/l1-core-protocols/tradepass-identity-specification.md

### 2) Compliance & Policy — GCI
- What: algorithmic compliance, attestations, policy checks, predictive risk.
- Why: make “who” and “which rules apply” transparent, consistent, and auditable.
- Key ideas: credential issuers, multi‑factor scoring, jurisdictional policies.
- Works independently: evaluate identity and compliance signals for any workflow.
- Composes with: TradePass (grant roles), PANX (validator classes/weights), PvP (regulatory gates).
- Spec: https://github.com/gtcx-pro
