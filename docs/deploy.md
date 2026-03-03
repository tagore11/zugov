# Deployment Guide — ZuGov V0

## Prerequisites

- Node.js 18+
- LLM API key (OpenAI or Anthropic)
- Pol.is account or self-hosted instance
- (Optional for full stack) MACI setup — see /docs/maci.md

## Quick Start

```bash
git clone https://github.com/tagore11/zugov
cd zugov
npm install
cp .env.example .env
```

Edit `.env`:
```
LLM_PROVIDER=openai          # or anthropic
LLM_API_KEY=your_key_here
LLM_MODEL=gpt-4o             # or claude-opus-4-6
POLIS_EMBED_URL=https://pol.is/your_conversation_id
```

```bash
npm run dev
# → http://localhost:3000
```

## Deploy to Vercel

```bash
npm install -g vercel
vercel --prod
```

Set environment variables in Vercel dashboard.

## First Decision Cycle

1. Open `localhost:3000/propose`
2. Submit a proposal (free text)
3. Grounding Engine generates report automatically
4. Share report URL with your community
5. Open Pol.is session
6. Run Daily Agora (45 min — see /facilitation/agora-guide.md)
7. Open MACI vote (or use manual consensus if MACI not deployed)

## Community Size Guidelines

| Size | Recommended Stack |
|------|-----------------|
| 5–20 people | Grounding Engine + manual consensus |
| 20–100 people | Full stack: Engine + Pol.is + MACI |
| 100+ people | Full stack + threshold MACI (V1) |

## Known Issues in V0

- Grounding Engine output quality depends on LLM quality — Claude claude-opus-4-6 recommended
- Pol.is requires minimum ~10 participants for meaningful clustering
- MACI coordinator trust assumption — see /docs/trust-model.md

*This document is updated as ZuKaş testing progresses.*
