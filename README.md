# ZuGov

**Open source epistemic governance infrastructure for emergent communities.**

Every community has the same problem: a decision needs to be made, information is scattered, interests conflict, time is short. And most of the time, a vote is held — but what happened *before* the vote? Who read what? Which questions were asked, and which were never raised?

Voting is not the problem. The epistemic process before voting is the problem.

ZuGov was built to close this gap.

---

## What It Does

ZuGov is a governance SDK for any community — DAO, popup city, municipality, cooperative. It adds a structured epistemic layer before any vote:

1. **Grounding Engine** — A pre-vote epistemic auditor. Any proposal goes in. A structured report comes out: what it assumes, what's missing, what historical base rates say. Zero voting authority. Zero veto power. Only a report.

2. **Pol.is integration** — Opinion clustering and cross-tribal consensus mapping before deliberation.

3. **MACI voting** — Minimum Anti-Collusion Infrastructure. ZK-verified, bribery-resistant voting. On-chain verifiable results.

The guarantee: *every binding decision is made after all members have had access to a structured epistemic report, through a bribery-resistant, ZK-verified voting mechanism.*

---

## The Grounding Engine — Six Questions

For every proposal, the Engine produces a structured report answering:

| # | Question | Purpose |
|---|----------|---------|
| 1 | What does this proposal assume to be true? | Surface hidden premises |
| 2 | What is the historical base rate of similar decisions? | Precedent visibility |
| 3 | Which counterarguments are absent from the proposal? | Galaxy-brain resistance |
| 4 | How reversible is this decision, and at what cost? | Decision cost awareness |
| 5 | Who is affected, and how? | Distributional impact |
| 6 | How have similar communities resolved comparable decisions? | Comparative precedent |

The output format is fixed. It cannot be modified by the proposal author. This is the galaxy-brain resistance mechanism: a structured template makes manipulation visible.

---

## Philosophy — w/acc

**Wisdom Acceleration.** As AI expands the capacity to make and execute decisions at scale, collective wisdom capacity must scale at the same rate — or the gap between decision speed and decision quality becomes catastrophic.

ZuGov does not replace human judgment. It makes collective reasoning visible before the vote happens.

The Grounding Engine is designed as *AI as interface* — Vitalik Buterin's Jan 2024 taxonomy of safe crypto+AI applications. Not *AI as rules* (dangerous: adversarial optimization). Not *AI as player* (no decision authority). A structured report that communities reason against, not a verdict they accept.

---

## Architecture

```
INPUT
  └── Any proposal (free text)
       │
       ▼
GROUNDING ENGINE
  ├── Fixed 6-question template
  ├── LLM produces structured HTML report
  ├── Output: epistemic report (never pass/fail)
  └── Runtime: API (V0) → Local open-weight LLM (V1)
       │
       ▼
DELIBERATION LAYER
  ├── Pol.is session (opinion clustering)
  ├── Daily Agora (45-min structured discussion)
  └── Report must be read before deliberation begins
       │
       ▼
MACI VOTE
  ├── ZK-verified vote privacy
  ├── Bribery-resistant (changeable until close)
  └── On-chain verifiable result + ZK proof published
```

---

## Decision Cycle

```
Day 0   Proposal submitted (any member)
Day 1   Grounding Engine report published — accessible to all
Day 2   Pol.is session opens
Day 3   Daily Agora — 45-min structured deliberation
Day 4   Second Agora (if needed) + consensus check
Day 5   MACI vote opens (48 hours)
Day 7   Vote closes, ZK proof published, decision recorded
```

---

## Trust Boundaries

Honest systems declare their weaknesses. ZuGov's known trust assumptions:

| Not Guaranteed | Why | Mitigation |
|----------------|-----|------------|
| Grounding Engine is always correct | LLM output can be wrong | Community can formally challenge any finding |
| MACI coordinator is honest | Known MACI weakness | Threshold MACI in V1 removes single coordinator |
| Sybil-proof identity | ZK alone is insufficient | Pluralistic identity: Humanode + ZK + social graph |
| Perfect facilitation | Human error | Backup facilitator + session documentation |

---

## First Deployment — ZuKaş 2026

**April 10 – May 10, 2026. Kaş, Turkey.**

ZuKaş is a 30-day governance residency on the Lycian coast — the same coastline where the Lycian League built the world's first federal proportional democracy 2,400 years ago. Montesquieu read it in 1748 and wrote it into the Enlightenment. Madison read Montesquieu and wrote it into the American republic.

We are not nostalgic. We are asking: if they solved the coordination problem of their era here, what is the coordination problem of our era, and what would it look like to solve it in the same place?

Glen Weyl (creator of Quadratic Voting, RadicalxChange, the Plurality framework) in residence for one week to stress-test the governance experiments.

**This repository is the living technical record of that experiment.**

→ [zukascity.com](https://zukascity.com)

---

## Running ZuGov V0

### Requirements

- Web server (Vercel free tier sufficient)
- LLM API — GPT-4o or Claude (~$20–50/month for small communities)
- Pol.is instance (free at pol.is, or self-hosted)
- MACI deployment (requires Solidity dev, ~2 days setup)

### Minimum Human Resources

- 1 facilitator per decision cycle (no technical background required)
- 1 technical steward (MACI + deployment)
- Community: minimum 5 people

### Deploy

```bash
git clone https://github.com/tagore11/zugov
cd zugov
npm install
cp .env.example .env
# Add your LLM API key to .env
npm run dev
```

*Full deployment guide: [/docs/deploy.md](./docs/deploy.md)*

---

## Open Questions — Tested at ZuKaş

These are hypotheses, not claims. ZuKaş is the test:

1. Do decisions made with Grounding Engine reports differ measurably from decisions made without them?
2. Does a multi-model Engine (multiple LLMs, parallel reports) outperform single-model?
3. Does facilitator rotation produce better deliberation than elected facilitation?
4. In communities of 30–50 people, does MACI voting produce higher legitimacy perception than consensus hand-raising?

Results will be published as ZuKaş progresses. The data is the paper.

---

## Online Parallel Residency

Can't attend ZuKaş physically? Join the **Online Parallel Residency**.

Run the same governance experiments in your own community. Connect to the weekly sync from ZuKaş. Contribute your results to the comparative dataset.

Communities running ZuGov simultaneously produce comparative governance data — which is the data the space doesn't have yet. Every community adds to the historical base rate database. That database is the long-term value.

→ [Apply to participate](https://zukascity.com)

---

## Contributing

ZuKaş 2026 Genesis Nodes are the founding contributor community. Their participation, challenges, and findings constitute the first empirical version of ZuGov.

All contributors are credited in the first ZuGov research paper.

```
Issues      → What breaks, what's missing, what's wrong
Discussions → Governance design questions
PRs         → Code, documentation, facilitation guides
```

---

## License

MIT — free to use, fork, and deploy.

If you deploy ZuGov in your community, we'd like to know. Not to track you — to add your outcomes to the base rate database.

---

## Status

| Component | Status |
|-----------|--------|
| Grounding Engine V0 | 🟡 In development |
| Pol.is integration | 🟡 In development |
| MACI deployment | 🔴 Pre-deployment |
| Daily Agora format | ✅ Documented |
| Facilitation guide | ✅ Documented |
| Online Residency track | 🟡 Accepting interest |

*First production deployment: April 10, 2026.*

---

*ZuGov is a living protocol. This repository is updated continuously during ZuKaş 2026.*

*Built on the Lycian coast, for the coordination problems of our era.*
