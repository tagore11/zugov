# ZuGov — Architectural Decision Log

**Last updated:** 2026-02-28

These decisions are locked. They are not up for discussion in sprint planning or implementation tickets. If a decision needs to be revisited, a new entry is added below the original with a `SUPERSEDES D-XXX` notation and a dated rationale. Do not delete or modify existing entries.

---

## D-001 — The Grounding Engine has ZERO voting/veto power

**Status:** Locked
**Date:** 2026-02-28

**Decision:** The Grounding Engine is a read-only epistemic overlay. It cannot vote. It cannot block a proposal from reaching a vote. It cannot modify, suppress, or delay vote outcomes. Its only output is a structured epistemic report that is visible to voters before the vote opens.

**Rationale:** Any system in which an AI can block, delay, or weight a governance outcome is a system in which the AI has political power. We reject this design unconditionally. The credibility of ZuGov as a governance tool depends entirely on the assurance that humans retain all decisional authority. The Grounding Engine's value is epistemic (improving the quality of information voters have) not decisional (changing the set of options available to voters).

**Implications for implementation:**
- The Grounding Engine is an off-chain service. It has no on-chain write access.
- Its report is stored as a content-addressed blob (IPFS or equivalent) and linked to the proposal record on-chain.
- The report is rendered in the voting UI as advisory content with explicit labeling: "Epistemic Audit — Advisory Only."
- The voting contract has no dependency on the Grounding Engine. A vote can proceed even if the Grounding Engine is offline.

---

## D-002 — MACI is the voting layer

**Status:** Locked
**Date:** 2026-02-28

**Decision:** All binding governance votes in ZuGov use MACI (Minimum Anti-Collusion Infrastructure) as the cryptographic voting primitive. Snapshot, on-chain direct voting, and multisig-as-governance are explicitly excluded.

**Rationale:** Governance systems that allow vote-buying and bribery are not governance systems — they are token-weighted auctions. MACI's ZK message encryption makes it cryptographically impossible for a voter to prove to a third party how they voted during the voting period, which eliminates the mechanics of vote buying. Snapshot does not provide this property. Direct on-chain voting does not provide this property.

**Implications for implementation:**
- ZuGov deploys and operates MACI contracts. The MACI operator key is held by the protocol operator (initially web3metahub, see D-005 for decentralization path).
- MACI version: v2.x (latest stable at time of MVP deployment).
- Network: to be determined based on gas cost and latency requirements at ZuKaş; candidates are a low-cost EVM-compatible L2 or a dedicated ZuGov testnet.
- All MACI tallies are published publicly after vote close. Tally verification instructions are surfaced in the UI.

---

## D-003 — Humanode for sybil resistance, not WorldCoin, not passport

**Status:** Locked
**Date:** 2026-02-28

**Decision:** ZuGov uses Humanode as the biometric uniqueness proof layer. WorldCoin (World ID), government passport verification, and social-graph-based sybil resistance are explicitly excluded.

**Rationale:**

- **WorldCoin rejection:** WorldCoin's iris scan infrastructure requires proprietary hardware (the Orb), is controlled by a centralized entity (Tools for Humanity), and has unresolved data custody concerns. It also creates vendor lock-in that is incompatible with ZuGov's long-term open-source posture.
- **Passport rejection:** Government-issued identity links pseudonymous governance participation to a real-world legal identity. This destroys privacy and excludes participants who cannot or choose not to present government ID (stateless persons, privacy-sensitive researchers, participants under repressive governments).
- **Humanode selection:** Humanode provides biometric uniqueness proof (one human = one credential) without storing or revealing identity. It is compatible with EVM tooling, it is not controlled by a single corporate entity, and its verification model is compatible with ZK credential generation.

**Implications for implementation:**
- Users complete Humanode verification once per governance context (or per configurable period).
- Humanode verification outputs a credential. ZuGov's ZK Identity layer transforms this into a ZK proof usable in the identity registry.
- If Humanode verification fails or is unavailable, the user cannot obtain a ZuGov identity credential. There is no fallback identity method in the MVP.

---

## D-004 — ZuKaş 2026 is the Alpha test environment

**Status:** Locked
**Date:** 2026-02-28

**Decision:** ZuGov's first live governance test is ZuKaş 2026 (April 10 – May 10, Kaş, Turkey). 150 Genesis Nodes are the alpha user population. No production deployment precedes this.

**Rationale:** Governance protocols require high-trust environments for early testing. ZuKaş is a curated, high-density gathering of builders and researchers who have explicitly opted into experimental governance processes. This is as close to a controlled research environment as is achievable with a real governance system. Deploying to an anonymous or uncontrolled user base before this test would produce noise, not signal.

**Implications for implementation:**
- The MVP scope is scoped to what is testable with 150 participants over 30 days (see PROJECT.md MVP section).
- All ZuKaş governance sessions are treated as research data. Consent and data handling procedures must be defined before April 10.
- ZuKaş-specific parameters: single governance context, organizer-controlled admin dashboard, proposals scoped to ZuKaş community decisions (e.g., daily schedule, resource allocation, event format choices).
- Failure modes are acceptable. The alpha is a learning instrument, not a production service.

---

## D-005 — Progressive decentralization: centralized LLM → open-weights → zkML

**Status:** Locked
**Date:** 2026-02-28

**Decision:** The Grounding Engine follows a defined three-phase decentralization path. Phase 1 uses a centralized LLM API. Phase 2 migrates to open-weights models. Phase 3 implements zkML (zero-knowledge machine learning) for verifiable, trustless inference.

**Phase breakdown:**

| Phase | Grounding Engine implementation | Trust model |
|---|---|---|
| Phase 1 (ZuKaş Alpha) | Centralized LLM API (e.g., Anthropic Claude, OpenAI) | Trust the operator |
| Phase 2 (Post-ZuKaş) | Self-hosted open-weights model (e.g., Llama 3 or Mistral class) | Trust the server operator |
| Phase 3 (Scale) | zkML: ZK proof that inference was run correctly on a specified open-weights model | Trustless, verifiable |

**Rationale:** zkML tooling (EZKL, Modulus Labs) is not yet production-ready for the inference scale required by The Grounding Engine. Shipping Phase 3 now would delay the MVP by 12+ months. The progressive path lets us ship a useful product now while maintaining a credible commitment to full trustlessness.

**Implications for implementation:**
- The Grounding Engine must be implemented behind a clean API interface that is swappable between phases. The voting and identity layers have no awareness of which Grounding Engine implementation is running.
- The Phase 1 centralized LLM choice is a product decision, not an architectural one. It can change without touching the DECISIONS log.
- The MACI operator key decentralization path follows the same logic: Phase 1 = operator-held key, Phase 2 = multi-party computation / MPC key, Phase 3 = fully on-chain operator committee.

---

## D-006 — w/acc philosophical framing

**Status:** Locked
**Date:** 2026-02-28

**Decision:** ZuGov's public philosophical position is w/acc (Wisdom Acceleration). The project does not affiliate with e/acc (effective accelerationism) or d/acc (defensive accelerationism) as primary frames.

**Rationale:** e/acc is correct that AI capability growth is net positive and should not be slowed, but it provides no theory of governance or collective intelligence. d/acc is correct that defense and resilience matter, but it tends toward insularity and can become a frame for stagnation. w/acc holds the tension: capability growth is good, and collective wisdom infrastructure must grow in parallel to keep the social layer coherent as AI complexity increases. ZuGov is the implementation of w/acc — it is a tool for accelerating collective wisdom, not a brake on capability.

**Implications for implementation:**
- All project communications, documentation, and grant applications use w/acc as the primary frame.
- The Epistemic Hole manifesto (planned) is the primary intellectual artifact for this position.
- Glen Weyl collaboration is framed within w/acc: Plurality governance is a specific instantiation of wisdom acceleration infrastructure.

---

## D-007 — Escrow wallet is a core protocol primitive

**Status:** Locked
**Date:** 2026-02-28

**Decision:** ZuGov includes a governance-controlled escrow wallet as a first-class protocol primitive, not a bolted-on feature.

**Rationale:** A governance system that cannot execute resource allocation decisions is an advisory system, not a governance system. For ZuGov to be meaningful, vote outcomes must be capable of triggering on-chain resource flows. The escrow wallet is the mechanism that makes this possible.

**Specification:**
- The escrow wallet is a multi-sig smart contract with governance-controlled signers.
- Signer set is determined by governance vote, not hardcoded.
- Disbursement transactions require a valid MACI tally that authorizes the disbursement.
- The MVP implementation uses a standard multi-sig (e.g., Safe / Gnosis Safe) with manual signer execution pending the automated disbursement integration.
- Phase 2: automated disbursement triggered by on-chain tally result.

**Implications for implementation:**
- Contracts directory must include the escrow contract alongside MACI and identity contracts.
- Grant funds ($2M target) will flow into the governance escrow, not to a personal or organizational wallet. This is a credibility commitment.

---

## D-008 — Glen Weyl collaboration = Plurality SDK integration, not fork

**Status:** Locked
**Date:** 2026-02-28

**Decision:** ZuGov integrates the Plurality SDK as an upstream dependency. We do not fork it, do not create a competing Plurality implementation, and do not make architectural changes that would make our integration incompatible with the upstream project.

**Rationale:** Glen Weyl is attending ZuKaş 2026. A fork or competing implementation would be an adversarial relationship with the person who has done the primary intellectual and technical work on Plurality. The correct relationship is additive: ZuGov extends Plurality with sybil resistance (Humanode) and anti-collusion voting (MACI) and an epistemic overlay (The Grounding Engine). These are capabilities the Plurality SDK does not currently provide. The integration is a contribution, not a competition.

**Implications for implementation:**
- All Plurality-related code must be architecturally separable from the MACI and Grounding Engine layers.
- API contracts between ZuGov and the Plurality SDK must be documented so that Plurality SDK updates can be adopted without full rewrites.
- Any custom extensions to Plurality behavior must be implemented as wrappers, not modifications to the SDK internals.
- Co-authorship on The Epistemic Hole is offered to Weyl as a natural extension of this collaborative posture.

---

## D-009 — Single governance context for MVP (single-tenant)

**Status:** Locked
**Date:** 2026-02-28

**Decision:** The MVP supports exactly one governance context (ZuKaş 2026). Multi-community / multi-tenant support is explicitly out of scope until Phase 2.

**Rationale:** Multi-tenancy requires permission isolation, context separation, and namespace management that adds significant implementation complexity. Building it before we understand the single-context use case adds risk without adding value. ZuKaş is the test. Everything we learn there informs the multi-tenant architecture.

---

## D-010 — All votes are non-binding at the infrastructure level in Phase 1

**Status:** Locked
**Date:** 2026-02-28

**Decision:** During the ZuKaş Alpha, all vote outcomes are advisory to the ZuKaş organizing team. The escrow wallet integration does not trigger automated disbursements in Phase 1. Human execution of vote outcomes is required.

**Rationale:** Automated execution of governance decisions in an alpha environment with unproven smart contracts creates irreversible financial risk. Phase 1 is a research environment. Outcomes should influence real decisions (to validate that ZuGov produces real governance value) but should not trigger automated financial flows until the contracts and the process have been validated.

**Implications:** The multi-sig escrow is deployed in Phase 1, but disbursements require manual signer action. The MACI tally result is the input that triggers the human decision. This creates an auditable record without automation risk.

---

## D-011 — Epistemic Latency is a measured research output, not a marketing claim

**Status:** Locked
**Date:** 2026-02-28

**Decision:** The concept of Epistemic Latency is operationally defined and will be measured during ZuKaş Alpha. It is not used as a vague marketing term.

**Operational definition:** For a given proposal, Epistemic Latency = the time delta between (a) when the earliest available evidence relevant to the proposal's core claim was publicly accessible, and (b) the median voter's stated awareness of that evidence at the time of voting (measured via post-vote survey).

**Measurement method:** Post-vote survey administered to all voters on each proposal. Survey asks: "Were you aware of [specific evidence item surfaced by the Grounding Engine] before the Grounding Engine report?" Binary response. Median response determines the community's epistemic state at vote time. The Grounding Engine timestamps the evidence it cites.

**Rationale:** If we cannot measure Epistemic Latency, we cannot make credible claims that The Grounding Engine reduces it. The grant proposal ($2M) makes this claim. We need data to support it.

---

## D-012 — The Grounding Engine does not summarize proposals — it audits them

**Status:** Locked
**Date:** 2026-02-28

**Decision:** The Grounding Engine's output is a structured epistemic audit, not a summary or simplification of the proposal. It surfaces what voters might not know or might be wrong about. It does not help voters understand what the proposal says (that is the proposer's job).

**Output schema (required fields):**

```
{
  "proposal_id": "<id>",
  "audit_timestamp": "<ISO 8601>",
  "epistemic_flags": [
    {
      "type": "UNSTATED_ASSUMPTION" | "WEAK_EVIDENCE" | "HIGH_LATENCY" | "OUTCOME_AMBIGUITY" | "MISSING_COUNTERFACTUAL",
      "description": "<specific description>",
      "severity": "LOW" | "MEDIUM" | "HIGH"
    }
  ],
  "synthetic_futarchy": {
    "stated_outcomes": ["<outcome 1>", "<outcome 2>"],
    "probability_estimates": [
      {
        "outcome": "<outcome>",
        "p_success": 0.0–1.0,
        "confidence": "LOW" | "MEDIUM" | "HIGH",
        "basis": "<brief rationale>"
      }
    ]
  },
  "epistemic_latency_flag": true | false,
  "latency_note": "<if flagged, what evidence may be unavailable to voters>",
  "audit_model": "<model name and version used>",
  "advisory_disclaimer": "This audit is advisory only. It has no effect on voting outcomes."
}
```

This schema is locked for Phase 1. Extensions may be proposed for Phase 2.
