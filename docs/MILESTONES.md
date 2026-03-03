# ZuGov — Phased Roadmap

**Last updated:** 2026-02-28
**Grant target:** $2,000,000 USD over 26 months
**Roadmap end date:** April 2028

---

## Budget Overview

| Phase | Duration | Allocation | Purpose |
|---|---|---|---|
| Phase 0 | Now → April 10, 2026 (~6 weeks) | $0 (pre-grant) | Bootstrap MVP from existing resources |
| Phase 1 | April 10 – May 10, 2026 (30 days) | $150,000 | ZuKaş Alpha operations + research |
| Phase 2 | May 2026 – August 2026 (4 months) | $450,000 | Post-alpha iteration, open source, community |
| Phase 3 | Q4 2026 – Q2 2028 (18 months) | $1,400,000 | Scale, zkML, multi-community, ecosystem |
| **Total** | **26 months** | **$2,000,000** | |

Grant funds flow into the ZuGov governance escrow wallet (see D-007). Phase allocations are released by governance vote of the ZuGov core team and early adopter committee. This structure is intentional: ZuGov is governed by ZuGov.

---

## Phase 0 — Pre-ZuKaş Bootstrap

**Duration:** Now → April 10, 2026 (~6 weeks)
**Budget:** $0 (pre-grant; all work is sweat equity or existing resources)
**Owner:** Sait Gumus / web3metahub core team

### Goal

Ship a working MVP that can run real governance processes at ZuKaş 2026 on Day 1. This is not a demo. It is a live system with real users making real decisions. Every deliverable in this phase is a hard prerequisite for Phase 1.

### Deliverables

**Contracts**
- [ ] Deploy MACI v2.x contracts to chosen test network
- [ ] Deploy ZK Identity Registry contract (nullifier tracking, credential verification)
- [ ] Deploy governance escrow wallet (Safe multi-sig, initial signers: ZuKaş core team)
- [ ] Write and audit Humanode credential → ZuGov identity bridge contract
- [ ] Integration tests: full proposal → audit → vote → tally → escrow flow on testnet

**Backend / Grounding Engine**
- [ ] Grounding Engine v0: REST API wrapper around centralized LLM (Phase 1 implementation per D-005)
- [ ] Input: proposal JSON (title, body, options). Output: structured audit JSON (schema per D-012)
- [ ] IPFS upload of audit report; return content hash for on-chain linking
- [ ] Unit tests for audit schema validation
- [ ] Rate limiting, error handling, basic auth (operator-only access to trigger audits)

**Frontend**
- [ ] Proposal submission form (requires ZK identity credential)
- [ ] Active proposal list with Grounding Engine report display
- [ ] Voting interface (MACI message signing + submission)
- [ ] Post-vote results page (tally display + ZK proof link)
- [ ] Admin dashboard: create governance contexts, view proposals, trigger audit manually
- [ ] Humanode verification flow (link out to Humanode UI, receive credential, register in ZuGov identity registry)

**Research Infrastructure**
- [ ] Post-vote survey instrument (questions for Epistemic Latency measurement)
- [ ] Data collection schema (what we log per proposal, per vote, per user)
- [ ] IRB-equivalent consent flow for ZuKaş participants (data use disclosure)

**Documentation**
- [ ] Participant onboarding guide (how to verify with Humanode, how to vote)
- [ ] Operator runbook (how to run a governance session, recover from failures)
- [ ] ZuKaş-specific governance charter (what ZuGov can govern at ZuKaş, what it cannot)

### Success Metrics for Phase 0

| Metric | Target |
|---|---|
| All MVP deliverables in PROJECT.md shipped | 100% |
| Full end-to-end flow tested with ≥5 test users | Complete |
| Grounding Engine produces valid audit JSON for ≥10 test proposals | Complete |
| MACI tally verified on testnet ≥3 times | Complete |
| Zero unresolved critical bugs at April 9 | Complete |

### People Needed (Phase 0)

| Role | Requirement | Status |
|---|---|---|
| Smart contract engineer | MACI experience, ZK basics | Needed |
| Full-stack engineer | React/Next.js + EVM integration | Needed |
| Protocol engineer / architect | Overall system design ownership | Sait Gumus (partial) |
| Humanode integration contact | API access and onboarding | Needed — contact Humanode directly |

---

## Phase 1 — ZuKaş Alpha

**Duration:** April 10 – May 10, 2026 (30 days)
**Budget:** $150,000
**Users:** 150 Genesis Nodes (ZuKaş participants)
**Owner:** Sait Gumus + ZuKaş organizing team

### Goal

Run ZuGov as the live governance system for ZuKaş 2026. Measure everything. Produce the first real-world dataset on AI-assisted governance with sybil-resistant voting. Build the research case for Phase 2 funding.

### Operational Budget Breakdown (Phase 1: $150,000)

| Item | Amount |
|---|---|
| Engineering: on-site support and hotfixes (2 engineers × 30 days) | $60,000 |
| Research: post-vote surveys, data analysis, Epistemic Latency measurement | $20,000 |
| ZuKaş operational costs attributable to ZuGov (space, equipment) | $25,000 |
| Humanode integration (API costs, onboarding support) | $10,000 |
| LLM API costs (Grounding Engine Phase 1 inference) | $5,000 |
| Security review / emergency contract audit | $20,000 |
| Buffer | $10,000 |

### Governance Sessions Plan

| Week | Proposed governance topics |
|---|---|
| Week 1 (Apr 10-17) | Onboarding governance: daily schedule format, working group formation |
| Week 2 (Apr 18-24) | Resource allocation: shared budget for community activities |
| Week 3 (Apr 25 – May 1) | Protocol decisions: ZuGov design feedback from Genesis Nodes; Weyl collaboration sessions |
| Week 4 (May 2-10) | Retrospective and legacy: what ZuKaş produces, how it is archived, what continues |

Each governance session: 1-3 proposals, full Grounding Engine audit, MACI vote, public tally.

Target: ≥12 proposals over 30 days. Minimum viable research dataset: ≥8 completed votes.

### Glen Weyl Engagement (Phase 1)

Weyl attends for approximately one week. During that week:
- ZuGov team presents the Plurality SDK integration architecture
- Joint session: Weyl + ZuGov team + interested Genesis Nodes on Synthetic Futarchy vs. standard Plurality
- Working sessions on The Epistemic Hole manifesto structure
- Potential outcome: Weyl co-authorship agreement, formal Plurality Institute collaboration

Preparation required before April 10:
- [ ] Plurality SDK integration branch ready to demo (does not need to be production-ready)
- [ ] One-page technical summary of how ZuGov extends Plurality for Weyl review
- [ ] Proposed manifesto outline ready for Weyl input

### Success Metrics for Phase 1

| Metric | Target |
|---|---|
| Genesis Nodes completing Humanode verification | ≥100 of 150 |
| Proposals submitted | ≥12 |
| Votes completed (full MACI tally) | ≥8 |
| Voter participation rate per vote | ≥60% of verified nodes |
| Post-vote surveys completed | ≥70% response rate |
| Grounding Engine reports generated | 100% of proposals (no missed audits) |
| Epistemic Latency data points collected | ≥8 (one per completed vote) |
| Zero irreversible smart contract failures | Required |
| Weyl collaboration session held | Required |

### Research Outputs (Phase 1)

- Raw dataset: proposal text, audit JSON, vote tally, post-vote survey responses (anonymized)
- Initial Epistemic Latency measurements: did The Grounding Engine reduce it?
- Qualitative: participant feedback on AI advisory overlay — did it feel manipulative? Useful? Ignored?
- Technical: MACI performance under ZuKaş conditions (latency, gas costs, UX friction)
- Draft of The Epistemic Hole manifesto (based on Weyl sessions and live governance observations)

---

## Phase 2 — Post-ZuKaş Iteration

**Duration:** May 2026 – August 2026 (4 months)
**Budget:** $450,000
**Owner:** ZuGov core team + new hires enabled by grant

### Goal

Take the raw learning from Phase 1 and convert it into a production-grade, open-source protocol. Open the codebase. Build the first external developer community. Begin the Plurality SDK integration formally. Migrate the Grounding Engine to open-weights models.

### Deliverables

**Protocol Iteration (based on Phase 1 findings)**
- [ ] Fix all known UX friction points in the Humanode → ZuGov identity flow
- [ ] Improve MACI vote UX (the current MACI frontend is a known weak point)
- [ ] Implement Plurality SDK deliberation layer (pairwise preferences, quadratic discussion weighting)
- [ ] Automated escrow disbursement: MACI tally result triggers multi-sig proposal (human still signs, but it is generated automatically)
- [ ] Multi-governance context support: deploy ZuGov for a second community (identify candidate from ZuKaş network)

**Grounding Engine v1**
- [ ] Migrate from centralized LLM API to self-hosted open-weights model (Phase 2, per D-005)
- [ ] Benchmark audit quality: human expert evaluation of audit reports vs. Phase 1 centralized LLM outputs
- [ ] Improve Synthetic Futarchy probability calibration (calibration data from Phase 1 outcomes vs. predictions)
- [ ] Public Grounding Engine API: allow any governance system to submit proposals for epistemic audit

**Open Source**
- [ ] Full codebase public on GitHub under OSI-approved license (Apache 2.0 or MIT)
- [ ] Contributor documentation: how to run a local ZuGov instance
- [ ] SDK packaging: ZuGov components as installable packages (npm for frontend, pip or cargo for backend components)
- [ ] First external contributor PRs merged

**Research Publication**
- [ ] ZuKaş Alpha research paper: methodology, Epistemic Latency findings, governance outcomes
- [ ] Target venues: CCS 2026, CSCW 2027, or equivalent
- [ ] The Epistemic Hole manifesto: final draft, publication on Plurality Institute channels and ZuGov site

**Grant Application**
- [ ] Submit $2M grant application to primary target funders (see below) using Phase 1 data as evidence
- [ ] Secondary applications: Ethereum Foundation, Plurality Institute, Gitcoin, potential sovereign wealth / government innovation funds

### Phase 2 Budget Breakdown ($450,000)

| Item | Amount |
|---|---|
| Engineering team: 3 FTE × 4 months | $240,000 |
| Research: paper writing, statistical analysis, peer review | $40,000 |
| Open-weights model hosting (self-hosted Grounding Engine) | $20,000 |
| Security audit: Phase 2 contracts and SDK | $60,000 |
| Community: hackathon, developer grants, documentation | $50,000 |
| Operations and legal (open source governance, entity setup) | $30,000 |
| Buffer | $10,000 |

### Grant Target Funders (Phase 2 Application)

| Funder | Rationale | Amount |
|---|---|---|
| Ethereum Foundation (ESP) | MACI is PSE-originated; ZuGov extends the PSE stack | $300,000–$500,000 |
| Plurality Institute / Weyl | Direct extension of Plurality; co-authored research | $200,000–$400,000 |
| Gitcoin Grants / Protocol Guild | Open source public goods track | $50,000–$150,000 |
| OSS / AI Governance foundations | w/acc frame, AI epistemic safety angle | $500,000–$1,000,000 |
| ZuZalu network / pop-up city ecosystem | ZuGov as governance layer for all future Zuzalu events | TBD |

### People Needed (Phase 2)

| Role | Requirement |
|---|---|
| Protocol lead engineer | ZK systems, MACI internals, Solidity |
| Frontend engineer | React, ZK wallet integration, UX |
| ML/AI engineer | Open-weights LLM deployment, fine-tuning, evaluation |
| Research lead | Governance research, academic writing, IRB process |
| Developer relations | Open source community, documentation, hackathons |
| Operations / program manager | Grant reporting, legal, hiring |

### Success Metrics for Phase 2

| Metric | Target |
|---|---|
| Open source codebase published | Complete by June 1, 2026 |
| External contributors (GitHub) | ≥10 unique contributors |
| Second governance community onboarded | ≥1 |
| Grounding Engine v1 (open-weights) deployed | Complete by July 1, 2026 |
| Plurality SDK integration complete | Complete by August 1, 2026 |
| Research paper submitted to venue | Complete by August 31, 2026 |
| $2M grant application submitted | Complete by July 31, 2026 |

---

## Phase 3 — Scale

**Duration:** Q4 2026 – Q2 2028 (18 months)
**Budget:** $1,400,000
**Owner:** ZuGov Foundation (legal entity to be established in Phase 2)

### Goal

Deploy ZuGov as infrastructure for multiple communities. Implement the full zkML Grounding Engine (trustless, verifiable inference). Build the developer ecosystem. Pursue broader adoption in pop-up city networks, DAO communities, and civic technology contexts.

### Deliverables

**zkML Grounding Engine (Phase 3 per D-005)**
- [ ] Evaluate zkML frameworks: EZKL, Modulus Labs, Risc Zero zkVM
- [ ] Prototype: generate ZK proof that a Grounding Engine audit was produced by a specific open-weights model on a specific proposal input
- [ ] Production deployment: zkML Grounding Engine with on-chain proof verification
- [ ] This is the milestone that makes The Grounding Engine fully trustless — no need to trust the operator

**Multi-Community Platform**
- [ ] ZuGov as a multi-tenant SaaS and self-hostable protocol
- [ ] Community onboarding toolkit: deploy ZuGov for your community in <1 day
- [ ] Target communities: pop-up cities (ZuZalu network), DAOs, civic tech pilots
- [ ] ZuGov directory: public registry of active ZuGov communities

**MACI Operator Decentralization**
- [ ] Phase 1-2: operator key held by web3metahub / ZuGov Foundation
- [ ] Phase 3: MPC-based operator key (multi-party, no single point of failure)
- [ ] Long-term target: fully on-chain operator committee governed by ZuGov itself

**Developer Ecosystem**
- [ ] ZuGov SDK: well-documented packages for embedding ZuGov components in external applications
- [ ] Grant program: ZuGov developer grants ($100,000 allocated from Phase 3 budget)
- [ ] Hackathon appearances: ETHGlobal, Devcon side events, Plurality Institute events
- [ ] Plugin ecosystem: third-party Grounding Engine implementations (allow communities to use alternative AI auditors within the ZuGov framework)

**Governance Research Program**
- [ ] Ongoing Epistemic Latency measurement across all ZuGov communities
- [ ] Published dataset: anonymized governance data for academic use
- [ ] Annual ZuGov governance research report

### Phase 3 Budget Breakdown ($1,400,000)

| Item | Amount |
|---|---|
| Engineering team: 6 FTE × 18 months | $810,000 |
| zkML research and implementation | $150,000 |
| Security audits (zkML, multi-tenant contracts, MPC) | $100,000 |
| Developer grants program | $100,000 |
| Research program (ongoing measurement, publications) | $80,000 |
| Community and ecosystem (hackathons, events, marketing) | $80,000 |
| Legal and operations (foundation, contracts, compliance) | $50,000 |
| Infrastructure (hosting, compute, IPFS) | $30,000 |

### Success Metrics for Phase 3

| Metric | Target |
|---|---|
| zkML Grounding Engine prototype | Live by Q2 2027 |
| zkML production deployment | Live by Q4 2027 |
| Active ZuGov communities | ≥10 by Q2 2028 |
| Total governance proposals processed | ≥500 |
| Developer SDK installs | ≥1,000 |
| External developer grants issued | ≥10 |
| Academic citations / research collaborations | ≥5 |
| ZuGov Foundation operational | By Q1 2027 |
| MPC operator key live | By Q2 2027 |

---

## Milestone Summary Table

| ID | Milestone | Phase | Due Date | Hard Dependency |
|---|---|---|---|---|
| M-01 | MACI + contracts deployed on testnet | 0 | April 1, 2026 | None |
| M-02 | Humanode → ZuGov identity flow working | 0 | April 5, 2026 | M-01 |
| M-03 | Grounding Engine v0 API live | 0 | April 5, 2026 | None |
| M-04 | Full MVP end-to-end tested | 0 | April 9, 2026 | M-01, M-02, M-03 |
| M-05 | ZuKaş Alpha Day 1 — system live | 1 | April 10, 2026 | M-04 |
| M-06 | ≥8 completed MACI votes with tally | 1 | May 10, 2026 | M-05 |
| M-07 | Epistemic Latency dataset collected | 1 | May 10, 2026 | M-06 |
| M-08 | Weyl collaboration session complete | 1 | ~April 20, 2026 | M-05 |
| M-09 | Codebase open-sourced | 2 | June 1, 2026 | M-06 |
| M-10 | Plurality SDK integration complete | 2 | August 1, 2026 | M-08, M-09 |
| M-11 | Grounding Engine v1 (open-weights) | 2 | July 1, 2026 | M-09 |
| M-12 | Research paper submitted | 2 | August 31, 2026 | M-07 |
| M-13 | $2M grant application submitted | 2 | July 31, 2026 | M-07, M-08 |
| M-14 | Second community onboarded | 2 | August 2026 | M-09 |
| M-15 | zkML Grounding Engine prototype | 3 | Q2 2027 | M-11, M-13 |
| M-16 | MPC operator key live | 3 | Q2 2027 | M-13 |
| M-17 | 10 active communities | 3 | Q2 2028 | M-15 |
| M-18 | zkML production deployment | 3 | Q4 2027 | M-15 |

---

*This file is the canonical roadmap. Update milestone status when deliverables are complete.*
