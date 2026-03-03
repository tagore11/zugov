# ZuGov — Project Master Context

**Last updated:** 2026-02-28
**Status:** Pre-alpha. MVP targeting ZuKaş 2026 (April 10).

---

## What ZuGov Is

ZuGov is an open-source Plurality Governance SDK designed to make collective decision-making in temporary, high-density communities legible, sybil-resistant, and epistemically sound. It combines MACI-based anti-collusion voting, ZK-verified unique identity via Humanode, and an AI epistemic auditor called The Grounding Engine — which has zero voting power and zero veto authority, serving purely as a signal layer that surfaces prediction-market-style probability assessments and argument quality scores before any vote is cast. ZuGov's philosophical anchor is w/acc (Wisdom Acceleration): the thesis that collective intelligence must be deliberately cultivated to keep pace with the rate of AI capability growth, and that governance tooling is a prerequisite for that cultivation, not an afterthought.

---

## Core Components

### 1. The Grounding Engine

The AI epistemic auditor. It is activated between proposal submission and vote opening. It does not vote. It does not block. It cannot veto.

What it does:
- Ingests a governance proposal (text + metadata)
- Runs structured argument analysis: claims, evidence quality, stated assumptions, logical dependencies
- Runs a synthetic prediction market simulation: assigns probability estimates to stated outcomes using available prior data, analogous cases, and base rates
- Surfaces a structured epistemic report visible to all voters before voting opens
- Flags "Epistemic Latency" events — cases where the community's collective model of a situation is demonstrably behind the available evidence

The Grounding Engine is a read-only oracle. All output is advisory. Voters may ignore it entirely.

### 2. MACI (Minimum Anti-Collusion Infrastructure)

The voting layer. MACI uses ZK cryptography to make votes private during the voting period and verifiable after tallying. It prevents vote-buying and bribery by making it impossible for a voter to prove to a third party how they voted while the vote is open.

- Operator: ZuGov protocol (initially centralized key, see D-005)
- Message processing: zkSNARKs (Groth16)
- Frontend: custom ZuGov UI wrapping MACI v2.x contracts
- Tally verification: fully public after vote close

### 3. ZK Identity

Proposal submission and voting require a verified ZK identity. This is not a social login. Identity proofs are:
- Non-transferable
- Unlinkable across sessions (privacy-preserving)
- Anchored to Humanode biometric uniqueness (one person, one identity)

ZK identity proofs are generated client-side. The protocol never sees raw biometric data.

### 4. Humanode Integration

Humanode provides biometric uniqueness proof: it verifies that a given wallet corresponds to a unique living human, without storing or revealing which human. This is the sybil-resistance layer.

- Why Humanode over WorldCoin: see D-003
- Integration point: users complete Humanode verification once, receive a ZK credential, present that credential to ZuGov's identity registry to unlock proposal and voting rights
- Testnet deployment: Humanode EVM-compatible testnet

### 5. Plurality SDK

The deliberation and preference aggregation layer. The Plurality SDK (associated with E. Glen Weyl and the Plurality Institute) provides mechanisms for:
- Quadratic voting weight assignment
- Pairwise preference collection
- Diversity-weighted aggregation (preventing majority tyranny on correlated preference clusters)

Integration with ZuGov is additive — we do not fork Plurality; we wrap and extend it (see D-008).

---

## Key Philosophical Positions

### w/acc — Wisdom Acceleration

w/acc is ZuGov's philosophical frame. It holds that:
1. AI capability is accelerating (e/acc is correct about this)
2. Unchecked acceleration without collective sense-making infrastructure is dangerous (d/acc is correct about this)
3. The correct response is to accelerate the development of collective wisdom infrastructure in parallel with AI capability — not to slow AI, and not to blindly accelerate it

w/acc is operationalized through ZuGov: every governance interaction is a data point in a collective learning system. The Grounding Engine is the feedback mechanism that makes that learning legible.

### Epistemic Latency

The gap between when evidence about a situation becomes available and when collective knowledge updates to reflect that evidence. High epistemic latency communities make decisions on stale models. The Grounding Engine is specifically designed to surface and reduce epistemic latency by making the evidence state explicit before voting opens.

Epistemic Latency is a measurable quantity. We intend to measure it at ZuKaş: for each proposal, we will record the delta between "when was the relevant evidence first available" and "what evidence did voters cite in post-vote surveys." This is a primary research output of the ZuKaş Alpha.

### Synthetic Futarchy

Traditional Futarchy: governance by prediction markets — if the market predicts policy X will improve metric Y, adopt policy X. Problem: thin markets, manipulation, short-termism, no deliberation.

Synthetic Futarchy is The Grounding Engine's approach: use prediction market *logic* (probability estimates, outcome decomposition, base rate reasoning) to structure the epistemic audit without actually running a market. The result is a proposal assessment that shows voters the predicted probability distribution of stated outcomes, the key assumptions those probabilities rest on, and the historical base rates for analogous decisions. Voters then vote via MACI with this structured information in hand.

This preserves the epistemic rigor of futarchy without its market manipulation vulnerabilities.

### The Epistemic Hole (Planned Manifesto)

A written critique of both naive Futarchy (markets as governance) and naive Plurality (quadratic voting as sufficient for epistemic health). The core argument: both systems assume voters have reasonably accurate models of reality, and neither provides infrastructure to maintain that accuracy as complexity scales. ZuGov and The Grounding Engine are the proposed solution layer. Planned for release during or after ZuKaş 2026.

---

## Technical Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        ZuGov Protocol                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   PROPOSAL LAYER                                            │
│   ┌──────────────────────────────────────────────────────┐  │
│   │ Proposer submits: title, body, options, deadline     │  │
│   │ Requires: valid ZK identity credential               │  │
│   └──────────────────────┬───────────────────────────────┘  │
│                          │                                  │
│   EPISTEMIC LAYER        ▼                                  │
│   ┌──────────────────────────────────────────────────────┐  │
│   │ THE GROUNDING ENGINE (read-only, no veto)            │  │
│   │   - Argument structure analysis                      │  │
│   │   - Synthetic Futarchy probability assessment        │  │
│   │   - Epistemic Latency flag (if applicable)           │  │
│   │   - Output: structured epistemic report (public)     │  │
│   └──────────────────────┬───────────────────────────────┘  │
│                          │                                  │
│   DELIBERATION LAYER     ▼                                  │
│   ┌──────────────────────────────────────────────────────┐  │
│   │ Plurality SDK                                        │  │
│   │   - Pairwise preference collection                   │  │
│   │   - Diversity-weighted discussion threads            │  │
│   │   - Quadratic comment weighting                      │  │
│   └──────────────────────┬───────────────────────────────┘  │
│                          │                                  │
│   VOTING LAYER           ▼                                  │
│   ┌──────────────────────────────────────────────────────┐  │
│   │ MACI v2.x                                            │  │
│   │   - Anti-collusion voting (bribery-resistant)        │  │
│   │   - ZK tally (private during vote, public after)     │  │
│   │   - Quadratic or 1p1v weighting                      │  │
│   └──────────────────────┬───────────────────────────────┘  │
│                          │                                  │
│   IDENTITY LAYER         ▼                                  │
│   ┌──────────────────────────────────────────────────────┐  │
│   │ ZK Identity Registry                                 │  │
│   │   - Credential issuance (after Humanode verification)│  │
│   │   - Nullifier tracking (prevent double-spend/vote)   │  │
│   │   - Session privacy (unlinkable across votes)        │  │
│   └──────────────────────┬───────────────────────────────┘  │
│                          │                                  │
│   SYBIL RESISTANCE       ▼                                  │
│   ┌──────────────────────────────────────────────────────┐  │
│   │ Humanode                                             │  │
│   │   - Biometric uniqueness proof (one human = one cred)│  │
│   │   - No raw biometric data stored                     │  │
│   │   - EVM-compatible credential output                 │  │
│   └──────────────────────┬───────────────────────────────┘  │
│                          │                                  │
│   TREASURY LAYER         ▼                                  │
│   ┌──────────────────────────────────────────────────────┐  │
│   │ Governance Escrow Wallet                             │  │
│   │   - Multi-sig with governance-controlled release     │  │
│   │   - Execution of on-chain outcomes from votes        │  │
│   └──────────────────────────────────────────────────────┘  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## MVP Definition (Must Be Live by April 10, 2026)

The following is the minimum viable system that makes the ZuKaş Alpha meaningful as a research environment. Anything below this line is not shipped — it is cut.

| Component | MVP Requirement |
|---|---|
| Humanode integration | A user can complete biometric verification and receive a ZK credential usable in ZuGov |
| ZK Identity Registry | Credential presentation, nullifier check, issuance of governance access |
| Proposal Submission UI | A form where a credentialed user submits a proposal (title, body, options, vote deadline) |
| Grounding Engine v0 | Submits proposal text to an LLM (centralized, API-based), returns structured epistemic report; report is publicly visible before vote opens |
| MACI Voting | A live MACI deployment on a supported network where credentialed users can vote on active proposals |
| Tally + Results | After vote close, ZK tally is computed and results are publicly verifiable |
| Governance Escrow Wallet | A multi-sig wallet that receives governance treasury funds and can be instructed by vote outcomes |
| Admin Dashboard | ZuKaş organizer can create governance contexts, set parameters, view all proposals and statuses |

Not in MVP (explicitly deferred):
- Plurality SDK deliberation layer (deliberation will happen in-person at ZuKaş)
- zkML Grounding Engine (Phase 3)
- Token-based incentives
- Mobile app
- Multi-community support (ZuKaş is a single-tenant alpha)

---

## Stakeholders

### Glen Weyl — Plurality Institute

Role: Plurality SDK author and integration partner. Weyl is physically attending ZuKaş 2026 for one week. This creates a direct opportunity for co-authorship on The Epistemic Hole manifesto and for technical alignment on the Plurality SDK integration. He is not a core team member. Collaboration scope is defined by D-008.

### ZuKaş 2026 Genesis Nodes (150 people)

Role: Alpha test users. These are the first 150 participants in any ZuGov governance process. They are not a passive user group — they are a curated set of builders, researchers, and governance practitioners selected for ZuKaş. Their feedback during April 10 – May 10 is a primary research input.

Data we will collect from them:
- Number of proposals submitted
- Participation rate per vote
- Post-vote epistemic survey: did the Grounding Engine report change their vote? Did it surface information they were unaware of?
- Measured epistemic latency per proposal

### ZuKaş Organizer (web3metahub / Sait Gumus)

Role: Protocol operator for the Alpha. Controls the MACI operator key during Phase 1. Controls the admin dashboard. Primary point of contact for Humanode and grant applications.

---

## Repositories and Links

| Resource | Location |
|---|---|
| ZuGov monorepo | `~/Projects/zugov/` |
| Frontend | `~/Projects/zugov/frontend/` |
| Backend / Grounding Engine | `~/Projects/zugov/backend/` |
| Smart contracts (MACI, identity, escrow) | `~/Projects/zugov/contracts/` |
| Documentation | `~/Projects/zugov/docs/` |
| MACI upstream | https://github.com/privacy-scaling-explorations/maci |
| Humanode | https://humanode.io |
| Plurality Institute | https://www.plurality.net |

---

*This file is the canonical project context. Update it when architecture decisions change.*
